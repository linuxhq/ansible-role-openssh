# ansible-role-openssh

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-openssh.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-openssh)

RHEL/CentOS - OpenSSH SSH daemon

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    openssh_auth: []

    openssh_client:
      default:
        ForwardX11Trusted: yes
        GSSAPIAuthentication: yes
        SendEnv:
          - LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
          - LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
          - LC_IDENTIFICATION LC_ALL LANGUAGE
          - XMODIFIERS

    openssh_server:
      default:
        AcceptEnv:
          - LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
          - LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
          - LC_IDENTIFICATION LC_ALL LANGUAGE
          - XMODIFIERS
        AddressFamily: any
        ChallengeResponseAuthentication: no
        GSSAPIAuthentication: yes
        GSSAPICleanupCredentials: no
        HostKey:
          - /etc/ssh/ssh_host_rsa_key
          - /etc/ssh/ssh_host_ecdsa_key
          - /etc/ssh/ssh_host_ed25519_key
        PasswordAuthentication: yes
        PermitRootLogin: yes
        Port: 22
        Protocol: 2
        Subsystem: 'sftp /usr/libexec/openssh/sftp-server'
        SyslogFacility: AUTHPRIV
        UsePAM: yes
        UsePrivilegeSeparation: sandbox
        X11Forwarding: yes

You can add host specific configs to ssh_config by doing the following:

    openssh_client:
      default:
        DefaultOption1: DefaultValue1
        DefaultOption2: DefaultValue2
      github_com:
        GithubOption1: GithubValue1
        GithubOption2: GithubValue2

You can match specific users in sshd_config by doing the following:

    openssh_server:
      default:
        DefaultOption1: DefaultValue1
        DefaultOption2: DefaultValue2
      username:
        UsernameOption1: UsernameValue1
        UsernameOption2: UsernameValue2
      
## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.openssh
          openssh_auth:
            - name: root
              exclusive: yes
              key_options: []
              shell: /sbin/nologin
              uid: 0
            - name: tkimball
              exclusive: yes
              group: wheel
              key: ssh-rsa {...}
              key_options: []
              password: {...}
              uid: 1000
          openssh_client:
            default:
              ForwardAgent: no
              ForwardX11Trusted: no
              GSSAPIAuthentication: no
              HashKnownHosts: yes
          openssh_server:
            default:
              AllowAgentForwarding: no
              Ciphers: aes128-ctr,aes192-ctr,aes256-ctr
              HostbasedAuthentication: no
              HostKey:
                - /etc/ssh/ssh_host_rsa_key
                - /etc/ssh/ssh_host_ecdsa_key
                - /etc/ssh/ssh_host_ed25519_key
              MACs: hmac-sha2-256,hmac-sha2-512
              PasswordAuthentication: no
              PermitEmptyPasswords: no
              PermitRootLogin: no
              PermitUserEnvironment: no

## License

GPLv3

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
