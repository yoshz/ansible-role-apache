# enrise.apache

This is an Ansible task for installing and configuring Apache (2.4),
as well as creating virtualhosts and directory permissions.

## Requirements

- Tested on Ansible 1.5
- Tested on Ubuntu 14.04 (trusty), but it should work on any modern Debian based system.

## Dependencies

None.

## Example playbook

To use this role, build a vars file (vars/apache.yml, for example) which you include in your playbook,
which contains something like the following:

    # A list of virtualhosts to create.
    apache_virtualhosts:
      hostname:
        hostname: 'myhostname.example.org'
        alias: 'alias.example.org'
        docroot: '/var/www'
      vhosts:
        hostname: 'virtual_docroot'
        virtual_docroot: '/var/www/sites/%0/public
      ssl:
        hostname: ssl.example.org
        docroot: '/var/www/sites/ssl/public'
        ssl_certfile: 'files/ssl.crt'
        ssl_keyfile: 'files/ssl.key'
        ssl_chainfile: 'files/ssl-chain.crt'

    # Directory permissions
    apache_directories:
      sites-public:
        directory: /var/www/sites/*/public
        options: FollowSymLinks
        allow_override: All

    # The port Apache should listen on.
    apache_listen_port: 80

    # The apache modules that should be enabled.
    apache_modules:
     - rewrite

    # The run user and group, if you wish to overwrite these.
    apache_run_user: 'vagrant'
    apache_run_group: 'vagrant'

Next, you can include the role in your playbook:

    - hosts: all
      sudo: yes
      vars_files:
        - vars/apache.yml
      roles:
        - enrise.apache

There are a lot of config settings you can overwrite, but you'll have to refer to the files
`defaults/main.yml` to see a list of variables and their description.

## Licence

MIT

## Feedback? Found a bug? Requests?

Let us have it! http://github.com/Enrise/ansible-role-apache/issues
