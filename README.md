# Ansible role [tomcat](https://galaxy.ansible.com/ui/standalone/roles/buluma/tomcat/documentation)

Install and configure tomcat on your system.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-tomcat/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-tomcat/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-tomcat.svg)](https://github.com/buluma/ansible-role-tomcat/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-tomcat.svg)](https://github.com/buluma/ansible-role-tomcat/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-tomcat.svg)](https://github.com/buluma/ansible-role-tomcat/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/tomcat)](https://galaxy.ansible.com/ui/standalone/roles/buluma/tomcat/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-tomcat/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    # tomcat_address: "127.0.0.1"
    tomcat_instances:
      - name: "tomcat"
      # - name: "tomcat-version-7"
      #   version: 7
      #   shutdown_port: 8007
      #   non_ssl_connector_port: 8082
      #   ssl_connector_port: 8445
      #   ajp_port: 8011
      # - name: "tomcat-version-8"
      #   version: 8
      #   shutdown_port: 8008
      #   non_ssl_connector_port: 8083
      #   ssl_connector_port: 8446
      #   ajp_port: 8012
      # - name: "tomcat-version-9"
      #   version: 9
      #   shutdown_port: 8019
      #   non_ssl_connector_port: 8084
      #   ssl_connector_port: 8447
      #   ajp_port: 8013
      # - name: "tomcat-specific"
      #   user: "specificuser"
      #   group: "specificgroup"
      #   shutdown_port: 8020
      #   shutdown_pass: shutme
      #   non_ssl_connector_port: 8085
      #   ssl_connector_port: 8448
      #   ajp_port: 8014
      #   xms: 256M
      #   xmx: 512M
      # - name: "tomcat-with-wars"
      #   shutdown_port: 8021
      #   non_ssl_connector_port: 8086
      #   ssl_connector_port: 8449
      #   ajp_port: 8015
      #   wars:
      #     - url: https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war
      #     - url: "https://github.com/aeimer/java-example-helloworld-war/raw/master/dist/helloworld.war"
      # - name: "tomcat-java_opts"
      #   shutdown_port: 8022
      #   non_ssl_connector_port: 8087
      #   ssl_connector_port: 8449
      #   ajp_port: 8016
      #   java_opts:
      #     - name: UMASK
      #       value: "0007"
      # - name: "tomcat-with_lib"
      #   shutdown_port: 8023
      #   non_ssl_connector_port: 8088
      #   ssl_connector_port: 8450
      #   ajp_port: 8017
      #   libs:
      #     - url: "https://search.maven.org/remotecontent?filepath=io/prometheus/simpleclient/0.6.0/simpleclient-0.6.0.jar"
      # - name: "tomcat-access-logs"
      #   shutdown_port: 8024
      #   non_ssl_connector_port: 8089
      #   ssl_connector_port: 8451
      #   ajp_port: 8018
      #   access_log_enabled: yes
      #   access_log_directory: "my-logs"
      #   access_log_prefix: my-access-logs
      #   access_log_suffix: ".log"
      #   access_log_pattern: "%h %l %u %t &quot;%r&quot; %s %b"
      # - name: "tomcat-config-files"
      #   shutdown_port: 8025
      #   non_ssl_connector_port: 8090
      #   ssl_connector_port: 8452
      #   ajp_port: 8019
      #   ajp_secret: "SoMe-SeCrEt"
      #   config_files:
      #     - src: "{{ role_path }}/files/dummy.properties"
      #       dest: "./"
      #       mode: "0644"

  roles:
    - role: buluma.tomcat
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-tomcat/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: buluma.bootstrap
    - role: buluma.core_dependencies
    - role: buluma.java
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-tomcat/blob/master/defaults/main.yml):

