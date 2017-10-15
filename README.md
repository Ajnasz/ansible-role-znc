# znc

Role for ZNC IRC bouncer

## Role variables

```yml
znc_ssl_cert_path: /etc/ssl/private/znc.pem
znc_ssl_cert_content: NO CERTIFICATE
znc_config_path: /etc/znc.conf

znc_users: []

# vi:sw=2:tabstop=2
```

## Example configuration

```yml
---
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
          - #ajnasz
    passes:
      - hash: "{{ znc_passwords.foo.hash }}"
        method: "{{ znc_passwords.foo.method }}"
        salt: "{{ znc_passwords.foo.salt }}"

# vi:sw=2:tabstop=2:et:
```
