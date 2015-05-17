ajgarlag.apache2
================

Ansible role to install and configure apache2


Role Variables
--------------

```yml
# If true, default HTTP virtual host will be enabled
ajgarlag_apache2_vhost_default_http: yes

# If true, default HTTPS virtual host will be enabled
ajgarlag_apache2_vhost_default_https: no

# Path to the HTTPS certificate file
ajgarlag_apache2_https_cert: /etc/ssl/certs/ssl-cert-snakeoil.pem

# Path to the HTTPS key file
ajgarlag_apache2_https_key: /etc/ssl/private/ssl-cert-snakeoil.key

# Path to the HTTPS CA chain file
#ajgarlag_apache2_https_chain:

# Log format
ajgarlag_apache2_log_format: combined

# Virtual hosts to define
ajgarlag_apache2_vhosts: {}
#  "example.org":
#    template: custom-template.j2
#    documentroot: /srv/www/example.org #required for vhost.conf.j2 template
#    serveralias: www.example.org example.com www.example.com
#    serveradmin: webmaster@example.org
#    ssl: yes
#    ssl_cert: '{{ ajgarlag_apache2_https_cert }}'
#    ssl_key: '{{ ajgarlag_apache2_https_key }}'
#    ssl_chain: /etc/ssl/certs/chain.pem
#    directories:
#     /usr/share/app1: ~
#     /usr/share/app2:
#       options: Indexes FollowSymLinks MultiViews
#       override: All
#       extras:
#         - Order allow,deny
#         - allow from all
#    aliases:
#      application1: /usr/share/app1
#      application2: /usr/share/app2
#    extras:
#      - LogLevel warn
#      - ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/

# List of extra virtual host to enable
ajgarlag_apache2_sites_enabled: []

# List of virtual host to disable
ajgarlag_apache2_sites_disabled: []

# List of modules to enable
ajgarlag_apache2_modules_enabled: []

# List of modules to disable
ajgarlag_apache2_modules_disabled: []
```


Example Playbook
----------------

```yml
- hosts: all
  vars:
    ajgarlag_apache2_vhost_default_http: no
    ajgarlag_apache2_vhost_default_https: no
    ajgarlag_apache2_https_cert: /etc/ssl/certs/example.com.pem
    ajgarlag_apache2_https_key: /etc/ssl/private/example.com.key
    ajgarlag_apache2_log_format: vhost_combined
    ajgarlag_apache2_vhosts:
      "example.com":
        documentroot: /srv/www/example.com
        serveralias: www.example.com
        serveradmin: webmaster@example.com
        directories:
         /usr/share/wordpress:
           override: All
        aliases:
          blog: /usr/share/wordpress
        extras:
          - CustomLog "|/usr/bin/logger -p local2.notice -t apache" combined
  roles:
    - role: ajgarlag.apache2
```


License
-------

MIT


Author Information
------------------

Developed with ♥ by [Antonio J. García Lagar](http://aj.garcialagar.es).