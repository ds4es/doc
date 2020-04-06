## Setup a Git repository to serve your Sphinx documentation 

On GitHub, create a new repository. For this example `my_sphinx_repo` is taken as **Repository name**.

Once created, somewhere on your local machine.
```
git clone https://github.com/username/my_sphinx_repo
cd ./my_sphinx_repo
```

Setup a repo dedicated to serve Sphinx documentation
```
sphinx-quickstart
```
Fill the asked parameters
```
> Separate source and build directories (y/n) [n]: y
> Project name: ds4es
> Author name(s): ds4es
> Project release []: 0.0.1
> Project language [en]: en
```
Specifying `y`, we choose to store our Sphinx editable files in `./source`.

Build Sphinx in a `./docs` subdirectory (This will suit GitHub to serve your documentation).
```
sphinx-build -b html ./source ./docs
# Add an empty `.nojekyll` file in `docs` repository 
# to make GitHub to not try interpret files as part of a Jekyll site
touch ./docs/.nojekyll
```

Push your Sphinx documentation on GitHub
```
git add .
git commit -m "First commit"
git push
```

On your GitHub go back to your project repo and in **Settings** > **GitHub Pages** set **Source** as `master branch /docs folder`.

Wait a bit and refresh this **Settings** page, when under **GitHub Pages**you will a green notification **Your site is published at https://xxxx.github.io/my_sphinx_repo/** your Sphinx will be available.

To rebuild locally your HTML Sphinx documentation files after modification reexcute 
```
sphinx-build -b html ./source ./docs
```

## Check your Sphinx documentation locally

Start an http server
```
python -m http.server 8080 --directory ./docs
```
Your Sphinx documentation will be serve at `0.0.0.0:8080`

## Using Markdown syntax in a Sphinx documentation
Install recommonmark
```
pip install --upgrade recommonmark
```

Add `recommonmark` to the list of configured extensions defined in `./source/conf.py`:
```
extensions = ['recommonmark']
```

## To install a custom theme
Install the theme you want, here `sphinx_rtd_theme`
```
pip install sphinx_rtd_theme
```
In `./source/conf.py`, comment the previous theme:
```
#html_theme = 'alabaster'
```

and declare your new theme
```
import sphinx_rtd_theme

html_theme = 'sphinx_rtd_theme'

html_theme_path = [sphinx_rtd_theme.get_html_theme_path()] 
```