Role Name
=========

Install Unbound DNS Server on recursive mode.

Requirements
------------

Operational systems: Ubuntu 22.04.

Role Variables
--------------

unbound_forward_zone:
  - domain: DOMAIN_NAME
    fwd_addr:
      - 'IP_ADDR'
      - 'IP_ADDR'
unbound_access_control:
  - address: 'IP_ADDR/NETMASK'
    state: 'allow|deny|refuse'
unbound_control_enable: 'no|yes'
unbound_control_port: 'NUM_PORT'
unbound_control_interface: IP_ADDR
unbound_trusted_domains:
  - domain: DOMAIN_NAME



Dependencies
------------

NONE.

Example Playbook
----------------

---
- name: Deploy Unbound Server
  hosts: unbound
  become: true
  vars:
    unbound_forward_zone:
    - domain: .
      fwd_addr:
        - 8.8.8.8
        - 4.2.2.2
    - domain: fnet
      fwd_addr:
        - 10.0.33.2
        - 10.0.17.2
    unbound_access_control:
      - address: '0.0.0.0/0'
        state: 'allow'
      - address: '10.0.35.0/24'
        state: 'allow'
    unbound_control_enable: 'yes'
    unbound_control_port: 957
    unbound_control_interface: 0.0.0.0
    unbound_trusted_domains:
      - domain: internal
  roles:
    - bhaldur.unbound


License
-------

BSD

Author Information
------------------

GitHub: github.com/aledaltro
alexandredaltro2@gmail.com


