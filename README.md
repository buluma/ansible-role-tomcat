# [Ansible role tomcat](#ansible-role-tomcat)

Install and configure tomcat on your system.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-tomcat/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-tomcat/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-tomcat/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-tomcat)|[![downloads](https://img.shields.io/ansible/role/d/buluma/tomcat)](https://galaxy.ansible.com/buluma/tomcat)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-tomcat.svg)](https://github.com/buluma/ansible-role-tomcat/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-tomcat/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
- become: true
  gather_facts: true
  hosts: all
  name: Converge
  roles:
  - role: buluma.tomcat
  vars:
    tomcat_instances:
    - name: tomcat
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-tomcat/blob/master/molecule/default/prepare.yml):

```yaml
- become: true
  gather_facts: false
  hosts: all
  name: Prepare
  roles:
  - role: buluma.bootstrap
  - role: buluma.core_dependencies
  - role: buluma.java
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-tomcat/blob/master/defaults/main.yml):

```yaml
_tomcat_unarchive_urls:
  7:
    url: '{{ tomcat_mirror }}/dist/tomcat/tomcat-7/v{{ tomcat_version7 }}/bin/apache-tomcat-{{
      tomcat_version7 }}.tar.gz'
  8:
    url: '{{ tomcat_mirror }}/dist/tomcat/tomcat-8/v{{ tomcat_version8 }}/bin/apache-tomcat-{{
      tomcat_version8 }}.tar.gz'
  9:
    url: '{{ tomcat_mirror }}/dist/tomcat/tomcat-9/v{{ tomcat_version9 }}/bin/apache-tomcat-{{
      tomcat_version9 }}.tar.gz'
  10:
    url: '{{ tomcat_mirror }}/dist/tomcat/tomcat-10/v{{ tomcat_version10 }}/bin/apache-tomcat-{{
      tomcat_version10 }}.tar.gz'
tomcat_access_log_directory: logs
tomcat_access_log_enabled: true
tomcat_access_log_pattern: '%h %l %u %t &quot;%r&quot; %s %b'
tomcat_access_log_prefix: localhost_access_log
tomcat_access_log_suffix: .txt
tomcat_address: 0.0.0.0
tomcat_ajp_enabled: true
tomcat_ajp_port: 8009
tomcat_ajp_secret: SoMe-SeCrEt
tomcat_directory: /opt
tomcat_group: tomcat
tomcat_instances:
- access_log_directory: '{{ tomcat_access_log_directory }}'
  access_log_enabled: '{{ tomcat_access_log_enabled }}'
  access_log_pattern: '{{ tomcat_access_log_pattern }}'
  access_log_prefix: '{{ tomcat_access_log_prefix }}'
  access_log_suffix: '{{ tomcat_access_log_suffix }}'
  ajp_enabled: '{{ tomcat_ajp_enabled }}'
  ajp_port: '{{ tomcat_ajp_port }}'
  ajp_secret: '{{ tomcat_ajp_secret }}'
  group: '{{ tomcat_group }}'
  java_opts:
  - name: JRE_HOME
    value: '{{ tomcat_jre_home }}'
  name: '{{ tomcat_name }}'
  non_ssl_connector_port: '{{ tomcat_non_ssl_connector_port }}'
  packet_size: 8192
  service_enabled: '{{ tomcat_service_enabled }}'
  service_state: '{{ tomcat_service_state }}'
  shutdown_port: '{{ tomcat_shutdown_port }}'
  ssl_connector_port: '{{ tomcat_ssl_connector_port }}'
  user: '{{ tomcat_user }}'
  version: '{{ tomcat_version }}'
  xms: '{{ tomcat_xms }}'
  xmx: '{{ tomcat_xmx }}'
tomcat_jre_home: /usr
tomcat_mirror: https://archive.apache.org
tomcat_name: tomcat
tomcat_non_ssl_connector_port: 8080
tomcat_service_enabled: true
tomcat_service_state: started
tomcat_shutdown_pass: SHUTDOWN
tomcat_shutdown_port: 8005
tomcat_ssl_connector_port: 8443
tomcat_unarchive_url: '{{ _tomcat_unarchive_urls[tomcat_version].url }}'
tomcat_user: tomcat
tomcat_version: 8
tomcat_version10: 10.1.20
tomcat_version7: 7.0.109
tomcat_version8: 8.5.100
tomcat_version9: 9.0.87
tomcat_xms: 512M
tomcat_xmx: 1024M
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-tomcat/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-core_dependencies)|
|[buluma.java](https://galaxy.ansible.com/buluma/java)|[![Build Status GitHub](https://github.com/buluma/ansible-role-java/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-java/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-java/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-java)|
|[buluma.service](https://galaxy.ansible.com/buluma/service)|[![Build Status GitHub](https://github.com/buluma/ansible-role-service/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-service/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-service/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-service)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-tomcat/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[opensuse](https://hub.docker.com/r/buluma/opensuse)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-tomcat/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-tomcat/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

