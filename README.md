# vpn_router

Ansible Role to terminate IPSec tunnel on Cisco IOS router.


## Usage

`ansible-galaxy install vpn_router`

LICENSE: 3-clause BSD license.


## Role Variables

```

ipsec_tunnels:

  - partner_name: router-id
    seq: 10
    peer_ip: 192.168.255.3
    transform_encryption: esp-3des
    transform_auth: esp-md5-hmac
    isakmp_encr: aes
    isakmp_auth: pre-share
    isakmp_key: cisco

```

## CONTRIBUTING

`git clone git@github.com:kecorbin/ansible-vpn-router`

---
Copyright © 2018, Kevin Corbin
