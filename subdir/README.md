# Ping App ARM Template 
This repo contains the ARM Template for all the resources required for the PingConsole or .NET Core App. It creates an Event Hub, KeyVault, Storage Account, Log Analytics Workspace, and Logic App which pulls all the ping data from event hub into a log analytics workspace. This demo shows that you can use the Azure Deploy Button without a custom Azure Resource Manager template (azuredeploy.json).

# Deployment Steps
<b>Step 1:</b> Click on the <b>'Deploy to Azure'</b> button below </br>

<a href="https://azuredeploy.net/" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

<b>Step 2:</b> Fill template form as shown below, fill the KeyVault Name with only letters between 3-24 with no numbers or special characters, ObjectId is a GUID string obtained from Azure CLI in portal, in PowerShell mode of Azure CLI type 'Get-AzADUser -UserPrincipalName foo@domain.com' repalcing foo@domain.com with your own Azure Portal email and pasting the Object Id string in the form below as shown, click <b>'Next' </b>button </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/1%20new.png">
<b>Azure CLI</b> How to obtain <b>'ObjectId'</b> field value from Azure CLI</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/0.5.png">
<b>Step 3:</b> Click <b>'Next' </b> after looking at validation passed </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/2%20new.png">
<b>Step 4:</b> Wait for Deployment to go through when you see the form below; your resources are ready in Azure Portal </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/4%20new.png">
<b>Step 5:</b> Login to Azure portal to view the newly created resources </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/5new.png">
<b>Step 6:</b> For now the Log Analytics connector is in (preview) mode therefore you will need to fill out the connection info manually. </br> Click on advanced settings for the log analytics workspace and copy the Workspace ID and Primary key 
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/5.5.png">
Copy the Workspace ID and Primary key in a seperate file or notepad as you will need it for the next step
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/6%20new.png">
<b>Step 7:</b> Open up the API connection for Log Analytics workspace as shown below and paste the information copied in previous step </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/7new.png">
<b>Step 8:</b> Click on Edit API connection 
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/6.5%20new.png" height="42" width="42">
<b>Step 9:</b> Paste the Workspace ID and Primary key copied in the previous steps as shown below and click on <b>Save</b> button </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/7.5.png">
<b>Step 10:</b> Next You need to replace the secrets in KeyVault with EventHubConnection string and also copy the name of the eventhub instance. In addition make note of the event hub name instance as pointed below</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/8.png">
<b>Step 11:</b>  Click on the EventHub and copy it's Connection String to a seperate file, you will need this to be added as Key-Vault Secret value</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/8.5.png">
Navigate to and Copy the event hub name as shown below</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/9.png">
<b>Step 12:</b> Blob Storage Primary Key is the second keyvault secret that we will retrieve as shown below. Open the Storage Account annd copy it's access key value and container name as show below   </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/10.png">
<b>Step 13:</b> Navigate to the Access Keys for the Storage account and copy the Key Value shown below onto a seperate file </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/11.png">
<b>Step 14:</b> Then Navigate to the Containers tab in the same storage account and copy the name of the container onto a seperate file as shown below. This will be need in appsettings json file of the ping utility code </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/12.png">
<b>Step 15:</b> Click on the Key vault and Navigate it to it's Overview section to copy the DNS name for the keyvault. Make a note of the key vault's DNS name as shown below on to a seperate file. This will be needed in appsettings json file of the ping utility code and then to navigate to it's Secrets section to replace the values with the information copied in the above steps. Key vault will have all the information collected above to be stored in key vault in the form of secret's value as shown below.</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/13.png">
Save the key-vault's DNS name in a seperate file, it will be needed in appsettings json file of the ping utility code </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/14.png">
<b>Step 16:</b> Open the Key Vault tab called "Secrets" and click on the first secret value "blobStoragePrimaryKey" and click on "New Version" to store the new value copied in the previous steps.
When the form opens, paste the Blob Storage Primary Key in the value field as shown below </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/14.5.png" >
<b>Step 17:</b> When the Blob Storage Primary Key is pasted in the value field as shown below, click on the Create button</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/15.png" >
<b>Step 18:</b> Then repeat the same steps for replacing the Event Hub Connection string titled "eventhubconnString", click on the New Version button and paste the Event Hub Connection string saved from the previous step</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/16.png" >
<b>Step 19:</b> The following Steps pertain to the installation of the PingAsync Utility on your System.
You need to create a Linux VM or setup an existing Linux/Windows VM, on which your PingAsync utility Code will run. The following requires you to open an Azure CLI and run the following commands. The following is taken from a reference article here (https://docs.microsoft.com/en-us/azure/key-vault/tutorial-net-linux-virtual-machine) </br>
<b>
az vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
</b>
Once the Linux VM is setup the next steps will show you how to link the VM to the keyVault. 
 </br>

<b>Your system is ready to be used! </b>

 

