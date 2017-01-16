Mailhog
=======

[![Build Status](https://travis-ci.org/jebovic/ansible-mailhog.svg?branch=master)](https://travis-ci.org/jebovic/ansible-mailhog) [![Ansible Galaxy](https://img.shields.io/badge/galaxy-jebovic.mailhog-blue.svg?style=flat)](https://galaxy.ansible.com/jebovic/mailhog)

Download, install and configure Mailhog, a great mail catcher

This role is a part of my [OPS project](https://github.com/jebovic/ops), follow this link to see it in action. OPS provides a lot of stuff, like a vagrant file for development VMs, playbooks for roles orchestration, inventory files, examples for roles configuration, ansible configuration file, and many more.

Compatibility
-------------

Tested and approved on :

* Debian jessie (8+)
* Ubuntu Trusty (14.04 LTS)
* Ubuntu Xenial (16.04 LTS)

Dependencies
------------

This role depends on [jebovic.supervisor](https://github.com/jebovic/ansible-supervisor) role to be fully functional

Role Variables
--------------

```yaml
# Mailhog installation configuration
mailhog_install_dir: /usr/local/bin
mailhog_binary_url: https://github.com/mailhog/MailHog/releases/download/v0.2.1/MailHog_linux_amd64
mhsendmail_binary_url: https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64
sendmail_bin_path: /usr/bin/sendmail
mailhog_bin_path: "{{ mailhog_install_dir }}/mailhog"
mailhog_mhsendmail_path: "{{ mailhog_install_dir }}/mhsendmail"
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - { role: jebovic.mailhog }
     - { role: jebovic.supervisor }
```

Example : config
----------------

```yaml
# launch mailhog with supervisor
supervisor_programs:
  mailhog:
    command: /usr/local/bin/mailhog -api-bind-addr :8025 -ui-bind-addr :8025
    autostart: "true"
    autorestart: "true"
    stderr_logfile: "{{ supervisor_log_path }}/mailhog-stderr.log"

supervisor_events:
  httpok:
    command: httpok -p mailhog http://localhost:8025
    events: TICK_60
```

License
-------

MIT

Author Information
------------------

Jérémy Baumgarth https://github.com/jebovic
