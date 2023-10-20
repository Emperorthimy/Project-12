## **Documentation for Project 12**

### Refactoring our Ansible for better maintainablity and extensibility

### Creating a new directory for jenkins to save artifacts to reduce complexity && Permission changed for jenkins to save artifacts in the new directory

`sudo mkdir /home/ubuntu/ansible-config-artifact`

`chmod -R 0777 /home/ubuntu/ansible-config-artifact`

![ansible-config-artifacts-directory-created](./Images/Ansible-config-dir.png)

### Copy Artifact plugin Installed on Jenkins

![copy-artifact-plugin-installed](./Images/copy-artifacts-plugin.png)

### save_artifact freestyle project created on Jenkins

![Save-artifact-freestyle-project-created](./Images/save-artifacts-step1.png)

### Configuring Number of Builds to Keep and which Project to Build Artifacts from

![Build-Config-Settings](./Images/save-artifacts-step2.png)

### Configuring a Build Step to copy artifact from project11ansible and Specifying the target directory which is ansible-config-artifact

![configuring-build-step](./Images/save-artifacts-step3.png)

### Successfully-configured
![copy-artifact-successfully-configured](./Images/save-artifact-step4.png)

### Testing our setup by making changes to readme file
![tested-with-changes-made-to-readme-file](./Images/save-artifacts-step5.png)

### Details of save_artifact first build in Console Output
![console-output](./Images/Save-artifacts-step6.png)
![console-output](./Images/Save-artifacts-step7.png)

### Our Jenkins Pipeline Looking neat, and Less Complex
![Less-Complex-jenkins-pipeline](./Images/inventory&&galaxy-init.png)

## Refactoring Ansible by Importing Playbooks for different tasks

### This is achieved by having a parent playbook named site.yml which will be used as a refference point for other playbooks (Child Playbooks)

### Running our Parent playbook site.yml against our dev environment for the removal(deleting) of wireshark, making use of the built-in ansible import-playbook Module and refferencing the child playbook static-assignment/common-del.yml

` ---`
` - hosts: all `
` - import_playbook: ../static-assignments/ ` `common-del.yml `

` ansible-playbook -i /home/ubuntu/ansible-config-artifact/inventory/dev.yml /home/ubuntu/ansible-config-artifact/playbooks/site.yml `
![running-ansible-playbook-import-against-dev-environment](./Images/running_playbook-to-delete-wireshark.png)

### Confirmation of removal(deleting) wireshark on all our target servers

![wireshark-removal-confirmation-on-all-servers](./Images/wireshark-deletion-confirmation.png)

## Configuring UAT webserver with a role webserver

### Role structure of our webserver Created with Ansible Galaxy

![role-structure-created-with-ansible-galaxy](./Images/role-structure.png)

## Refferencing our webserver role inside static-assignments folder which is a container for our child playbooks

### Creating a separate assignment for our webserver role in static-assignments folder

`touch uat-webservers.yml`

![refferencing-roles-in-child-playbook-container-static-assignments](./Images/uat-webserver.png)

### Importing our roles playbook inside our parent playbook site.yml using the built-in ansible import playbook

`- hosts: uat-webservers `
` - import_playbook: ../static-assignments/uat-webservers.yml `

![importing-uat-webservers-playbook](./Images/import-playbook-to-site.yml.png)

### Running our playbook against the UAT inventory for Deploying our tooling Website on the UAT servers

`ansible-playbook -i inventory/uat.yml playbooks/site`

![ansible-playbook result for UAT webservers](./Images/deploying-tooling-on-webservers.png)

### Tooling website live on both of our UAT webservers

`http://3.15.212.16/index.php`

`http://54.211.141.19/index.php`

![ansible-playbook result for UAT webservers](./Images/tooling-website.png)
