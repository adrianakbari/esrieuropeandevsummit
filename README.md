# Automate GIS deployment
the repo for automating your GIS infrastructure. Esri European Dev Conference 2022

## Infrastructure Provisioning
For this demo a multi-tier architecture is deployed using Terraform. In case of interest please contact me on akbari.adrian@gmail.com

## Application Provisioning
For this demo Ansible is chosen to be automation tool. Ansible can run on any cloud proveder and on on-prem. it also run on windows and linux. Ansible offers more options in comparision to other tools.

## Architecture
A multi-tier architecture with 3 tiers: A web tier, A GIS tier and a Database tier. 

## Prerequisite
1. Check the prerequisite for ArcGIS Enterprise Implementation: https://enterprise.arcgis.com/en/system-requirements/latest/linux/arcgis-enterprise-overall-system-requirements.htm
2. At least a self-signed SAN certificate in .p12 or .pfx format. Place this certificate in roles > arcgistomcat > files
3. A sattelite server where you can download arcgis installation files. Or change ansible code to copy installation files from your local directory.
4. Place arcgis portal (.json) and arcgis server (.prvc) files in ansible/files
4. adjust parameters in ansible.cfg, inventory_test, arcgis.yml, arcgistomcat.service, tomcat server.xml, createportal.properties, server role > script-site.py

## Installation
Install ansible on a management node: 
sudo add-apt-repository --yes --update ppa:ansible/ansible

## Run Ansible
1. Make sure you have arcgis site pass and arcgis portal pass in Ansible vault. 
2. copy ansible files to your management node. 
3. cd to /ansible directory
3. ansible-playbook -i inventory_test arcgis.yml --ask-pass --ask-vault-pass


## Considerations
- this implementation is NOT secured. It suits the dev/test workloads. For production apply security best practices. 
- in the vault you need to enter 2 values: 
1. siteadminpassword
2. portaladminpassword
- To run the script for Staging or Prod environemnts:
1. check out the code that is commented in each task. uncomment the part that includes when: versie == "{version}"
2. Create another inventory file named inventory_{version}
3. run ansible: ansible-playbook -i inventory_{version} arcgis.yml --ask-pass --ask-vault-pass
- Tomcat is configured wtih ports 80 and 443. In case you need to use other ports:
1. change the ports in server.xml
2. If the ports < 1024, see tomcat docs for ports below 1024 on the server. One way is to use Authbind. Because Ansible doesnt support running shell command with Authbind, you  need  to modify the startup.sh. An example is provided in this repo where the deafult exec line is modified to:
exec authbind --deep  "$PRGDIR"/"$EXECUTABLE" start "$@"

## Contact
I love to hear what you think about my article or hear your questions.
For any questions contact me on akbari.adrian@gmail.com