# Ansible role for Supervisor

[![Build Status](https://travis-ci.org/torian/ansible-role-supervisor.svg)](https://travis-ci.org/torian/ansible-role-supervisor)

This role will install [Supervisor](https://supervisord.org/), a process 
control system


## Tested on

  * Ubuntu trusty
  * Amazon Linux 2015.03


## Defaults

  * `supervisor_cfg_loglevel`: info
  * `supervisor_services`: `{}`


## Usage

Services are configured using the `supervisor_services` hash,
in which every entry is a different service. In turn, you can
specify any supervisor parameter you need.


### Running a command

```
---
- hosts: localhost

  vars:
    - supervisor_services:
        celery:
          command:        celery -A tasks worker --loglevel=info
          directory:      /opt/celery_app
          process_name:   celery_worker
          num_procs:      2
          autostart:      true
          stdout_logfile: /var/log/supervisor/celery-app.log
          stderr_logfile: /var/log/supervisor/celery-app.err
        
  roles:
    - role: ansible-role-supervisor

```


## TODO

  * Make a template for the main supervisord config
  * Event listeners
  * more things ?

