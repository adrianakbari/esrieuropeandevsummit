# Automate GIS deployment
the repo for automating your GIS infrastructure. Esri European Dev Conference 2022

## Infrastructure Provisioning
Using Terraform. Can be used in multiple clouds and on-prem.  
Other options: Cloud native tools such as ARM in Azure.

## Application Provisioning
Using Ansible. Can be used on multiple clouds and on-prem.  
Other options: Cloud native tools such as DSC in Azure, Command Line tools (Powershell, Bash, CLI), Python.

## Architecture
A HA GIS setting with 3 tiers. A web tier, A GIS tier and a DB tier. Each tier has a replicated env for HA. 
<insert architecture pic>

## Considerations
- this implementation is NOT secured. It suits the dev/test workloads. For production apply security best practices. 