```yaml
---
# defaults file for tomcat

# Some "sane" defaults.
tomcat_name: tomcat
tomcat_directory: /opt
tomcat_version: 8
tomcat_user: tomcat
tomcat_group: tomcat
tomcat_xms: 512M
tomcat_xmx: 1024M
tomcat_non_ssl_connector_port: 8080
tomcat_ssl_connector_port: 8443
tomcat_shutdown_port: 8005
tomcat_shutdown_pass: SHUTDOWN
tomcat_ajp_enabled: yes
tomcat_ajp_port: 8009
tomcat_ajp_secret: "SoMe-SeCrEt"
tomcat_jre_home: /usr
tomcat_service_state: started
tomcat_service_enabled: yes
# You can bind Tomcat to a specified address globally using this variable, or
# in the `tomcat_instances`. The `tomcat_instances.address` is more specific
# so it takes priority over `tomcat_address`.
tomcat_address: "0.0.0.0"

# Configure tomcat access logs
tomcat_access_log_enabled: yes
tomcat_access_log_directory: logs
tomcat_access_log_prefix: localhost_access_log
tomcat_access_log_suffix: ".txt"
tomcat_access_log_pattern: "%h %l %u %t &quot;%r&quot; %s %b"

# This role allows multiple installations of Apache Tomcat, each in their own
# location, potentially of different version.
# This is done by defining a "tomcat_instances" where "name:" is a unique
# identifier of an instance.
# The default tomcat_instances is one instance using the defaults described
# in defaults/main.yml.
tomcat_instances:
  - name: "{{ tomcat_name }}"
    version: "{{ tomcat_version }}"
    user: "{{ tomcat_user }}"
    group: "{{ tomcat_group }}"
    xms: "{{ tomcat_xms }}"
    xmx: "{{ tomcat_xmx }}"
    non_ssl_connector_port: "{{ tomcat_non_ssl_connector_port }}"
    ssl_connector_port: "{{ tomcat_ssl_connector_port }}"
    shutdown_port: "{{ tomcat_shutdown_port }}"
    ajp_enabled: "{{ tomcat_ajp_enabled }}"
    ajp_port: "{{ tomcat_ajp_port }}"
    ajp_secret: "{{ tomcat_ajp_secret }}"
    # You can pick an address per instance:
    # address: "127.0.0.1"
    packet_size: 8192
    java_opts:
      - name: JRE_HOME
        value: "{{ tomcat_jre_home }}"
    access_log_enabled: "{{ tomcat_access_log_enabled }}"
    access_log_directory: "{{ tomcat_access_log_directory }}"
    access_log_prefix: "{{ tomcat_access_log_prefix }}"
    access_log_suffix: "{{ tomcat_access_log_suffix }}"
    access_log_pattern: "{{ tomcat_access_log_pattern }}"
    service_state: "{{ tomcat_service_state }}"
    service_enabled: "{{ tomcat_service_enabled }}"

# The explicit version to use when referring to the short name.
tomcat_version7: "7.0.109"
tomcat_version8: "8.5.73"
tomcat_version9: "9.0.55"

# The location where to download Apache Tomcat from.
tomcat_mirror: "https://archive.apache.org"

# If you want to download Tomcat from another location, adjust these parameters
# to your liking. For "normal" use, this does not require modification.
_tomcat_unarchive_urls:
  7:
    url: "{{ tomcat_mirror }}/dist/tomcat/tomcat-7/v{{ tomcat_version7 }}/bin/apache-tomcat-{{ tomcat_version7 }}.tar.gz"
  8:
    url: "{{ tomcat_mirror }}/dist/tomcat/tomcat-8/v{{ tomcat_version8 }}/bin/apache-tomcat-{{ tomcat_version8 }}.tar.gz"
  9:
    url: "{{ tomcat_mirror }}/dist/tomcat/tomcat-9/v{{ tomcat_version9 }}/bin/apache-tomcat-{{ tomcat_version9 }}.tar.gz"

tomcat_unarchive_url: "{{ _tomcat_unarchive_urls[tomcat_version].url }}"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-tomcat/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Ansible Molecule](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-core_dependencies.svg)](https://github.com/shadowwalker/ansible-role-core_dependencies)|
|[buluma.java](https://galaxy.ansible.com/buluma/java)|[![Ansible Molecule](https://github.com/buluma/ansible-role-java/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-java/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-java.svg)](https://github.com/shadowwalker/ansible-role-java)|
|[buluma.service](https://galaxy.ansible.com/buluma/service)|[![Ansible Molecule](https://github.com/buluma/ansible-role-service/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-service/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-service.svg)](https://github.com/shadowwalker/ansible-role-service)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-tomcat/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/repository/docker/buluma/enterpriselinux/general)|8|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|
|[Fedora](https://hub.docker.com/repository/docker/buluma/fedora/general)|all|
|[opensuse](https://hub.docker.com/repository/docker/buluma/opensuse/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-tomcat/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-tomcat/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-tomcat/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)


Template inspired by [Robert de Bock](https://github.com/robertdebock)
