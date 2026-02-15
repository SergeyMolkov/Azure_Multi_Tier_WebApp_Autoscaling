These steps set up the basic Azure environment and GitHub repository for the project. All steps use Azure CLI (no Terraform or similar tools). Assume you have an Azure account; if not, sign up for a free one at [portal.azure.com](https://portal.azure.com).

## Step 1: Install Azure CLI and Login
- Download and install Azure CLI from [https://docs.microsoft.com/en-us/cli/azure/install-azure-cli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
- Open a terminal (CMD/PowerShell on Windows, Bash on Linux/Mac).
- Login: `az login` (this opens a browser for authentication).
- Show your subscription ID: `az account list`
- Set your subscription: `az account set --subscription <your-subscription-id>`.

## Step 2: Create Resource Group
- A resource group to hold all Azure resources.  
- Command: `az group create --name "Sergey-MultiTier-App-RG" --location "EastUS"`
(Replace "Sergey-MultiTier-App-RG" with the name of your resource group.)

## Step 3: Create GitHub Repository
- Go to [github.com](https://github.com) and create a new repository named "Multi-Tier-Web-App-Auto-Scaling".
- Clone it locally: `git clone https://github.com/SergeyMolkov/Cloud_Infrastructure/Multi_Tier_WebApp-With_Autoscaling.git`.
(Replace "SergeyMolkov/Cloud_Infrastructure/Multi_Tier_WebApp-With_Autoscaling.git" with the name of your path and nmae of the file.)
- Create folders: `mkdir AKS frontend backend scripts docs`.
- Create `README.md` with this content:
"This is a multi-tier web app on Azure with auto-scaling."
