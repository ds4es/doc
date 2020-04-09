This repo aims to support the [Data Science for Emergency Services](https://ds4es.github.io/doc/) initiative that is a community effort where everyone is welcome to contribute.

There are many ways to contribute but improving this documentation is critical.

Please refer to [How to contribute](https://ds4es.github.io/doc/contributing.html) if you are not sure how to contribute to a GitHub repo.

### Prerequisites to build this Sphinx documentation

To build and preview this documentation on your laptop you need to have with `python`, `pip` and the `sphinx` and `sphinx-rtd-theme` packages installed. (See [Setup your working environment](https://ds4es.github.io/doc/working_environment.html) for more details)

You can install `sphinx` and `sphinx-rtd-theme` with `pip`:
```
pip install sphinx
pip install sphinx-rtd-theme
```

### Build and preview the documentation

From this repo root folder on your computer
```
cd ./doc
```

..to rebuild the HTML Sphinx documentation files after changes, execute: 
```
sphinx-build -b html ./source ./docs
```

To preview it, you can start an http server with Python:
```
python -m http.server 8080 --directory ./docs
```

Your Sphinx documentation will be serve at [http://0.0.0.0:8080](http://0.0.0.0:8080).

Open this URL with the browser of your choice.
