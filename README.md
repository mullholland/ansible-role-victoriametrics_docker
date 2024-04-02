# [Ansible role victoriametrics_docker](#victoriametrics_docker)

Installs and configures grafana container based on official grafana docker container

|GitHub|Downloads|Version|
|------|---------|-------|
|[![github](https://github.com/mullholland/ansible-role-victoriametrics_docker/actions/workflows/molecule.yml/badge.svg)](https://github.com/mullholland/ansible-role-victoriametrics_docker/actions/workflows/molecule.yml)|[![downloads](https://img.shields.io/ansible/role/d/mullholland/victoriametrics_docker)](https://galaxy.ansible.com/mullholland/victoriametrics_docker)|[![Version](https://img.shields.io/github/release/mullholland/ansible-role-victoriametrics_docker.svg)](https://github.com/mullholland/ansible-role-victoriametrics_docker/releases/)|
## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/mullholland/ansible-role-victoriametrics_docker/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true
  roles:
    - role: "mullholland.victoriametrics_docker"
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/mullholland/ansible-role-victoriametrics_docker/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: true
  vars:
    pip_packages:
      - "docker"

  roles:
    - role: mullholland.docker
    - role: mullholland.repository_epel
    - role: mullholland.pip
```



## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/mullholland/ansible-role-victoriametrics_docker/blob/master/defaults/main.yml):

```yaml
---
# General config
vm_docker_network_name: "web"
vm_docker_base_path: "/opt"
vm_docker_timezone: "Europe/Berlin"

# User/Group of the stack. Everything is mapped to this, instead of root.
vm_docker_user: "homelab"
vm_docker_uid: "900"
vm_docker_group: "homelab"
vm_docker_gid: "900"
vm_docker_user_system: true

# which container version to install
# https://hub.docker.com/r/grafana/grafana/tags
# can also be latest
vm_docker_version: "victoriametrics/victoria-metrics:latest"

vm_docker_commands:
  - "--storageDataPath=/storage"
  # - "--graphiteListenAddr=:2003"
  # - "--opentsdbListenAddr=:4242"
  - "--httpListenAddr=:8428"
  # - "--influxListenAddr=:8089"
  - "--vmalert.proxyURL=http://vmalert:8880"

vm_docker_environment_variables: []
vm_docker_volumes:
  - "{{ vm_docker_base_path }}/victoriametrics/data:/storage"

# which port to expose. can be empty
vm_docker_ports:
  - "8428:8428"
  # - "8089:8089"
  # - "8089:8089/udp"
  # - "2003:2003"
  # - "2003:2003/udp"
  # - "4242:4242"

vm_docker_labels:
  - "traefik.enable=false"
# - "traefik.enable=true"
# - "traefik.http.routers.grafana.entryPoints=https"
# - "traefik.http.routers.grafana.rule=Host(`grafana.example.com`)"
# - "traefik.http.routers.grafana.tls.certResolver=letsEncrypt"
# - "traefik.http.routers.grafana.tls=true"
#  - "traefik.http.routers.grafana.service=grafana"
#  - "traefik.http.routers.grafana.loadbalancer.server.port=80"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/mullholland/ansible-role-victoriametrics_docker/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[mullholland.repository_epel](https://galaxy.ansible.com/mullholland/repository_epel)|[![Build Status GitHub](https://github.com/mullholland/ansible-role-repository_epel/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-repository_epel/actions)|[![Build Status GitLab](https://gitlab.com/opensourceunicorn/ansible-role-repository_epel/badges/master/pipeline.svg)](https://gitlab.com/opensourceunicorn/ansible-role-repository_epel)|
|[mullholland.docker](https://galaxy.ansible.com/mullholland/docker)|[![Build Status GitHub](https://github.com/mullholland/ansible-role-docker/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-docker/actions)|[![Build Status GitLab](https://gitlab.com/opensourceunicorn/ansible-role-docker/badges/master/pipeline.svg)](https://gitlab.com/opensourceunicorn/ansible-role-docker)|
|[mullholland.pip](https://galaxy.ansible.com/mullholland/pip)|[![Build Status GitHub](https://github.com/mullholland/ansible-role-pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-pip/actions)|[![Build Status GitLab](https://gitlab.com/opensourceunicorn/ansible-role-pip/badges/master/pipeline.svg)](https://gitlab.com/opensourceunicorn/ansible-role-pip)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://mullholland.net) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/mullholland/ansible-role-victoriametrics_docker/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/mullholland/enterpriselinux)|all|
|[Fedora](https://hub.docker.com/r/mullholland/fedora/)|38, 39|
|[Ubuntu](https://hub.docker.com/r/mullholland/ubuntu)|all|
|[Debian](https://hub.docker.com/r/mullholland/debian)|all|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-victoriametrics_docker/issues).

## [License](#license)

[MIT](https://github.com/mullholland/ansible-role-victoriametrics_docker/blob/master/LICENSE).

## [Author Information](#author-information)

[mullholland](https://mullholland.net)
