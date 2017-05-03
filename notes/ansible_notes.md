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

  * [Modules](http://docs.ansible.com/ansible/playbooks_templating.html)  

    > Ansible commands

  * [Variables](http://docs.ansible.com/ansible/playbooks_variables.html)

    > variables can be defined and overwirte in different layers

Vagrant Notes
=====================



Resources
---------------------
1. [Installation Ansible and Vagrant](

2. Book [Ansible Up and Running](https://jira.vasco.com/confluence/download/attachments/2392392/Ansible_Up_and_Running.pdf?version=1&modificationDate=1445007305543&api=v2)

3. [Ansible Variables](http://docs.ansible.com/ansible/playbooks_variables.html)

4. [Design and Architecture](https//jira.vasco.com/confluence/pages/viewpage.action?pageId=4849700)



