Data Science Project Template
=============================

Each ds4es data science project will be materialized by a GitHub repo.

For the sake of reproducibility we advice a logical, reasonably standardized, but flexible data science project structure inspired by https://drivendata.github.io.

.. code-block:: default

	.
	├── .env               <- Store your secrets and config variables in a special file
	├── .gitignore         <- Avoids uploading data, credentials, 
	|                         outputs, system files etc
	├── env                <- Will contain the Python executable files and installed libraries for your virtualenv environment
	├── requirements.txt   <- Install the environment dependencies with: `pip install -r requirements.txt`
	├── LICENSE
	├── Makefile           <- Makefile with commands like `make data` or `make train`
	├── README.md          <- The top-level README for developers using this project.
	├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
	├── data
	│   ├── external       <- Data from third party sources.
	│   ├── interim        <- Intermediate data that has been transformed.
	│   ├── processed      <- The final, canonical data sets for modeling.
	│   └── raw            <- The original, immutable data dump.
	├── docs                <- Space for Sphinx documentation
	├── models             <- Trained and serialized models, model predictions, or model summaries
	├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
	│   |                     the creator's initials, and a short `-` delimited description, e.g.
	│   |                     `1.0-jqp-initial-data-exploration`.
	│   ├── eda            <- Placholder for describing exploratory data analysis
	│   ├── evaluation     <- Placholder for describing model evaluation
	│   ├── modeling       <- Placholder for describing how the model is built
	│   └── poc            <- Describing Proof-of-Concept
	├── references         <- Data dictionaries, manuals, etc.
	├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
	│   └── figures        <- Generated graphics and figures to be used in reporting
	├── src                <- Source code for use in this project.
	│   ├── __init__.py    <- Makes src a Python module
	│   ├── data           <- Scripts to download or generate data
	│   │   └── make_dataset.py
	│   ├── features       <- Scripts to turn raw data into features for modeling
	│   │   ├── build_features.py
	│   ├── models         <- Scripts to train models and then use trained models to make
	│   │   │                 predictions
	│   │   ├── predict_model.py
	│   │   └── train_model.py
	│   └── visualization  <- Scripts to create exploratory and results oriented visualizations
	│       └── visualize.py
	└── tox.ini               <- Automate testing, cf. https://tox.readthedocs.io/en/latest/.

* `data`: Folder for storing subset data for experiments. It includes both raw data and processed data for temporary use.
* `docs`:
* `models`: Folder for storing binary (json or other format) file for local use.
* `notebooks`: Storing all notebooks includeing EDA and modeling stage.
* `references`:
* `reports`:
* `src`: Stores source code (python, R etc) which serves multiple scenarios. During data exploration and model training, we have to transform data for particular purpose. We have to use same code to transfer data during online prediction as well. So it better separates code from notebook such that it serves different purpose.
