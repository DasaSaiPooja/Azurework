This repository contains a simple ASP.NET web application that displays a custom greeting message including the current server time and logs each request.This guide specify how to create resources in azure. The deployment guide below explains how to run the application locally and deploy it to both Windows and Linux environments on Azure.
## Prerequisites
Before you begin, ensure you have the following:
- An Azure Account
- Azure CLI installed 
- Arm tools installed
- Visual Studio Code
### Running the Application Locally

To run the application locally, follow these steps:

1. Clone this repository to your local machine.
2. Open the solution file (HelloWorldApp.sln) in Visual Studio.
3. Build the solution and run the project.
4. Access the application in your web browser at http://localhost:<port>.

### Creating Resources:
1. If you haven't already, download and install Visual Studio Code from the official website: [Download Visual Studio Code](https://code.visualstudio.com/download).
2. Install Azure CLI on your machine. You can find installation instructions for various operating systems here: [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
3. Open Visual Studio Code, go to the Extensions view (Ctrl+Shift+X), and search for "Azure Resource Manager Tools." Install this extension to work with ARM templates directly in VS Code.
4. Open Visual Studio Code and create a new folder for your ARM template project.Inside the folder, create a new file named azuredeploy.json (the main ARM template file).
5. Write your ARM template in the azuredeploy.json file. Define resources like Virtual Machines, Load Balancers, Public IPs, etc., as needed for your application deployment.
6. Open azure portal.
    - create resource group in azure portal specifying subscription,resource group name,location.
    - select deploy custom template and navigate to load file and upload arm templates .Click on review and create.
- Deployment Instructions for Azure (Windows and Linux)
 ### Windows Deployment
1. Manually create a new Azure Virtual Machine using the arm template.
2. Configure the VM settings, such as resource group, VM name, region, VM size, administrator account, and networking options (public IP, inbound port rules for HTTP/HTTPS).
3. Once the VM is deployed, go to the Virtual Machines section in the Azure Portal.
   - Select your VM and click on "Connect" to get connection details (RDP for Windows).
   - Use Remote Desktop Protocol (RDP) to connect to the VM using the provided credentials(virtual machine password).
4. After connecting to the VM, open Server Manager.
   - In Server Manager, click on "Add roles and features."
   - Follow the wizard to install the Web Server (IIS) role.
   - Once IIS is installed, you can deploy your web application to the appropriate directory
5. Copy your web application files to the directory where IIS is serving content. Ensure that the necessary permissions are set for the web application files and directories.
6. Open a web browser on your local machine.Enter the public IP address or DNS name of your Azure VM in the browser's address bar.
### Linux Deployment
1. Manually create one or more Linux Virtual Machine using arm template.
2. SSH into your Linux VM using a tool like command prompt.
   ``` bash
   ssh username@hostname
   ```
3. Install any dependencies required for your application.
     ``` bash
     wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    sudo dpkg -i packages-microsoft-prod.deb
    sudo apt-get update
    sudo apt-get install -y apt-transport-https
    sudo apt-get update
    sudo apt-get install -y dotnet-sdk-8.0
    ```
4. Upload your application files to the VM or clone your application repository.
    ``` bash
    git clone https://<your-token>@github.com/username/repo.git
    ```
    ``` bash
    scp /path/to/local/file <username>@<vm-ip>:/path/on/remote/vm
    ```
5. Create load balancer manually using arm template.Configure basic settings.Once the load balancer is set up, you can test it by accessing your application through the load balancer's public IP or DNS name.
