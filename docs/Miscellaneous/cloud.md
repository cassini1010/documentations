# Azure Cloud

## Infrastructure as a service (IaaS)

Infrastructure as a service refers to providing complete aaccess to the servers OS. Typically, laaS provides hardware, storage, servers and data center space or network components; it may also include software.



## Platform as a service (PaaS)

In Platform as a Service, one does not get access to the whole Operating System. Rather access is given at a Dashboard level, where a user uploads the data, and the rest is taken care by the cloud provider.



## Software as a service (SaaS)

Software as a Service refers to the practice of directly providing the software to the customer, without making any server or dashboard available to them. Ex. Google Drive



## Azure core architecture

Azure has 4 agents that can interact with the Azure resources

- Azure Portal

- Azure Powershell

- Azure CLI

- REST Client

All these agents are capable of interactivng with the Azure Resource Manager, which inturn connects the agent to the requires service.



## Azure services

Azure provides services in below domains

- Compute

- Networks

- File Storage

- Database

- Identity

- Management

- AI + ML

### Compute

#### Virtual Machine (IaaS)

Its a server/ fresh computer whcih has an OS just installed and no other software installed. Its like a Bare miinnimum computer. Azure gives remote connection access to it. If windows remote desktop can be used to connect, if linux SSH.

#### Function App (PaaS)

One do not get the access to the operating system. Its like a developer gets a dashboard where he can upload a code that needs to be run as a baackend service in the cloud which accepts images form user. Only the code is delployed as a service and developer is not given the access to the OS.

> Website can not be deployed here as this is a system wehre it accespts input and gives outptu. 

#### App Service (PaaS)

Launch or Deploy website. User gets dashboard where upload website files/ code. No access to OS here too.

#### Azure Kubernetet Service

Azure Kubernetes Service (AKS) is a managed container orchestration service, based on the open source Kubernetes system, which is available on the Microsoft Azure public  cloud.

### Networking

#### Virtual Network

If one buys two or there servers and wants those server to talk to each other, it can be placed in a virtual network. This will emulate the scenario where all the servers are in a same network. If Virtual network is not bought, then the servers have to rely on internet to talk to eaach other by opening a port between each other. (no so secure).

Other Networking services:

- Load Balancer

- Application gateway

- DNS Zones

- Content Delivery Network (CDN)



### Database

- Data Lake Analytics

- Event Hubs

- Data Factory

- CosmosDB

- SQL Database




