# Ansible Role for Lutim (Let's Upload That Image)

[![Build Status](https://travis-ci.org/noplanman/ansible-lutim.svg?branch=master)](https://travis-ci.org/noplanman/ansible-lutim)

Installs and configures Lutim on Debian/Ubuntu servers.
Find out more about Lutim [here](https://framagit.org/luc/lutim), created by [Luc Didry](https://framagit.org/u/luc).

This role will automatically install a service that will start when the server boots up.
It will figure out which service manager is being used automatically too.

## Requirements

Using this role doesn't install Nginx or Apache as a reverse proxy, you need to do that yourself!
An example configuration for Nginx can be found [here](https://framagit.org/luc/lutim/wikis/installation#putting-lutim-behind-nginx).

## Role Variables

Set the user/group that will be used to run Lutim. It makes sense to use the webserver user/group.

```
lutim_user: www-data
lutim_group: www-data
```

There are a few mandatory and many optional values. Check all possible variables in `defaults/main.yml`.

```
# Required!
lutim_working_dir: "/var/www/example.com"
lutim_listen: "http://127.0.0.1:8080"
lutim_contact: "admin@example.com"
lutim_secrets: ["array", "of", "random", "secrets"]
# Optional
lutim_theme: "default"
lutim_hosted_by: 'My super hoster <img src="http://hoster.example.com" alt="Hoster logo">'
lutim_broadcast_message: "Maintenance"
lutim_allowed_domains: []
```

## Role Tags

Each part of the setup has a tag.

```
lutim.install
lutim.site
lutim.service
```

## Dependencies

None.

## Example Playbook

```
# playbook.yml
---
- hosts: servers
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - { role: noplanman.lutim }
```
```
# vars/main.yml
---
lutim_working_dir: "/var/www/lutim.example.com"
lutim_listen: "http://127.0.0.1:8080"
lutim_contact: "admin@lutim.example.com"
lutim_secrets: ["eo5jeiD8","OhshiGh2","mieSh0po","iD6ohNg2","gueb4Mee","VoeNgei5","kaV3EeT2","en9Ohshi"]
lutim_broadcast_message: "Welcome to Lutim. Upload those images!"
```

## License

MIT
