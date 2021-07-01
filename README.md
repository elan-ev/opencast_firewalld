Ansible: Opencast Firewalld Role
================================

This Ansible role provides a simple firewalld configuration for Opencast.
The idea behind this set-up is to:

- Generally allow network communication within the cluster
- Allow communication via HTTP(S) from the outside world


Requirements
------------

This role uses [community.general.dig](https://docs.ansible.com/ansible/latest/collections/community/general/dig_lookup.html)
to look up the IP addresses for the given hostnames.
Make sure to have on your host system:

- dnspython
- [community.general collection](https://galaxy.ansible.com/community/general)


Role Variables
--------------

- `opencast_firewall_internal_hosts`
    - List of hosts between which to allow all network communication (default: `groups["all"]`)
- `opencast_firewall_http_hosts`
    - List of hosts to allow external HTTP(S) communications to (default: `groups["all"]`)
	 - Often makes sense to set this to something like `groups["opencast"]`
- `opencast_firewall_ipv4`
    - Look up IPv4 addresses of hostnames
- `opencast_firewall_ipv6`
    - Look up IPv6 addresses of hostnames


Example Playbook
----------------

Example of how to configure and use the role:

```yaml
- hosts: servers
  become: true
  roles:
    - role: lkiesow.opencast_firewalld
      opencast_firewall_http_hosts: '{{ groups["opencast"] }}'
```
