# ansible-role-auter

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-auter.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-auter)

RHEL/CentOS - Automatic updates for RHEL, CentOS or Fedora Linux servers

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    auter_auto_reboot: False
    auter_config_set: default
    auter_max_delay: 3600
    auter_only_install_from_prep: False
    auter_package_manager_options: ''
    auter_pre_download_updates: True

Additional variables not defined by default

    auter_cronjobs:
      - name: Pre-download updates before applying
        job: /usr/bin/auter --prep
        minute: 0
        hour: 05
        weekday: '*'
        day: '*'
        month: '*'
      - name: Apply updates, and reboot if AUTOREBOOT=yes
        job: /usr/bin/auter --apply
        minute: 0
        hour: 06
        weekday: '*'
        day: '*'
        month: '*'

    auter_scripts:
      pre_apply:
        path: /etc/auter/pre-apply.d
        scripts:
          - name: pre_apply.sh
            mode: '0755'
            base64: |
              ZWNobyBwcmVfYXBwbHkK
      post_apply:
        path: /etc/auter/post-apply.d
        scripts:
          - name: post_apply.sh
            mode: '0755'
            base64: |
              ZWNobyBwb3N0X2FwcGx5Cg==

## Dependencies

 * https://galaxy.ansible.com/linuxhq/epel/
 
## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.auter
          auter_only_install_from_prep: True
          auter_cronjobs:
            - name: Apply updates, and reboot if AUTOREBOOT=yes
              job: /usr/bin/auter --apply
              minute: 0
              hour: 06
              weekday: '*'
              day: '*'
              month: '*'

## License

BSD

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
