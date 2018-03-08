# {{cookiecutter.application_name}} Ansible Deployment Automation

This is an Ansible playbook accompanying {{cookiecutter.application_name}}. It provides means to deploy
{{cookiecutter.application_name}} to an Ubuntu server with root access to it. It will:

 - create a virtualenv and install `{{cookiecutter.package_name}}` setuptools package into it, or update it if it is
   already installed but changed since last deployment

 - install uWSGI, or update it if it's version changed since last deployment

 - create a service running {{cookiecutter.application_name}} in a uWSGI instance, and ensure the service is running

 - install nginx and configure it as a reverse proxy to a uWSGI instance running {{cookiecutter.application_name}};
   update configuration if any changes are made since last deployment


## Prerequisites

 - Ubuntu development machine

 - [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html): `sudo pip install ansible`

 - required roles, install with `ansible-galaxy install -r requirements.yml`

 - to test the playbook, [Vagrant](https://www.vagrantup.com/) and [Virtualox](https://www.virtualbox.org/):
   `sudo apt install vagrant virtualbox`

 - to deploy to production, an Ubuntu server with ssh access to it and possibility to escalate privileges to root


## Test

    vagrant up


## Deploy to production

Create Ansible [inventory file](http://docs.ansible.com/ansible/latest/intro_inventory.html) with
the list of servers to deploy to. Use included `inventory.ini` as a template.

> Heads up! `inventory.ini` file from this repository is ignored by Git. It won't be included into any commits
> (unless forced) and it is local to your work station therefore.

> Inventory file can be placed to any other location, if this is more suitable.
> [Anisble Inventory](http://docs.ansible.com/ansible/latest/intro_inventory.html) gives more details.

To run the deployment:

    ansible-playbook playbook.yml -i inventory.ini


## Install Python on target server

Ansible requires Python to be installed on the target server to run most of the tasks. It it is not the case with
your server, use `bootstrap.yml` playbook to fix this. This is how `Vagrantfile` works.


## Maintain target server up to date

Use included `osupgrade.yml` playbook to upgrade OS packages.
