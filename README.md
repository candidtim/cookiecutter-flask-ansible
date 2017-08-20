# flask-ansible for flask-minimal

This is an Ansible playbook template accompanying [flask-minimal](https://github.com/candidtim/cookiecutter-flask-minimal)
cookiecutter template. It provides means to deploy `flask-minimal` application on an Ubuntu server.


## Usage

Install `cookiecutter` and create a Flask application as per
[flask-minimal](https://github.com/candidtim/cookiecutter-flask-minimal) and build it (`make sdist`).

Create accompanying Ansible project from this template. Put it side-by-side with the Flask application
created above (in the same root directory), and use same value for application package name, or you will need to change
generated configuration accordingly:

    cookiecutter https://github.com/candidtim/cookiecutter-flask-ansible.git

Install prerequisites as per generated README, and then run the application in the Virtualbox to test the generated
configuration:

    cd yourapplication-ansible
    vagrant up

And open deployed application at [http://127.0.0.1:8080/](http://127.0.0.1:8080/)

When ready, deploy to the server with:

  ansible-playbook playbook.yml -i inventory.ini


## Provided configuration

 - [setuptools-ready `Flask` application](http://flask.pocoo.org/docs/0.12/patterns/distribute/) installs into a
   dedicated virtualenv
 - runs in a uWSGI web server instance, installed into the same virtualenv
 - nginx server is used as a reverse proxy
 - all this is installed on an Ubuntu server, with a systemd service to run uWSGI instance
 - for tests only, Vagrant and Virtualbox are used

This implementation also assumes an Ubuntu development machine.


# Opinionated, while still being minimal and production ready

This template is much more opinionated compared to the `flask-minimal`, but it still strives to be minimal and
production-ready in its own way.

Deploying Flask application to production implies a lot of choice: OS version, WSGI implementation, reverse proxy
HTTP server, logging configuration, maybe other ones. It is hard to provide a solution flexible enough to fit all
possible needs: such an attempt will likely result in a very complex solution, and will still require customizations in
most of real-world scenarios. More importantly, it is rarely required: for example, most projects won't require to be
deployed to different WSGI servers at the same time, but stick to one of them.

This is why this project, instead, provides a simple solution, which is ready for use, but makes a couple of choices.
You can use this in two cases:

 - if choices made here fit your needs
 - or as an example to build your own configuration


# Contributions

... are welcome! Feel free to create a pull request to fix bugs, keep up to date, or propose a feature.
