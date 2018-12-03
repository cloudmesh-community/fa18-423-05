## Overview:
This document explains how to access Microsoft Azure and how Azure is used to run programs in the cloud server.

## Processing:
  ### Previous Method 
  **Get Azure set up**
  
  Go to https://portal.azure.com/ to register an Azure account. Once you get an account for the Azure, you can go to Azure Portal to set up all the tools you need. The searching bar at the very top could help you access to any resource you need in the Azure.
  
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

  ### Current Method
  **Get Azure set up**
  
  Navigate to the Azure Portal, and then select the Virtual Machine blade from the side manu to set up a new virtual machine. The first step is to select subscription, which is Free Trial for our usage. Then, select the resource group, which is like a folder, for the virtual machine and also name it. After that, the region of the virtual machine should be selected. There are multiple options for the region, but the closest one is recommanded for a faster access. Once those steps are finished, size the of virtual machine should be determined. There are different options for the memory and storage, which are all in different price. Next, an administrator account would be registered for future access to the virtual machine. Finally, there is one option for selecting inbound ports, where SSH should be selected for easier connection. Then click on the "preview and create" button to finish setting up the virtual machine.

  **Accessing the Server**
  
  To access the server, navigate to the virtual machine on the portal and select connect botton on the top of the panel for connection information. Once the connect botton is clicked, there would be a side panel showing the address and portal number of the server. Through Git Bash or Terminal, we can connect to the server with those information and the administrator account we've created before.

  **Uploading Files**
  
  To uploading files to the server, we can use WinSCP or Cyberduck to connect to the server and manage files in the server easily. 

  **Execute Code**
  
  Once files are uploaded to the server, we can return back to the Git Bash or Terminal to execute python code by running the command:

  > "python3 <file name>"

  To install python modules, this command could be used:

  > "pip install <module name>"

  **Disclaimer**
  
  The previous method used cannot successfully execute the code for some reason, because it crashes the server every time when it is executed.
  The current method used can make the code successfully run, though it takes a really long time for the code to full executed, due to the size of data being input is that large.
