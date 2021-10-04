# AzurePaaSAnywhere
Azure now has released the capability to run Azure Application Services to run anywhere which are Arc enabled. 

# STEPS TO RUN AZURE APPLICATION SERVICES ON YOUR LAPTOP OR OTHER HOME DEVICES

# Step 1 – Enable K8S on your laptop, and connect it to Azure using Arc

There are multiple ways on running Kubernetes locally on your laptop (miniKube, Kind etc), I have chosen the option of using Docker Desktop. If you have Docker desktop running, you can enable Kubernetes in the settings:

![DockerDesktop](/.images/DockerDesktopWelcomeScreen.png)

Now, using Windows terminal or Powershell if you can get to the correct cluster context and run the following commands to see everything is it should be.

![ClusterContext](.images/TerminalClusterContext.png)

I found this resource useful which takes you through how to connect your cluster to Azure Arc - Existing cluster | Azure Arc Jumpstart

To connect this docker-desktop to Azure Arc, create a resource group (or use an existing one) and then the command to connect.
```
az group create -n arccluster1345 -l westeurope

az connectedk8s connect --name arcpblaptop1506 --resource-group arccluster1506
```

![ClusterConnectCommand](.images/ArcConnectDockerDesktop.png)

Now that your laptop is connected to Azure Arc, you can see the following pods running in your laptop cluster 

![GetNodesAfterClusterConnect](.images/RunningPodsonDockerDesktop.png)

You can explore the resource group arccluster1345 in the portal where you can see an Azure Arc Cluster. 

![AzureArcClusterPortal](.images/PortalExploreArc.png)

# Step 2 – Install the App Service extension to your docker desktop cluster

Now that your laptop cluster is connected, you can install an App Service extension as shown here:

![InstallAppServiceExtenstion](.images/InstallAppServiceExtensions1.png)
![InstallAppServiceExtenstion2](.images/InstallAppServiceExtensions2.png)

You have a field to enter your static ip as shown below. I don’t have any static IP’s (there are service providers who can set up and manage static ip’s dedicated for you, which are not free as far as I know).
I have used my router’s public ip which you can find using whatismyip.com  (ipv4). However taking this approach will mean that, you need to do port forwarding on ports 80, 443 and 8081 as well as open the OS firewall to these 3 ports. Refer appendix to see more detail and screen shots from port forwarding. 

![InstallAppServiceExtenstion3](.images/InstallAppServiceExtensions3.png)

Defaulting on the Monitoring and Tags tabs will take you to the screen shown here. It presents you with a series of commands to push the extension to your laptop cluster. Copy the commands, and run one by one in sequence. Screen shots should provide you guidance. (Note that there are some steps to be taken after you run the first few commands, and before you run the create custom location command – so follow through the screen shots)

![InstallAppServiceExtenstion4](.images/InstallAppServiceExtensions4.png)

![InstallAppServiceExtenstion5](.images/InstallAppServiceExtensions5.png)


