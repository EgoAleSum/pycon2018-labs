# Create a Docker container using VS Code

## Overview

VS Code has an integrated terminal which allows for a convenient development workflow.

## What is covered in this lab?

In this lab, you will:

* Use VS Code to build a Docker container and run it locally

## Part A: Build the Docker container

Starting with the sample flask app and Dockerfile you will create, build and run a docker container with VS Code.

1. [ ] In the `app/main.py` file, modify the "Hello World!" message on line 6 to a fun message of your choice, type in some HTML if you want!

2. [ ] Press ``Ctrl-` `` to open the integrated terminal in VS Code

3. [ ] Build the image, for name pick a name (e.g. your name without spaces)
`docker build --rm -t dockerlab:latest .`

## Part B: Run the Docker container

4. [ ] Run the container using the following command:
`docker run --rm -it -p 8000:8000 dockerlab:latest`

5. [ ] Open the browser, and browse to `localhost:8000` to view the app!

6. [ ] In the VS Code integrated terminal, press `Ctrl-C` to stop the container

To learn about ways to deploy Docker containers on Azure, explore the other lab options