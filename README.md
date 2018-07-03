# ansible-role-openssh

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-openssh.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-openssh)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-openssh-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/openssh)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](https://github.com/linuxhq/ansible-role-openssh/blob/master/COPYING)

RHEL/CentOS - OpenSSH SSH daemon

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    openssh_client:
      ForwardX11Trusted: true
      GSSAPIAuthentication: true
      SendEnv:
        - LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
        - LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
        - LC_IDENTIFICATION LC_ALL LANGUAGE
        - XMODIFIERS
    openssh_server:
      AcceptEnv:
        - LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
        - LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
        - LC_IDENTIFICATION LC_ALL LANGUAGE
        - XMODIFIERS
      AddressFamily: any
      ChallengeResponseAuthentication: false
      GSSAPIAuthentication: true
      GSSAPICleanupCredentials: false
      HostKey:
        - /etc/ssh/ssh_host_rsa_key
        - /etc/ssh/ssh_host_ecdsa_key
        - /etc/ssh/ssh_host_ed25519_key
      PasswordAuthentication: true
      PermitRootLogin: true
      Port: 22
      Protocol: 2
      Subsystem: 'sftp /usr/libexec/openssh/sftp-server'
      SyslogFacility: AUTHPRIV
      UsePAM: true
      UsePrivilegeSeparation: sandbox
      X11Forwarding: true
    openssh_server_autocreate_server_keys:
      - RSA
      - ECDSA
      - ED25519
    openssh_server_ssh_use_strong_rng: false


## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.openssh
          openssh_client:
            ForwardAgent: false
            ForwardX11Trusted: false
            GSSAPIAuthentication: false
            HashKnownHosts: true
          openssh_server:
            AllowAgentForwarding: false
            Ciphers: aes128-ctr,aes192-ctr,aes256-ctr
            HostbasedAuthentication: false
            HostKey:
              - /etc/ssh/ssh_host_rsa_key
              - /etc/ssh/ssh_host_ecdsa_key
              - /etc/ssh/ssh_host_ed25519_key
            MACs: hmac-sha2-256,hmac-sha2-512
            PasswordAuthentication: false
            PermitEmptyPasswords: false
            PermitRootLogin: false
            PermitUserEnvironment: false

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
