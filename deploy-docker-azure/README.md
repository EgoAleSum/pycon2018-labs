# Deploy a docker image to Azure Web Apps for Containers

Starting with the sample docker container provided, you will create an Azure Web App and deploy the docker container.

[ ] 1. In the docker tab of the explorer, right click on the container named `pycondemos.azurecr.io/docker-pycondemo` and select Push

[ ] 2. Press `Ctrl-Shift-P` and type + select `Azure: Open Bash in Cloud Shell`

![alt text](Images/BashCloudShell.png)

[ ] 3. In the terminal run the following command to create a new webapp: 

`az webapp create --name MyDockerWebApp --resource-group PyConDemos --plan PyConDemosPlan --deployment-container-image-name "pycondemos.azurecr.io/docker-pycondemo"`

Feel free to change MyDockerWebApp to a name of your choosing, just remember to use the same name in the following steps.

[ ] 4. Run the following command to configure the port number:

`az webapp config appsettings set --name MyDockerApp --resource-group WebAppsDemos --settings  WEBSITES_PORT=5000`

[ ] 5. Run the following to configure the web app to pull from the registry:

`az webapp config container set --name MyDockerApp --resource-group PyConDemos --docker-custom-image-name pycondemos.azurecr.io/docker-pycondemo --docker-registry-server-url https://pycondemos.azurecr.io --docker-registry-server-user pycondemos --docker-registry-server-password <TODO>`

[ ] 6. Right-click on MyDockerWebApp in the Azure App Service section of the explorer, and select restart.

![alt text](Images/RestartWebApp.png)

[ ] 7. Browse to `mydockerwebapp.azurewebsite.net` and see your app running!