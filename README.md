# nephelaiio.playbooks-freeipa

[![Build Status](https://travis-ci.org/nephelaiio/ansible-playbooks-freeipa.svg?branch=master)](https://travis-ci.org/nephelaiio/ansible-playbooks-freeipa)

A set of ansible playbooks to install and configure [FreeIPA](https://www.freeipa.org/). Extends existing playbooks and roles available directly from [FreeIPA](https://github.com/freeipa/ansible-freeipa)

## Playbook descriptions

The following lists the group targets and descriptions for every playbook

| playbook    | description                                | target      |
| ---         | ---                                        | ---         |
| server.yml  | install/configure freeipa server           | ipa_server  |
| replica.yml | install/configure freeipa server           | ipa_replica |
| nginx.yml   | install ngnix reverse proxy for freeipa ui | ipa_proxy   |
| client.yml  | install ngnix reverse proxy for freeipa ui | ipa_client  |

## Playbook variables

See [Ansible FreeIPA](https://github.com/freeipa/ansible-freeipa#ansible-inventory-file) documentation for a list of additional supported variables

### [server.yml](local.yml):
| required | variable       | description                                 | default   |
| ---      | ---            | ---                                         | ---       |
| no       | pdns_recursors | pdns recursors to register delegations with | undefined |

### [nginx.yml](nginx.yml):
| required | variable                              | description                                  | default                                |
| ---      | ---                                   | ---                                          | ---                                    |
| *yes*    | ipa_url                               | target freeipa proxy url                     | n/a                                    |
| *yes*    | acme_certificate_email                | letsencrypt email                            | n/a                                    |
| *yes*    | acme_certificate_aws_accesskey_id     | an ec2 key id with route53 management rights | lookup('env', 'AWS_ACCESS_KEY_ID')     |
| *yes*    | acme_certificate_aws_accesskey_secret | an ec2 key secret                            | lookup('env', 'AWS_SECRET_ACCESS_KEY') |

[replica.yml](replica.yml) and [client.yml](client.yml) playbooks have to user defined parameters

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
