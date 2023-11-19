# Creating a Dev/Test Workspace in Azure via Terraform

In line with the teaching from Dereck Morgan's course available here: https://courses.morethancertified.com/p/rfp-terraform-azure, this project aims to help you navigate the basics of Terraform. 

You'll be using Visual Studio Code on any platform (Windows, Mac, or Linux!) to set up Azure resources and an Azure Virtual Machine (VM). The VM allows for SSH access, creating a redeployable workspace that's ideal for any of your future projects!

I've taken the liberty of modifying some of the supplied scripts to further tailor it according to my requirements. I've added additional variables such as Azure's location, source IP, and key file location to enhance the reusability of the script.

# Testing out AADSSHLogin

The goal of this optional task was to implement Azure Active Directory (AAD) login functionality on an Azure Linux VM. Building upon this Azure Terraform project, the following steps were necessary to facilitate logging into the Linux VM created via Terraform:

## 1. Enable a System-Assigned Managed Identity on the Azure Linux VM

This step involves activating a system-assigned identity for the Azure Linux VM, which grants the VM an Azure AD identity for accessing other Azure services.

## 2. Install the AADSSHLogin Extension

The installation of the AADSSHLogin extension is done through the 'Extensions and Applications' feature within Azure. This extension is crucial for enabling AAD authentication on the VM.

## 3. Assign Roles in Access Control (IAM)

Assign the "Virtual Machine Administrator Login" role to your Azure AD account to grant sudo privileges on the Azure Linux VM. Alternatively, if sudo rights are not required, the "Virtual Machine User Login" role can be assigned.

Following these configurations, you can connect to the VM using the Azure CLI with the command:

```
az ssh vm --name "VM-Name" --resource-group "Resource-Group"

```

The following can be used to confirm that sudo right has been assigned to your Azure AD Account 

```
sudo -l -U username

```

# Next Steps

To implement the above as part of the overall Terraform script