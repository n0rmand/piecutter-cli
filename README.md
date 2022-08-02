<div align="center">
    <img src="statics/logo.png" width="250" />
    <h4>
        An open-source CLI app to build your entire ML project, from research to production. <br />
        Piecutter-CLI 0.1.0 is released! :rocket:
    </h4>
    <p>
        <img src="https://img.shields.io/pypi/pyversions/piecutter-cli" />
        <img src="https://badge.fury.io/py/piecutter-cli.svg" />
        <img src="https://img.shields.io/pypi/l/piecutter-cli" />
    </p>

| :exclamation:  This package is starting as a personal project and is in it's initial development phase.   |
|-----------------------------------------------------------------------------------------------------------|
</div>


## :notebook: Base Piecutter Project Structure
The project structure generated by Piecutter for you to use in the research/modeling phase of your project.

    ------------
        ├── Makefile              -> The Makefile of your project.
        ├── README.md             -> The README.md file for describing your project.
        ├── requirements.txt      -> List of requirements to run your code.
        ├── data                  -> The dataset of your project at different stages.
        │   ├── raw
        │   ├── processed
        │   ├── finalized
        ├── notebooks             -> Your jupyter notebooks.
        ├── references            -> Any external reference used in your project.
        ├── results               -> Results folder to store figures, tables and trained models.
        │   ├── figures
        │   ├── models
        │   ├── tables
        ├── tests                 -> Write tests to your scripts here!
        |    ├── test_predict.py
        |    ├── test_train.py
    ------------

## :interrobang: Why Piecutter?
Piecutter CLI is a project highly inspired by the well-known <a href="https://github.com/cookiecutter/cookiecutter" target="_blank">Cookiecutter</a> project.

*But why another CLI app inspired in a well established one?*

A lot of data scientists need to put models into production right after the modeling phase :crystal_ball:, and Cookiecutter doesn't help with this important step of the machine learning lifecycle :recycle:. Moreover, the project template generated by Cookiecutter :cookie: has some files and folders that we, as data scientists, don't use very often in a research-to-production environment :microscope:. Piecutter generates a much more cleaner structure of folders and files for the research phase of a ML project.

*And about the production phase?*

Piecutter implements a standardized way to package :zap: and put trained models and ML pipelines into production by using BentoML :rocket:. BentoML is a tool to standardize the process of ML model deployment by building an inference API around your trained pipeline as well as containerizing this application with docker :whale:, making it available for deployment right off the bat.

*But why should I use Piecutter CLI if BentoML exists?*

Well, BentoML's development is in full swing :steam_locomotive:, but this is good and bad at the same time. Although very standardized, the BentoML team constantly make significant changes on the package design :fire:, which affects not only the user experience, but also makes the official documentation outdated very fast :cyclone:. Piecutter puts all this mess :poop: out of your sight and gives you few commands for you to generate your entire research environment structure as well as to generate your production-ready inference API code in a matter of seconds :alarm_clock:!

Moreover, BentoML isn't capable of generating the research and the production structure in the same codebase :computer:, it isn't meant for that actually. Piecutter :cake: takes care of this integration and on top of that implements *Custom Runnables* for any unsupported framework as well as for more complex AI pipelines just by running one or two commands :tada:.

## Features
+ Cross-platform: Windows, Linux and Mac are supported.
+ Works with Python 3.8, or a newer version.
+ Code formatting with Python Black.

## :alien: Who Should Use Piecutter?
+ Anyone starting a career in data science.
+ People who like low-code solutions.
+ Data scientists with no experience in software engineering and want a standardized solution for model packaging and deployment.

## :heavy_check_mark: Supported Frameworks
+ <a href="https://pycaret.org/" target="_blank">PyCaret</a>

*OBS.: The first version of Piecutter has just been released and for now we only have support for **PyCaret** automated deployment code generation. (You can expect support for all major frameworks in the coming days (I'm developing this package in my spare time, as fast as I can)*.

## :bookmark_tabs: API Docs

## :page_with_curl: Table of Contents
1. :satellite: Installation
2. :heavy_check_mark: Check Version
3. :closed_book: Open Documentation
4. :new: Create a New Project
5. :new: Generate a New Bento
6. :carousel_horse: Generate a New API Route
***

###  Installation
Piecutter is available as a PyPI package, to install it, just run:

    $ pip install piecutter-cli

### Check Version
Run the `version` command to check if piecutter is installed:

    $ piecutter version

### Open Documentation
Use the `docs` command to quickly open the official documentation (this one you're reading) on your browser:

    $ piecutter docs

### Create a New Project
To generate a new project template, run:

    $ piecutter new project --name diamonds-prices-regression

*In the example above we've created a new project called `diamonds-prices-regression` with the following structure*:

    ------------
        ├── Makefile              -> The Makefile of your project.
        ├── README.md             -> The README.md file for describing your project.
        ├── requirements.txt      -> List of requirements to run your code.
        ├── data                  -> The dataset of your project at different stages.
        │   ├── raw
        │   ├── processed
        │   ├── finalized
        ├── notebooks             -> Your jupyter notebooks.
        ├── references            -> Any external reference used in your project.
        ├── results               -> Results folder to store figures, tables and trained models.
        │   ├── figures
        │   ├── models
        │   ├── tables
        ├── tests                 -> Write tests to your scripts here!
        |    ├── test_predict.py
        |    ├── test_train.py
    ------------

*You can check out this real world project implemented in our <a href="https://github.com/g0nz4rth/piecutter-cli/tree/main/examples/diamonds-prices-regression" target="_blank">example/diamonds-prices-regression</a> folder*.

### Generate a New Bento
After having finished your modeling phase, use the `generate bento` command to generate your model deployable code:

    $ piecutter generate bento --base-framework pycaret

And a folder with the following structure will be added to your project directory:

    ------------
        ├── bentofile.yaml          -> File used by bento to build the BentoML image.
        ├── predict.py              -> Script to generate predictions with your trained model.
        ├── service.py              -> The BentoML service file, which starts the Bento server.
        ├── train.py                -> Script to retrain your model (and serialize it in the current dir)
    ------------

*You can see the real world version of this file in the <a href="https://github.com/g0nz4rth/piecutter-cli/tree/main/examples/diamonds-prices-regression/bento" target="_blank">examples/diamonds-prices-regression/bento</a>*.

| :warning: WARNING          |
|:---------------------------|
| Please, execute `generate bento` from the outside of your project root dir. This bug will be fixed in the next release!      |

### Generate a New API Route
After generating a `bento`, you need to generate at least one API endpoint to serve your model:

    $ piecutter generate api-route predict --no-secured

The `generate api-route` command has two possible [required] flags:
+ `--secured` to generate a JWT-secured API endpoint (Piecutter also generates an auth token for you).
+ `--no-secured` to generate an API endpoint with no security implemented (anyone can reach the endpoint).

*In the example above we've generated a new not-secured API route (endpoint) called `predict`*.

*In the <a href="https://github.com/g0nz4rth/piecutter-cli/tree/main/examples/diamonds-prices-regression" target="_blank">example/diamonds-prices-regression</a> project I've generated an unsecure API endpoint for inference*.
