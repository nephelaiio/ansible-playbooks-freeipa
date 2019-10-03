# nephelaiio.playbooks-freeipa

[![Build Status](https://travis-ci.org/nephelaiio/ansible-playbooks-freeipa.svg?branch=master)](https://travis-ci.org/nephelaiio/ansible-playbooks-freeipa)

A set of ansible playbooks to install and configure [FreeIPA](https://www.freeipa.org/). Extends existing playbooks and roles available directly from [FreeIPA](https://github.com/freeipa/ansible-freeipa)

## Playbook descriptions

The following lists the group targets and descriptions for every playbook

| playbook    | description                       | target      |
| ---         | ---                               | ---         |
| server.yml  | install/configure freeipa server  | ipa_server  |
| replica.yml | install/configure freeipa replica | ipa_replica |
| client.yml  | instal/configure freeipa client   | ipa_client  |
| users.yml   | manage ipa users and groups       | ipa_user    |

## Playbook variables

See [Ansible FreeIPA](https://github.com/freeipa/ansible-freeipa#ansible-inventory-file) documentation for a list of additional supported variables

### [server.yml](server.yml):
| required | variable       | description                                 | default   |
| ---      | ---            | ---                                         | ---       |
| no       | pdns_recursors | pdns recursors to register delegations with | undefined |

### [users.yml](users.yml):
| required | variable        | description              | default   |
| ---      | ---             | ---                      | ---       |
| no       | ipa_groups      | ipa groups to manage     | undefined |
| no       | ipa_users       | ipa users to manage      | undefined |
| no       | ipa_users_host  | ipa server to connect to | undefined |
| no       | ipa_users_debug | toggle debug logging     | false     |

### [client.yml](client.yml):
| required | variable                            | description                                     | default          |
| ---      | ---                                 | ---                                             | ---              |
| no       | freeipa_pki_autogen                 | toggle flag for host certificate autogeneration | yes              |
| no       | freeipa_pki_certdir                 | cert file location                              | /etc/pki/certs   |
| no       | freeipa_pki_keydir                  | cert key location                               | /etc/pki/private |
| no       | ipaclient_krb_overrides             | krb5.conf overrides for [libdefaults] section   | []               |
| no       | ipaclient_ssh_login_manage          | toggle ssh login management                     | no               |
| no       | ipaclient_ssh_login_password_enable | enable ssh login passwords                      | no               |

The generated cert and key files will be located at "{{ freeipa_pki_certdir }}/{{ ansible_fqdn }}.crt" and "{{ freeipa_pki_keydir }}/{{ ansible_fqdn }}.key" by default

[client.yml](client.yml) playbook has no user defined parameters

## Data Formats

### Groups
```{yaml}
ipa_groups:
  - name: test_group
    state: present
```

### Users
```{yaml}
ipa_users:
  - user_name: test_user
    groups:
      - test_group
    pass: supersecret
    first_name: Test
    last_name: User
    telephonenumber: 55566778899
    mail: user@test.com
    update_password: on_create
    state: present
```

## Dependencies

These playbooks have the following git submodule dependencies:

* [submodules/ansible-freeipa](https://github.com/freeipa/ansible-freeipa)

And role dependencies:

* [bertvv.hosts](https://galaxy.ansible.com/bertvv/hosts)
* [nginxinc.nginx](https://galaxy.ansible.com/nginxinc/nginx)
* [nephelaiio.acme_certificate_route53](https://galaxy.ansible.com/nephelaiio/acme_certificate_route53)
* [nephelaiio.plugins](https://galaxy.ansible.com/nephelaiio/plugins)

## Example Invocation

```
git checkout https://galaxy.ansible.com/nephelaiio/ansible-playbooks-freeipa freeipa
ansible-playbook -i inventory/ freeipa/server.yml
```

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
