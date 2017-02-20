Let's Encrypt Ansible Role for nginx
==========================

Provides ssl certificates management by letsencrypt for nginx servers.

Note that the full certificates installation process is not implemented yet.
For now you'll have to manually include SSL configuration into your server config file like so:

```
server
{

    # ...

    include snippets/ssl-params.conf;
    include snippets/ssl-example.com.conf;

    # ...

}
```

Requirements
------------

Make the webroot authentication path available in your HTTP nginx configuration before playing the role, e. g.:

```
server
{
    server_name  example.com;
    listen       80;

    # letsencrypt webroot authentication
    location ~ /.well-known/acme-challenge {
        root /var/www/letsencrypt;
        allow all;
    }
    
    # Redirect all http traffic to https
    location / {
        return 301 https://$host$request_uri;
        add_header  X-Clacks-Overhead "GNU Terry Pratchett";
    }
}
```

Role Variables
--------------

TBD

Dependencies
------------

TBD

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: ozean12.letsencrypt, letsencrypt_primary_domain: example.com, letsencrypt_email: admin@example.com }

License
-------

MIT

Author Information
------------------

TBD
