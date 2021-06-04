# Ansible-MultipleOS-LAMP

## Description:

A simple ansible role to setup LAMP server on muliple [Linux Distributions](https://en.wikipedia.org/wiki/List_of_Linux_distributions). This role can be use to setup LAMP on [Amazon Linux](https://aws.amazon.com/amazon-linux-ami/), [Red Hat Linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux), [Centos](https://www.centos.org/) and [Ubuntu](https://ubuntu.com/). This role installs all necessary packages, Apache/Apache2, PHP 7.4, Mariadb/MySQL server and also completes MySQL secure installation. This role also enables Apache virtual hosts and you can make this role custom with variables defined for this role. The variables used are given below.

## Role Variables

The variables used in this role are given below. You can edit the roles on file /vars/main.yml ,
```
domain_name: "markdevops.xyz"
httpd_group: "apache"
httpd_user: "apache"
ubuntu_user: "www-data"
ubuntu_group: "www-data"
httpd_port: "80"
mysql_root: "myroot123"
```

## How to use?

I have added this role to [Ansible Galaxy](https://galaxy.ansible.com/) and you can use it to install this role on your Ansible Server. Ansible Galaxy is a large public repository of Ansible roles. Please use the following command to install this role on your Ansible Server.
```
ansible-galaxy install markantonygit.ansible_multipleos_lamp
```
Once the role is installed on your server, you can use this role on any of your playbooks. I have created a sample playbook to run this role and it is given below.

## Example Playbook 

This playbook is just for checking the working of the role and to upload a sample index.php file to the virtual host document root. 

```
---
- name: "Testing Ansible role"
  hosts: all
  become: true
  roles:
    - markantonygit.ansible_multipleos_lamp
  tasks:

    - name: "Uploading Sample Index File to RedHat Based Distributions"
      when: ansible_os_family=="RedHat"
      copy:
        src: index.php
        dest: "/var/www/html/{{  domain_name  }}/"
        owner: "{{ httpd_user }}"
        group: "{{ httpd_group }}"

    - name: "Uploading Sample Index File to Debian Based Distributions"
      when: ansible_os_family=="Debian"
      copy:
        src: index.php
        dest: "/var/www/{{ domain_name }}/public_html/"
        owner: "{{ ubuntu_user }}"
        group: "{{ ubuntu_group }}"
```
##### Sample Index.php File

This index file displays the OS distribution of the server and the header Sample Website. 
 
```
<div style='text-align: center'><?php
echo php_uname();
echo "<h1><center>Sample Website</center></h1>"
?></div>
```

## Sample Screenshots

-- Sample Index Pages

![](https://i.ibb.co/rdyhvZg/lamp1.jpg)
![](https://i.ibb.co/hFCbL6j/lamp2.jpg)

-- Play 

![](https://i.ibb.co/gtSXGf0/lamp4.jpg)

-- Play Output

![](https://i.ibb.co/XbQcLms/lamp3.jpg)

---------------- Mark Antony ------------------------------------------------------------------------------------------------------ linkedin.com/in/mark-antony-345473211 ----------------------------------------------------------------------------------------- markantony.alenchery@gmail.com ---------------------------------------------
                                                        
