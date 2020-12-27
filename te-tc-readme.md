# Terraform Enterprise / Terraform Cloud

## Overview
**Terraform Cloud** - It is available as a hosted service. It manages Terraform runs in a consistent and reliable environment, and includes easy access to shared state and secret data, access controls for approving changes to infrastructure, a private registry for sharing Terraform modules, detailed policy controls for governing the contents of Terraform configurations, and more.

**Terraform Enterprise**  - It offers enterprises a private instance of the Terraform Cloud application, with no resource limits and with additional enterprise-grade architectural features like audit logging and SAML single sign-on.

> *Before mid-2019, all distributions of Terraform Cloud used to be called Terraform Enterprise; the self-hosted distribution was called Private Terraform Enterprise (PTFE).*

## Components 
![Alt text](/images/terraform-architecture.jpg)

* **Private Module Registry** - It provides plugins to manage any infrastructure API, pre-made modules to quickly configure common infrastructure components, and examples of how to write quality Terraform code. It is a resource for discovering integrations (providers) and configuration packages (modules) for use with Terraform developed by HashiCorp, third-party vendors, and  Terraform community. Refer [Terraform Registry](https://www.terraform.io/docs/registry/index.html)
* **Version Control System (VCS)** - Terraform Cloud is designed to work directly with version control system (VCS) provider. Terraform Cloud automatically retrieves configuration content from the repository, and will also watch the repository for changes.
* **Remote Operation / Remote Terraform execution** - Terraform Cloud runs Terraform on disposable virtual machines in its own cloud infrastructure. Terraform Cloud performs Terraform runs in single-use Linux virtual machines, running on an x86_64 architecture. The operating system and other software installed on the worker VMs is an internal implementation detail of Terraform Cloud. It is not part of a stable public interface, and is subject to change at any time. Before Terraform is executed, the worker VM's shell environment is populated with environment variables from the workspace, the selected version of Terraform is installed, and the run's Terraform configuration version is made available. Refer [Terraform Cloud Run](https://www.terraform.io/docs/cloud/run/run-environment.html)
* **Workspaces** - Terraform Cloud organizes infrastructure with workspaces instead of directories. Each workspace contains everything necessary to manage a given collection of infrastructure, and Terraform uses that content whenever it executes in the context of that workspace.
* **Access Control & Governance**
    * Team-Based Permissions System - With Terraform Cloud's team management, you can define groups of users that match your organization's real-world teams and assign them only the permissions they need. When combined with the access controls your VCS provider already offers for code, workspace permissions are an effective way to follow the principle of least privilege.
    * Sentinel Policies - Terraform Cloud embeds the Sentinel policy-as-code framework, which lets you define and enforce granular policies for how your organization provisions infrastructure. You can limit the size of compute VMs, confine major updates to defined maintenance windows, and much more.

## References
* [Terraform cloud overview](https://www.terraform.io/docs/cloud/overview.html)
* [Terraform cloud agents](https://www.terraform.io/docs/cloud/agents/index.html)
* [Terraform Cloud Run](https://www.terraform.io/docs/cloud/run/run-environment.html)