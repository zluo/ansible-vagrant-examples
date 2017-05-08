# Ansible Notes

## Why Ansible
* Underneath Ansible is just SSH.
## Why not just use Bash scripts? 
* Ansible has an edge over Bash scripts because of its simplicity.
* Ansible just uses a list of tasks to run in YAML2 format. 
* Ansible also comes with idempotency out of the box. 
> That means you can run the same operation numerous times, and the output will remain consistent (i.e. it won't do something twice unless you ask it to). You can write Bash scripts this way, but it requires quite a bit more overhead.

## Others
* Ansible write with python 
* Ansible works only in linux

## Setup Develop Environment

See [Installation Document](https://jira.vasco.com/confluence/display/DEV/Setting+up+Development+Environment)

* ### Install virtualbox
   https://www.virtualbox.org/wiki/Downloads
* ### Install Vagrant
    https://www.vagrantup.com/downloads.html
* ### Install Ansible
    ```
    sudo easy_install pip

    sudo pip install ansible==2.1.1
    ```
#### Alternative Install ansible from source code (For windows cygwin)

    ```
    cd /opt
    git clone https://github.com/ansible/ansible
    ```
* ### Install Vagrant add-ons
```
vagrant plugin install vagrant-triggers
vagrant plugin install vagrant-host-shell
vagrant plugin install vai
```
* ###  Getting Deployment Scripts
   ```
   git clone git@git.silanis.com:auto/common.deployment.scripts.git
   ```
* ### Copy manifest.yml and evm-manifest.yml to common.deployment.scripts.git
```
http://binary-repo.silanis.com/repositories/tags/esignlive/V11.3.0/manifest.yml
http://binary-repo.silanis.com/repositories/tags/evm/EVM-1.0.15/evm-manifest.yml
```

### Ansible Configuration

In ~/.bashrc, add below lines
```
# Ansible settings
ANSIBLE=/opt/ansible
export PATH=$ANSIBLE/bin:$PATH
export PYTHONPATH=$ANSIBLE/lib
export ANSIBLE_LIBRARY=$ANSIBLE/library
export ANSIBLE_CONFIG=/cygdrive/c/src/dev/common.deployment.scripts/ansible-pipeline.cfg
export INVENTORY_TEMPLATE="minimal-evm"
```

## Run ansible Script
* Clean up Vagrant and Install esl
```
   ./cleanupLocalEnvironment.sh
```
* Install evm
```
  ./dev-ansible-playbook.sh playbooks/evm_initial_install.yml --extra-vars="@evm-manifest.yml"
```
* Update Platform
```
  ./dev-ansible-playbook.sh playbooks/evm_platform_update.yml --extra-vars="@evm-manifest.yml"
```
## An ansible example

```
    ---
    - hosts: webservers
      remote_user: root
      tasks:
      - name: ensure apache is at the latest version
        yum: name=httpd state=latest
      - name: write the apache config file
        template: src=/srv/httpd.j2 dest=/etc/httpd.conf
      - name: restart apache
        service: name=httpd state=restarted
```
## Ansible Terms

  * [Playbook](http://docs.ansible.com/ansible/playbooks.html)
    > playbook is an ansible term for scripts. 


  * [Roles](http://docs.ansible.com/ansible/playbooks_roles.html)
   
    > resuseable task

  * [YML Syntax](http://docs.ansible.com/ansible/YAMLSyntax.html)  
  
    > an human readable format of json or xml

  * [Inventory](http://docs.ansible.com/ansible/intro_inventory.html)  

    > environment configurations

  * [Template](http://docs.ansible.com/ansible/playbooks_templating.html)  
  
    > Ansible use Jinja2(python template engine) templating to enable dynamic expressions and access to variables

  * [Modules](http://docs.ansible.com/ansible/modules.html)  

    > Ansible commands

  * [Variables](http://docs.ansible.com/ansible/playbooks_variables.html)

    > variables can be defined and overwirte in different layers



## Ansible Structure
```

common.deployment.scripts
|
|--inventories
|  |--vagrant
|  |--sandbox
|  |--production
|
|--playbooks
|  |--group_vars
|  |   |--evm_servers.yml
|  |   |--vault_servers.yml
|  |--includes
|  |evm_initial_install.yml
|  |evm
|
|--roles
   |--evm
   |--vault

```

## Vagrant Notes

  vagrant is used for create vm. 

  ## vagrant commands.
  
  - init

   ```
   vagrant init boxcutter/centos67 
   ```

  - start vm

   ```
   vagrant up 
   ``` 

  - ssh

   ```
   vagrant ssh 

   ssh vagrant@<hostname> password: vagrant
   ``` 

  - save and restore vm

   ```
   vagrant snapshot save esl

   vagrant snapshot restore esl

   ``` 
## Resources

0. [Setting up Development Environment](https://jira.vasco.com/confluence/pages/viewpage.action?pageId=2393441)

1. [Ansible and Vagrant Quickstart Tutorial](https://jira.vasco.com/confluence/pages/viewpage.action?pageId=2393441)

2. Book [Ansible Up and Running](https://jira.vasco.com/confluence/download/attachments/2392392/Ansible_Up_and_Running.pdf?version=1&modificationDate=1445007305543&api=v2)

3. [Automated Deployment Scripts](http://docs.ansible.com/ansible/playbooks_variables.html)

4. [Design and Architecture](https//jira.vasco.com/confluence/pages/viewpage.action?pageId=4849700)



