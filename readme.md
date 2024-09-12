# Deploying Static Website using Load Balancer by ARM Template

## Project Overview

**Art Showcase Hub** An Art Showcase hub website is a platform for artists to display their work, allowing users to explore and interact with curated art galleries. It features artist profiles, virtual exhibitions, and search filters for different art forms, fostering community engagement and exposure for artists. 

This project demonstrates the deployment of **Art Showcase Hub** using Azure's ARM templates and load balancing across two Virtual Machines (VMs) in different availability zones for high availability and scalability.

## Problem Statement

Artists often struggle to find platforms that offer visibility and engagement for their work, while art enthusiasts lack centralized spaces to explore diverse collections. An art showcase hub aims to bridge this gap, providing a virtual gallery that connects artists with a broader audience.

## Project Goals

- Deploy the **Art Showcase Hub** website on Azure using ARM templates.
- Set up a **Virtual Network (VNet)** with two **Subnets** and a **Network Security Group (NSG)**.
- Use a **Load Balancer** to distribute traffic between two VMs located in different availability zones.
- Host the static website on these VMs and make it accessible via the load balancer's frontend IP.

## Technologies and Azure Services Used

1. **Azure CLI**: Used to create the resource group and Virtual Network.
2. **ARM Templates**: Automated the creation of VNet, subnets, and NSG.
3. **Azure Virtual Machines (VMs)**: Hosted the Closet.AI website.
4. **Azure Load Balancer**: Distributed the traffic between two VMs to ensure high availability.
5. **Nginx**: Used as a web server on both VMs to serve the static content.
6. **Git**: Cloned the website from GitHub onto the VMs using a custom script.
7. **Custom Script Extension**: Used to automatically configure the VMs upon deployment.

## Project Steps

### 1. Website Development
- **Art Showcase Hub**: A static website allowing users to explore and interact with curated art galleries.

### 2. Deploying the Website on GitHub
- The frontend of **Art Showcase Hub** was uploaded to a public GitHub repository: [Frontend-Art ShowCAse Hub](https://github.com/Alekhyagit99/Staticweb.git).

### 3. Azure Deployment Using ARM Templates
- **Resource Group**: Created using Azure CLI to hold all the resources.
- **Virtual Network (VNet)**: Set up using an ARM template, which included two subnets for distributing the VMs.
- **Network Security Group (NSG)**: Applied inbound rules to allow traffic on ports 22 (SSH) and 80 (HTTP).
  
### 4. Virtual Machines Setup
- **VM 1**: Created in Availability Zone 1 using Azure Portal. Configured with:
  - Custom Script Extension to clone the website from GitHub.
  - Networking settings to connect to the VNet and assigned Subnet.
  
  Custom Script:
  ```bash
  #!/bin/bash
  sudo apt update
  sudo apt install nginx git -y
  cd /tmp && git clone https://github.com/Alekhyagit99/Staticweb.git mysitee
  sudo rm -rf /var/www/html/index.nginx-debian.html
  sudo cp -r /tmp/mysitee/* /var/www/html/
  ```

- **VM 2**: Created in Availability Zone 2 with the same configuration as VM 1.

### 5. Load Balancer Configuration
- **Load Balancer**: Configured to distribute traffic between VM 1 and VM 2.
  - **Frontend IP Configuration**: Assigned a new frontend IP for external access.
  - **Backend Pool**: Added both VMs to the backend pool for traffic distribution.
  - **Load Balancing Rule**: Defined to balance HTTP traffic (port 80) across the VMs.
  - **Health Probe**: Set up to monitor the health of the VMs and ensure traffic is routed only to healthy VMs.

### 6. Testing and Accessing the Website
- After the load balancer deployment, the website became accessible via the frontend IP of the load balancer. Users can interact with **Art ShowCase Hub** to generate galleries from their art uploads.

## How to Use Art ShowCase Hub

1. Upload your art images.
2. The system will generate multiple images of what type of art you required.
3. Explore the generated pictures and get inspired to pick your favorite ensemble.

## Azure Services and Tools Used

- **Azure CLI**: Resource group creation and management.
- **Azure Resource Manager (ARM) Templates**: Infrastructure-as-Code to deploy resources.
- **Virtual Network (VNet)**: Networking and subnetting.
- **Network Security Group (NSG)**: Security rules for VM access.
- **Azure Virtual Machines**: Hosting the website on multiple VMs.
- **Azure Load Balancer**: Load balancing between VMs.
- **Nginx**: Web server for hosting static content.
- **Git**: Version control and cloning the website onto VMs.
- **Custom Script Extension**: Automated configuration of VMs.

## Live Website and Resources

- **Website Link**: [Art ShowCase Hub](https://github.com/Alekhyagit99/Staticweb.git)
- **Project Video**: [Project Video](https://drive.google.com/file/d/1KoVZAeFeHnawi3tuxac35bfjGKmSIu-w/view?usp=sharing)
- **Screenshots**:
  **Created Resource Group Screenshot**
  - ![ResourceGroup Screenshot](./Project/az_login.png)

  **VNet Subnets RSG ARM Template Output**
  - ![Deployment Screenshot](./Project/deployment.png)

   **Deployed VM 1 Screenshot**
  - ![VM1 Screenshot](./Project/Vm-1.png)

  **Deployed VM 2 Screenshot**
  - ![VM2 Screenshot](./Project/Vm-2.png)

  **Deployed LoadBalancer Screenshot**
  - ![Loadbalancer Screenshot](./Project/Loadbalancer.png)

  **Website Home Page Screenshot**
  - ![Website Screenshot](./Project/website.png)

## Conclusion

This project showcases the end-to-end process of deploying a static website using Azure's ARM templates and load balancing capabilities. By distributing traffic between two VMs in different availability zones, we ensure high availability and scalability for the **Closet.AI** platform. The integration of Azure's powerful tools and services simplified the deployment and configuration process.

## Author

**Ch Alekhya**
**Salma Saher**
Deployed in group as part of learning Azure's cloud infrastructure.
