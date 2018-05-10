# Deploy a docker image to Azure Web Apps for Containers

## Overview

VS Code extensions are a way to customize your development environment with the exact tools you need. The Docker and Azure extensions make it easy to build and deploy containerized applications from Visual Studio Code and includes functionality:

- Automatic Dockerfile and docker-compose.yml file generation
- Syntax highlighting and hover tips for docker-compose.yml and Dockerfile files
- IntelliSense (completions) for Dockerfile and docker-compose.yml files
- Linting (errors and warnings) for Dockerfile files
- Command Palette (F1) integration for the most common Docker commands (e.g. Build, Push)
- Explorer integration for managing Images and Containers
- Deploy images from DockerHub and Azure Container Registries to Azure App Service

## What is covered in this lab?

In this lab, you will:

- Create a Docker image using a provided Python application and Dockerfile
- Create an Azure Container Registry and Azure Web App
- Configure your Web App to use your Docker image from the Azure Container Registry

## Part A: Create a Docker container in VS Code

1. [ ] Double click on the Visual Studio Code icon on the desktop to open Visual Studio Code

2. [ ] In the `app/main.py` file, modify the "Hello World!" message on line 6 to a fun message of your choice, type in some HTML if you want!

3. [ ] Right-click on the `Dockerfile` file and select `Build Image` to build the docker image. Name the image `pyconlabs.azurecr.io/<app_name>:latest`, where `<app_name>` is a globally unique name, e.g. `<your_name_no_spaces>pycon`.

!IMAGE[Build Docker Image](Images/BuildImage.png)

## Part B: Sign in to Azure

4. [ ] Press `Ctrl+Shift+P` to open the Command Palette, type and/or select `> Azure: Sign In`.

!IMAGE[Build Docker Image](Images/AzureSignIn.png)

5. [ ] Click the `Copy + Open` button, and login using the email and password listed above (you can use the copy button to copy the email and password).

## Part C: Create Web App from Container

6. [ ] In the docker tab of the explorer, right-click on the container named `pyconlabs.azurecr.io/<app_name>` and select Push

!IMAGE[Push docker image](Images/PushDockerImage.png)

7. [ ] Right->click Deploy to Azure App service, 

!IMAGE[Push docker image](Images/DeployImageToAppService.png)

In the series of menus enter:
 - `DockerLab` for the resource group
 - `DockerLabPlan` for the app service plan name
 - `B1 Basic` for the plan SKU
 - The same `<app_name>` you picked above for the site name

## Part D: Final configuration

Finally, we need to set the port number on the site to match the port on the Docker container.

8. [ ] Go to the Azure tab, expand the subscription and web site, right-click on Application settings and select `Add New Setting...`. Name the setting `WEBSITES_PORT`, and set the value to `8000`.

!IMAGE[Push docker image](Images/AddSetting.png)

9. [ ] Right-click on the site and select `Restart`, and wait for the site to finish restarting

!IMAGE[Push docker image](Images/RestartWebApp.png)

10. [ ] Right-click on the site and select `Browse`, or browse to ```<app_name>.azurewebsites.net``` to see your message! It may take a minute to load.
