How to Contribute
=================

Choose a project
----------------

**ds4es** projects are community efforts, and everyone is welcome to contribute. There are many ways to contribute. Improving the documentation is no less important than coding. 

* This documentation use Sphinx and is hosted at https://github.com/ds4es/doc.
* Projects are hosted in different repos under https://github.com/ds4es

We have also setup a bunch of empty project just waiting for you:

* **empty templated projects** with the Cookiecutter Data Science project structure

.. figure::  _static/images/contributing/empty-templated-project.png
   :align:   center

* **empty projects** if another structure is needed for your project 

.. figure::  _static/images/contributing/empty-project.png
   :align:   center


.. note::

  As soon as possible, any project should have a README.md filled with the minimal informations describing how to install and run the project as it is.

Edit your choosen project
-------------------------

To contribute whether for this documentation or any ds4es GitHub repo **in brief:** start by forking it on GitHub, edit your forked version of the repo and submit a "pull request".

**In details:**

1. `Create a GitHub account <https://github.com/join>`_ if you do not 
   already have one.

2. On GitHub under the project you want to contribute click on the **Fork** button near the top of the page. This creates a copy of the code under your GitHub user account. 

.. figure::  _static/images/contributing/fork.jpg
   :align:   center

From there you have 2 options to make changes to your fork:

* :ref:`option-a` at https://github.com/your_user_name/repo_name
* or :ref:`option-b`

.. _option-a:

Option A: Edit changes directly on GitHub
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3. Edit changes through the GitHub web interface at https://github.com/your_user_name/repo_name

Consider this option for quick fixes especially for documentation otherwise it will be better to follow Option B.

Once done follow instructions from :ref:`submit-changes`.

.. _option-b:

Option B: Edit changes on a local computer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pre-requisite: `Having Git installed <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_

3. Clone the forked repo from your GitHub account to a local working directory::

		git clone https://github.com/your_user_name/repo_name
		cd repo_name

A git clone will also setup the alias ``origin`` referring to this remote repository (to this url). 

4. We will define another alias pointing the original repository with the alias name ``upstream``. It will be used to keep your repository
   synchronized with the latest changes::

		git remote add upstream https://github.com/ds4es/repo_name

You have now a git repository properly configured. Next steps describe the process of modifying code and submitting a pull request:

5. Working with others, take the habit on a regular basis to synchronize your master branch with the upstream master branch::
		
		git checkout master
		git pull upstream master

The ``git checkout`` command lets you navigate between branches.

6. Create and navigate to a new feature branch to hold your development changes::

		git checkout -b my_feature_branch

7. Make the changes on your feature branch on your computer. It's good
   practice to never work on the ``master`` branch!
   When you're done editing, save your changes locally with ``add`` and ``commit``::

   		# Add all changes to the staging area
		git add . 
		# To add only a specific file do: git add filename
		# Captures a snapshot of the project's currently staged changes in a commit
		git commit -m "commit descriptive message"

   , then push the changes to your fork on GitHub::

		git push -u origin my_feature_branch

.. _submit-changes:


Submit your changes to the original GitHub repo
-----------------------------------------------

To propose your changes to the original GitHub repo (https://github.com/ds4es/repo_name) you have to create a pull request that will send an email to the committers.

8. On GitHub, from your fork: https://github.com/your_user_name/repo_name, GitHub noticing your changes should propose you a **Compare & pull request** button. (You can also click on **New pull request > Create pull request**)

.. figure::  _static/images/contributing/pull-request-02.png
   :align:   center

9. Select the branch of the upstream repository you'd like to merge changes into and select the branch you made your changes in.

.. figure::  _static/images/contributing/pull-request-01.png
   :align:   center


10. Type a title and description for your pull request. 

.. figure::  _static/images/contributing/pull-request-03.png
   :align:   center

11. And click **Create pull request** to create a pull request that is ready for review.


Keep your local feature branch synchronized
-------------------------------------------

It is a good pratice to keep your local feature branch synchronized with the latest changes of the main repository:

		git fetch upstream
		git merge upstream/master


Resolve conflicts
-----------------

You might need to solve conflicts, for that purpose check the
`Git documentation related to resolving merge conflict using the command
line <https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line/>`_.

.. note::

  The `Git documentation <https://git-scm.com/documentation>`_ http://try.github.io is an excellent resource to get started with git, and understanding all of the commands shown here.


Pull request checklist
----------------------

//TODO 
