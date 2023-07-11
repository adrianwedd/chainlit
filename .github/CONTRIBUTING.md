# Contribute to Chainlit

To contribute to Chainlit, you first need to setup the project on your local machine.

## Table of Contents
<!--
Generated using https://ecotrust-canada.github.io/markdown-toc/.
I've copy/pasted the whole document there, without the previous two headings.
-->

- [Local setup](#local-setup)
  * [Requirements](#requirements)
  * [Setup the repo](#setup-the-repo)
  * [Install JS dependencies](#install-js-dependencies)
  * [Install python dependencies](#install-python-dependencies)
- [Start the UI](#start-the-ui)
- [Setup the server](#setup-the-server)
  * [Install from local sources](#install-from-local-sources)
  * [Start the server](#start-the-server)
- [Run the tests](#run-the-tests)
  * [Run one test](#run-one-test)
- [Only contribute to one side of the project](#only-contribute-to-one-side-of-the-project)
  * [Only contribute to the frontend](#only-contribute-to-the-frontend)
  * [Only contribute to the server](#only-contribute-to-the-server)

## Local setup

### Requirements

1. Python >= `3.8` 
2. Poetry ([See how to install](https://python-poetry.org/docs/#installation))
3. NodeJS >= `16` ([See how to install](https://nodejs.org/en/download))


### Setup the repo

With this setup you can easily code in your fork and fetch updates from the main repository.

1. Go to https://github.com/Chainlit/chainlit/fork to fork the chainlit code into your own repository.
2. Clone your fork locally
```sh
$ git clone https://github.com/YOUR_USERNAME/YOUR_FORK.git
```
3. Go into your fork and list the current configured remote repository.
```sh
$ git remote -v
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push) 
```
4. Specify the new remote upstream repository that will be synced with the fork.
```sh
$ git remote add upstream https://github.com/Chainlit/chainlit.git
```
5. Verify the new upstream repository you've specified for your fork.
```sh
$ git remote -v
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
> upstream  https://github.com/Chainlit/chainlit.git (fetch)
> upstream  https://github.com/Chainlit/chainlit.git (push)
```

### Install JS dependencies

```sh
npm install
npm run installUiDeps
```

### Install python dependencies

```sh
cd src
poetry install
```

Make sure you have the Python code formatter `black` installed as it is used in a pre-commit hook. Run `pip install black` if needed.

## Start the UI

```sh
npm run buildUi
cd src/chainlit/frontend
npm run dev -- --port 5174
```

The `buildUi` step is currently needed by the server.

If you visit `http://127.0.0.1:5174/`, it should say that it can't connect to the server.

## Setup the server

### Start the server

Start by running `src/chainlit/hello.py` as an example.

```sh
cd src
poetry run chainlit run chainlit/hello.py -h
```

The `-h` parameter (headless) means the UI will not automatically open.

You should now be able to use the UI you launched previously on `http://127.0.0.1:5174/`.

If you've made it this far, you can now replace `chainlit/hello.py` by your own target. 😎

## Run the tests

Run `npm test`

Once you create a pull request, the tests will automatically run. It is a good practice to run the tests locally before pushing.

### Run one test

1. Find the folder containing the e2e test that you're looking for in `cypress/e2e`.
2. Run `SINGLE_TEST=FOLDER npm test` and change FOLDER with the folder from the previous step (example: `SINGLE_TEST=scoped_elements run test`).

## Only contribute to one side of the project

This is the easiest solution if you want to only make a change in the UI or the server.

Start with following the steps from the [Local setup](#local-setup).

### Only contribute to the frontend

1. Change the server url in [src/chainlit/frontend/src/api/index.ts](/src/chainlit/frontend/src/api/index.ts) to match your target chainlit server. Below is an example using a public chainlit server. Don't forget to change the configuration back before commiting.

```js
const devServer = 'https://img-gen.chainlit.app/';
```
2. Follow the steps from [Start the UI](#start-the-ui).

### Only contribute to the server

1. Build the UI.

```sh
npm run buildUi
```

2. Follow the instruction from [Install from local sources](#install-from-local-sources).

3. Run the server without the `-h` flag. Replace `target.py` with the file you want to run. You can use `src/chainlit/hello.py` as an example.

```sh
poetry run chainlit run target.py
```

4. Any time you've made a change, restart the server from the previous step.
