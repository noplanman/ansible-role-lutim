# Ansible Role for Lutim (Let's Upload That Image)

[![Build Status][travis-build-status]][travis-tests]

---

:rocket: Development has moved to **[git.feneas.org]**.

(The repository on GitHub is only a mirror, so fork on Feneas to contribute. No registration needed, just sign in with your GitHub account.)

---

This role installs and configures Lutim on Debian/Ubuntu servers.
Find out more about [Lutim], created by [Luc Didry].

This role will automatically install a service that will start when the server boots up.
It will figure out which service manager is being used automatically too.

## Requirements

Using this role doesn't install Nginx or Apache as a reverse proxy, you need to do that yourself!
Take a look at the [example configurations].

## Role Variables

Set the user/group that will be used to run Lutim. It makes sense to use the webserver user/group.

```
lutim_user: www-data
lutim_group: www-data
```

Set if Lutim should be kept up to date. (default: no)

```
lutim_keep_updated: no
```

There are a few mandatory and many optional values. Check all possible variables in [`defaults/main.yml`][defaults].

```
# Required!
lutim_working_dir: "/var/www/example.com"
lutim_listen: "http://127.0.0.1:8080"    # Or an array, if multiple addresses.
lutim_contact: "admin@example.com"
lutim_secrets: ["array", "of", "random", "secrets"]

# Optional
lutim_theme: "default"
lutim_proxy: no
lutim_url_length: 8
lutim_crypto_key_length: 8
lutim_provis_step: 5
lutim_provisioning: 100
lutim_anti_flood_delay: 5
lutim_tweet_card_via: "@foo"
lutim_max_file_size: 10485760
lutim_piwik_img: ""
lutim_hosted_by: ""
lutim_broadcast_message: ""
lutim_allowed_domains: []
lutim_default_delay: 0
lutim_max_delay: 0
lutim_always_encrypt: no
lutim_token_length: 24
lutim_prefix: "/"
lutim_db_type: "sqlite"
lutim_db_path: "lutim.db"
lutim_pgdb:
    database: "lutim"
    host: "localhost"
    user: "DBUSER"
    pwd: "DBPASSWORD"
minion:
    enabled: yes
    db_type: "sqlite"
    db_path: "minion.db" # SQLite ONLY
    pgdb:                # PostgreSQL ONLY
        database: "lutim_minion"
        host: "localhost"
        user: "DBUSER"
        pwd: "DBPASSWORD"
lutim_ldap:
    uri: "ldaps://ldap.example.org"
    user_tree: "ou=users,dc=example,dc=org"
    bind_dn: "uid=ldap_user,ou=users,dc=example,dc=org"
    bind_pwd: "secr3t"
    user_attr: "uid"
    user_filter: "(!(uid=ldap_user))"
lutim_htpasswd: "lutim.passwd"
lutim_session_duration: 3600
lutim_disable_img_stats: no
lutim_thumbnail_size: 100
lutim_max_files_in_zip: 15
lutim_cache_max_size: 0
lutim_memcached_servers: []
lutim_quiet_logs: no
lutim_csp: "default-src 'none'; script-src 'self'; style-src 'self'; img-src 'self' data:; font-src 'self'; form-action 'self'; base-uri 'self'"
lutim_x_frame_options: "DENY"
lutim_x_content_type_options: "nosniff"
lutim_x_xss_protection: "1; mode=block"
lutim_fixed_domain: "example.org"
lutim_stats_day_num: 365
lutim_keep_ip_during: 365
lutim_max_total_size: 10*1024*1024*1024
lutim_policy_when_full: "warn"
lutim_delete_no_longer_viewed_files: 90
```

## Role Tags

Each part of the setup has a tag.

```
lutim:install
lutim:site
lutim:service
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

## Tests

Docker is used to test the role with different operating systems.

*(from `.travis.yml`)*
```bash
$ wget -O ${PWD}/tests/test.sh https://gist.githubusercontent.com/noplanman/40e96f31ee2301469769d4236aff40e2/raw/
$ chmod +x ${PWD}/tests/test.sh
$ distro=ubuntu1604 ${PWD}/tests/test.sh
$ distro=ubuntu1404 ${PWD}/tests/test.sh
$ distro=debian9 ${PWD}/tests/test.sh
$ distro=debian8 ${PWD}/tests/test.sh
```

## License

MIT

[travis-build-status]: https://travis-ci.org/noplanman/ansible-role-lutim.svg?branch=master "Travis-CI Build Status"
[travis-tests]: https://travis-ci.org/noplanman/ansible-role-lutim "Travis-CI Tests"
[git.feneas.org]: https://git.feneas.org/noplanman/ansible-role-lutim "Ansible Role Lutim on Feneas"
[Lutim]: https://framagit.org/luc/lutim "Lutim on Framagit"
[Luc Didry]: https://framagit.org/u/luc "Luc on Framagit"
[example configurations]: https://framagit.org/luc/lutim/wikis/installation#putting-lutim-behind-nginx "Example configurations"
[defaults]: https://git.feneas.org/noplanman/ansible-role-lutim/blob/master/defaults/main.yml "Default variables"
