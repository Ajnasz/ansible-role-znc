# znc

Role for ZNC IRC bouncer

## Role variables

```yml
znc_ssl_cert_content: NO CERTIFICATE

znc_exec_user: 
znc_exec_group: 

znc_config_path: "/home/{{ znc_exec_user }}/.znc"
znc_ssl_cert_path: "{{ znc_config_path }}/znc.pem"

znc_users: []
```

## Example configuration

```yml
---
znc_exec_user: znc
znc_exec_group: znc
znc_users:
  - name: foo
    nick: foo
    ident: foo
    admin: true
    realname: John Doe
    networks:
      - name: freenode
        server: "irc.freenode.net +6697 {{ znc_passwords.foo.networks.freenode }}"
        modules:
          - nickserv
          - simple_away
        chans:
          - #foobar
    passes:
      - hash: "{{ znc_passwords.foo.hash }}"
        method: "{{ znc_passwords.foo.method }}"
        salt: "{{ znc_passwords.foo.salt }}"

```
