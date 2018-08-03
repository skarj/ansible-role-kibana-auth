Kibana-uth role
=========
[![Build Status](https://api.travis-ci.org/skarj/ansible-role-kibana-auth.svg?branch=master)](https://travis-ci.org/skarj/ansible-role-kibana-auth)

Ansible role that installs and configure HTTPD as a revers proxy in front of Kibana
with ldap and file authentications. The LDAP provider will attempt to authenticate the user first.
If it is unable to authenticate the user, the file provider will be called.


Requirements
------------

* Ansible 2.5
* This role requires [hash_behaviour=merge](http://docs.ansible.com/ansible/latest/reference_appendices/config.html#default-hash-behaviour) for variables


Dependencies
------------

None


Role Variables
--------------

Default config variables are described in *defaults/main.yml*.
This is a description for main variables which you may want to change.

  * _kibana.address_ Kibana URL
  * _kibana-auth.port_ port HTTPD will listen on
  * _kibana-auth.Name_ the name of the authorization realm for a directory
  * _kibana-auth.UserFile_ path to the user file
  * _kibana-auth.ldapBindDN_ optional DN to use in binding to the LDAP server
  * _kibana-auth.BindPassword_ password for the bind DN
  * _kibana-auth.ldapURL_ URL specifying the LDAP search parameters. An RFC 2255 URL which specifies the LDAP search parameters to use
     example: "ldap://ldap1.example.com ldap2.example.com/dc=..."
  * _kibana-auth.ldap.Group_ LDAP group whose members are allowed access
     example: "CN=kibana-users,OU=groups,DC=example,DC=com"


Example Playbook
----------------

An example of how to use this role:

        - hosts: all
          roles:
            - role: ansible-role-kibana
              kibana_auth:
                name: "Active Directory authentication"
                UserFile: "/etc/nginx/htpasswd.user"
                ldap:
                  BindDN: "authuser@example.com"
                  BindPassword: "secret_pass"
                  URL: 'ldap://192.168.93.187:389/DC=example,DC=com?sAMAccountName?sub?(objectClass=*)'
                kibana:
                  address: "http://127.0.0.1:5601"

License
-------

MIT


Author Information
------------------

Sergey Baranov <skaarj.sergey@gmail.com>
