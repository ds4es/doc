Apache Kafka
============

Source:
* https://www.digitalocean.com/community/tutorials/how-to-install-apache-kafka-on-centos-7
* https://kafka.apache.org/quickstart

Prerequisites
-------------

Install prerequisites package

	sudo dnf install java-11-openjdk wget

Creating a User for Kafka
-------------------------

Since Kafka can handle requests over a network, you should create a dedicated user for it. This minimizes damage to your CentOS machine should the Kafka server be compromised. 

Create a user for Kafka

	sudo useradd kafka -m

Set the password for your ``kafka`` user

    sudo passwd kafka

Give your ``kafka`` user root privileges

	sudo usermod -aG wheel kafka

Log into this new account

	su -l kafka

Downloading and Extracting the Kafka Binaries
---------------------------------------------

Download the Kafka binaries in ``/home/kafka/Downloads``

	wget -P ~/Downloads https://downloads.apache.org/kafka/2.5.0/kafka_2.13-2.5.0.tgz

Create a directory called kafka and change to this directory

	mkdir ~/kafka && cd ~/kafka

Extract the archive in it

	tar -xvzf ~/Downloads/kafka_2.13-2.5.0.tgz --strip 1

Configuring the Kafka Server
----------------------------

Kafka’s default behavior will not allow us to delete a topic, the category, group, or feed name to which messages can be published. To modify this, let’s edit the configuration file. 

To allow us to delete Kafka topics, add the following to the bottom of the file

	echo '
	delete.topic.enable = true
	' | tee -a ~/kafka/config/server.properties

Save and close the file

Creating Systemd Unit Files and Starting the Kafka Server
---------------------------------------------------------

Zookeeper 
^^^^^^^^^

Create the unit file for Zookeeper

	echo "
	[Unit]
	Requires=network.target remote-fs.target
	After=network.target remote-fs.target

	[Service]
	Type=simple
	User=kafka
	ExecStart=/home/kafka/kafka/bin/zookeeper-server-start.sh /home/kafka/kafka/config/zookeeper.properties
	ExecStop=/home/kafka/kafka/bin/zookeeper-server-stop.sh
	Restart=on-abnormal

	[Install]
	WantedBy=multi-user.target
	" | sudo tee /etc/systemd/system/zookeeper.service

Save and close the file

Kafka 
^^^^^

Create the unit file for Kafka

	echo "
	[Unit]
	Requires=zookeeper.service
	After=zookeeper.service

	[Service]
	Type=simple
	User=kafka
	ExecStart=/bin/sh -c '/home/kafka/kafka/bin/kafka-server-start.sh /home/kafka/kafka/config/server.properties > /home/kafka/kafka/kafka.log 2>&1'
	ExecStop=/home/kafka/kafka/bin/kafka-server-stop.sh
	Restart=on-abnormal

	[Install]
	WantedBy=multi-user.target
	" | sudo tee /etc/systemd/system/kafka.service

Save and close the file

To avoid an error caused by the fact no rule in SELinux policy allows the specific access: allow non-transitioning execution of a file with context config_home_t by a process running in init_t domain.

Generate a local policy module to allow this access:

	sudo ausearch -c '(start.sh)' --raw | sudo audit2allow -M zookeeper-server-start.sh

	sudo semodule -X 300 -i zookeeper-server-start.sh.pp

	sudo ausearch -c 'zookeeper-serve' --raw | sudo audit2allow -M kafka-server-stop.sh

	sudo semodule -X 300 -i kafka-server-stop.sh.pp


Start Kafka

	sudo systemctl start kafka

Check a Kafka server is running

	journalctl -u kafka

Enable kafka on server boot

    sudo systemctl enable kafka

Testing the Installation
^^^^^^^^^^^^^^^^^^^^^^^^

Publishing messages in Kafka requires:

* A producer, which enables the publication of records and data to topics.
* A consumer, which reads messages and data from topics.

Create a topic named ``TutorialTopic``:

    ~/kafka/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic TutorialTopic

You will see the following output:

Output
Created topic "TutorialTopic".

You can create a producer from the command line using the ``kafka-console-producer.sh`` script. It expects the Kafka server’s hostname, port, and a topic name as arguments.

Publish the string ``"Hello, World"`` to the ``TutorialTopic`` topic by typing:

    echo "Hello, World" | ~/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic TutorialTopic > /dev/null

Next, you can create a Kafka consumer using the ``kafka-console-consumer.sh`` script. It expects the ZooKeeper server’s hostname and port, along with a topic name as arguments.

The following command consumes messages from ``TutorialTopic``. Note the use of the ``--from-beginning`` flag, which allows the consumption of messages that were published before the consumer was started:

    ~/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TutorialTopic --from-beginning

If there are no configuration issues, you should see ``Hello, World`` in your terminal:

Output
Hello, World

The script will continue to run, waiting for more messages to be published to the topic. Feel free to open a new terminal and start a producer to publish a few more messages. You should be able to see them all in the consumer’s output.

When you are done testing, press ``CTRL+C`` to stop the consumer script. Now that we have tested the installation, let’s move on to installing KafkaT. 