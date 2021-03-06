# Release Note for OMS Linux Agent 

##### OMS Agent 1.2.0-75 (9/27/16) - Docker Provider 1.0.0-12 
- Added Docker 1.12 and Ubuntu 16.04 TLS support

##### OMS Agent 1.2.0-148 (11/9/16) - Docker Provider 1.0.0-16
- Support ACS DC/OS and Mesosphere DC/OS
    -   Container Solution is available on Mesosphere Universe. This solution will only monitor the Docker Container. Customer can select and run the OMS Agent for Linux on each VMs in DC/OS. You will require OMS WorkspaceID and Primary Key beforehand to install the OMS Agent for Linux.To support ACS DC/OS, you must use the OMS Agent for Linux in the Mesosphere DC/OS Universe.  
        -   For more information about ACS DC/OS, please go [here.](https://azure.microsoft.com/en-us/documentation/services/container-service/)
-   Simplified installation 
	- Previously, Container Solution required universal setting for the docker log. This is no longer necessary. Follow the instruction on the github or website. 
-  Enhanced log collecton. 
	-  Customers can now run docker log directly on the container itself and will also collect the logs on OMS as well. 
- Bug fix
	- Container Hostname provided container SHA ID information instead of the hostname.

##### OMS Agent 1.3.2-15 (03/31/17) - Docker Provider 1.0.0-22
- Updated the container image to Ubuntu 16.04 LTS
- Graceful shutdown of OMS process
- Decrease containerized OMS Linux Akgent size for lighter agent experience
- Increase buffer size
- Capture host syslog
- Bug fix
	- segfault error due to libcontainer.so. 

##### OMS Agent 1.3.4-127 (05/10/17) - Docker Provider 1.0.0-23
- Added Fairfax workspace support to containerized OMS Agent for Linux
- Added new dataset which provides container node information such as Node Operating System, Docker version, Orchestration type, volume, and network.
	Type=ContainerNodeInventory
- Bug fix
        - segfault error 

##### OMS Agent 1.3.4-127 (05/24/17) - Docker Provider 1.0.0-24
- Bug fix
	- Memory Leak
	- Improved Container Log collection
	- segfault error

##### OMS Agent 1.4.0-12 (06/30/17) - Docker Provider 1.0.0-25
- Added support for Docker Swarm
- Added support for journald and json log-drivers
- Added support for secrets (Docker Swarm and Kubernetes)
- Added livenessProbe for deploying container

##### OMS Agent 1.4.0-45 (08/23/17) - Docker Provider 1.0.0-27
- Added Kubernetes events
- Added Kubernetes cluster awareness with hierarchy inventory and search filters for hierarchy like namespace etc.
- Captures pod label and provides search filters for them
- Captures container process information ( docker container top ) 
- Added container node inventory


##### OMS Agent 1.4.3-174 (01/23/18) - Docker Provider 1.0.0-30
- Fixed exceptopn handling in kube api
- Dedup kube events based on event id and count instead of event ID
- Enhanced container log collection mechanism for better scalability
- Enhanced monitoring data buffering on agent by providing isolation to buffer based on collected data type. This eliminated the deadlock situation on buffer causing the data to not be sent to Log Analytics.  


#### Due to the backend changes, for container monitoring with OMS Agent for Linux and it is a fresh install, you will need to run this workaround. 

If this a fresh install, install the agent and onboard later by doing the following steps: 
1. Download the OMS Agent for Linux. Install the OMS Agent for Linux. 

	```sudo ./omsagent*.sh --install``` 

2. Onboard your OMS workspace.

	```sudo /opt/microsoft/omsagent/bin/omsadmin.sh -w <wsid> -s <key>``` 

If you have already installed and onboarded, re-onboard by doing the following steps:
1. Remove all the onboarded OMS workspace.  

	```sudo /opt/microsoft/omsagent/bin/omsadmin.sh -X```

2. Re-onboard your OMS workspace. 

	```sudo /opt/microsoft/omsagent/bin/omsadmin.sh -w <wsid> -s <key>```
