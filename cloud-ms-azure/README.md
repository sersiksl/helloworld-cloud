# Microsoft Azure

  - [Create an Account](#create-an-account)
  - [Choose a Terminal](#choose-a-terminal)
    - [Use a Web Based Terminal](#use-a-web-based-terminal)
    - [Use Your Own Computer’s Terminal](#use-your-own-computers-terminal)
  - [Tutorials](#tutorials)
  - [Cheat Sheet](#cheat-sheet)

## Create an Account

Link for everybody: https://azure.microsoft.com/en-us/free/

* $200 credit to explore any Azure service for 30 days
* 12 months of popular free services

Link for students: https://azure.microsoft.com/en-us/free/students/

* Get a $100 credit when you create your free Azure for Students account

**Some important facts:**

* You must provide credit card or bank details to set up a billing account to verify your identity, but you won't be charged during the free trial.

    ![Docker Components](cloud-ms-azure/images/ms-azure-logininfos.png)

* Possibility to schedule a live demo to see Azure in action
* Microsoft-Like Tour through the portal
* Many free services for 12 months or some even longer: https://azure.microsoft.com/en-us/free/free-account-faq/ - some examples:
    * 128 GB of Managed Disks as a combination of two 64 GB (P6) SSD storage
    * 5 GB of LRS File Storage with 2 million read, 2 million list, and 2 million other file operations
    * 1 million requests and 400,000 GBs of resource consumption with Azure Functions
    * First 5 users free with Azure DevOps
    * Free Azure Container service to cluster virtual machines
    * First 5 users free with Azure DevOps

## Choose a Terminal
You can choose either to use a web based terminal or install and run the required command line interfaces on your own computer’s terminal. There is no recommended terminal, you should use what you feel more comfortable with in a special situation. Below are both sets of instructions.

### Use a Web Based Terminal
Azure hosts Azure Cloud Shell, an interactive shell environment that you can use through your browser. Cloud Shell lets you use either bash or PowerShell to work with Azure services. You can use the Cloud Shell pre-installed commands to run the code in this article without having to install anything on your local environment.

To launch Azure Cloud Shell there are 2 Options:

1. Go to [https://shell.azure.com](https://shell.azure.com) or select the Launch Cloud Shell button to open Cloud Shell in your browser.

    ![Docker Components](cloud-ms-azure/images/ms-azure-cloud-shell.png)

2. Select the Cloud Shell button on the top-right menu bar in the [Azure portal](https://portal.azure.com/).

    ![Docker Components](cloud-ms-azure/images/ms-azure-cloud-shell-menu.png)

### Use Your Own Computer’s Terminal
You can also a local installation of the Azure CLI. If you'd like to use it locally, version 2.0.55 or later is recommended. Run az --version to find the version. If you need to install or upgrade, see [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).


## Tutorials
* Microsoft Azure Tutorial for Beginners (contains good overview of the Azure concepts): https://www.guru99.com/microsoft-azure-tutorial.html
* Microsoft Azure Collection of tutorials: https://docs.microsoft.com/en-us/learn/paths/azure-fundamentals/
* Quick Start for Containers: https://docs.microsoft.com/en-us/azure/container-instances/container-instances-quickstart


## Cheat Sheet
* [Cloud Shell](https://shell.azure.com) 
* [Container Registry](https://portal.azure.com/#create/Microsoft.ContainerRegistry)



