# Ping App ARM Template 
This repo contains the ARM Template for all the resources required for the PingConsole or .NET Core App. It creates an Event Hub, KeyVault, Storage Account, Log Analytics Workspace, Logic App which pulls all the ping data from event hub into a log analytics workspace. This demo shows that you can use the Azure Deploy Button without a custom Azure Resource Manager template (azuredeploy.json).

# Deployment Steps
<b>Step 1:</b> Click on the <b>'Deploy to Azure'</b> button below </br>

<a href="https://azuredeploy.net/" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

<b>Step 2:</b> Fill template form as shown below, click <b>'Next' </b>button </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/1%20new.png">
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
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/6.5%20new.png">
<b>Step 9:</b> Fill out the Workspace ID and Primary key as shown below and click on <b>Save</b> button </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/7.5.png">
<b>Step 10:</b> Next You need to replace the secrets in KeyVault with EventHubConnection string and also copy the name of the eventhub instance.</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/8.png">
<b>Step 11:</b>  Click on the EventHub and Copy it's connection string to a seperate file. Also make note of the event hub name instance as shown below </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/8.5.png">
Navigate to and Copy the event hub name as shown below</br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/9.png">
<b>Step 12:</b> Blob Storage Primary Key is the second keyvault secret that we will retrieve as shown below. Open the Storage Account annd copy it's access key value and container name as show below   </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/10.png">
<b>Step 13:</b> Navigate to the Access Keys for the Storage account and copy the Key Value shown below onto a seperate file </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/11.png">
<b>Step 14:</b> Then Navigate to the Containers tab in the same storage account and copy the name of the container onto a seperate file as shown below   </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/12.png">
<b>Step 15:</b> Lastly Click on the Key vault where all the information with regards to the secrets collected above will be pasted as shown below. First Copy the key vault's DNS name as show in the next step </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/13.png">
<b>Step 16:</b> Copy the key vault's DNS name as shown below </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/14.png">
<b>Step 16:</b>  </br>
<img src="https://komalsandboxdiag.blob.core.windows.net/pingarmtemplatereadmefiles/14.png">
<b>Your system is ready to be used! </b>

 

Click on the Key vault and Navigate it to it's Overview section to copy the DNS name for the keyvault and then to navigate to it's Secrets section to replace the values with the information copied in the above steps