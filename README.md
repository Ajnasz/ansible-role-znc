# znc

Role for ZNC IRC bouncer

## Role variables

```yml
znc_ssl_cert_content: NO CERTIFICATE

znc_owner: 
znc_group: 

znc_config_path: "/home/{{ znc_exec_user }}/.znc"
znc_ssl_cert_path: "{{ znc_config_path }}/znc.pem"

znc_users: []
```

## Example configuration

```yml
znc_owner: znc
znc_group: znc

znc_users:
  - name: "foo"
    nick: "foo"
    ident: "foo"
    admin: true
    realname: "John Doe"
    networks:
      - name: bitlbee
        server: "im.bitlbee.org 6667 {{ znc_passwords.foo.networks.bitlbee.password }}"
      - name: freenode
        server: "irc.freenode.net +6697"
        modules:
          - nickserv
          - simple_away
          - cert
          - sasl
        chans:
          - "#foo"
          - "#bar"

    passes:
      - hash: "{{znc_passwords.foo.hash}}"
        method: "{{znc_passwords.foo.method}}"
        salt: "{{znc_passwords.foo.salt}}"
```

Into vault encrypted file:
```yml
znc_passwords:
  userone:
    hash: ""
    method: "SHA256"
    salt: ""
    networks:
      bitlbee:
        password: ""
		cert_pem: |
		  ...

znc_ssl_cert_content: \
 ...
```
