## Overview:
This document explains how to access Microsoft Azure and how Azure is used to run programs in the cloud server.

## Processing:
  **Get Azure set up**
  Once you get an account for the Azure, you can go to Azure Portal to set up all the tools you need. The searching bar at the very top could help you access to any resource you need in the Azure.
  
  **Create a Python web app through Azure app services**
  First of all, clone the folder containing code files and data files from Github with Bash/Terminal into your local machine. 
  Before other operation, run the Python files locally to check if the program runs well.
  Then, back to the Azure portal which is set up previously, open the Cloud Shell for following operations.
  The very first step to take is to create a deployment user, if you do not already have one. The command should be used is:
  
  > "az webapp deployment user set --user-name <username> --password <password>"

  where <username> and <password> should be replaced with the username and password you are going to use. After successfully run the command, there should be a JSON output with your password shown as null.
  The user name and the password should be recorded for future use.
  After that, you have to create a resource group to make it easier to manage, by using the command:

  > "az group create --name myResourceGroup --location "East US""

  For this command, "East US" could be replaced by other regions where Azure is avaliable, but for the connection stability, it would be best to use the closest region.
  Then, an Azure App Service plan should be created. The command to be used is:

  > "az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1 --is-linux"

  When those steps are done, it is the time to create the web app. Still working on the Azure Cloud Shell, type the following command lines:

  > "az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "PYTHON|3.7" --deployment-local-git"

  These command lines would return an output starting with:

  > "Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'"

  This URL of git should be kept as you will need it later for connection.

  After those steps, back to local bash for the following operations. The first step is to add an Azure remote to the local Git repository by using the command:

  > "git remote add azure <deploymentLocalGitUrl-from-create-step>"

  And then use:

  > "git push azure master"

  to push to Azure form Git repository. This command should take a bit longer to process. Once the processing is done, you can go back to the Azure portal to access the App Services to find the one just being created. Click on that service and then go to the side bar to click on the SSH under Development Tools, and then, you can access all the files you've push on the cloud server.
   
