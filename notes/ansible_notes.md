# Ansible Notes

## Why Ansible
* Underneath Ansible is just SSH.
## Why not just use Bash scripts? 
* Ansible has an edge over Bash scripts because of its simplicity.
* Ansible just uses a list of tasks to run in YAML2 format. 
* Ansible also comes with idempotency out of the box. 
> That means you can run the same operation numerous times, and the output will remain consistent (i.e. it won't do something twice unless you ask it to). You can write Bash scripts this way, but it requires quite a bit more overhead.

## An ansible example

```
    ---
    - hosts: webservers
      vars:
        http_port: 80
        max_clients: 200
      remote_user: root
      tasks:
      - name: ensure apache is at the latest version
        yum: name=httpd state=latest
      - name: write the apache config file
        template: src=/srv/httpd.j2 dest=/etc/httpd.conf
      - name: restart apache
        service: name=httpd state=restarted
```
## ansible terms

  * [Playbook](http://docs.ansible.com/ansible/playbooks.html)
> playbook


  * [Roles](http://docs.ansible.com/ansible/playbooks_roles.html)
  * [YML Syntax](http://docs.ansible.com/ansible/YAMLSyntax.html)  
  * [Inventory](http://docs.ansible.com/ansible/intro_inventory.html)  
  * [Template](http://docs.ansible.com/ansible/playbooks_templating.html)  
  * [Modules](http://docs.ansible.com/ansible/playbooks_templating.html)  



Vagrant Notes
=====================


Resources
---------------------
1. Installation





3. [Ansible Variables](http://docs.ansible.com/ansible/playbooks_variables.html)


4. [Design and Architecture](https//jira.vasco.com/confluence/pages/viewpage.action?pageId=4849700)



