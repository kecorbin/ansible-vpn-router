vpn-router
=========

Ansible role for terminating IPSec VPN on Cisco IOS routers

Requirements
------------

Any IOS device supporting IPSec

Role Variables
--------------

### Per Device Variables

|Variable|Default|Description|
|---|---|---|
| `crypto_map` | ANSIBLE_CRYPTO_MAP | The crypto map to manage
| `crypto_map_interface` | | interface where the crypto map will be applied
| `crypto_map_source_interface` | | source interface for ISAKMP/IPSec packets
| `ipsec_tunnels` | | List of IPSec tunnels to be configured on this device (see below)

### Per Tunnel Variables

|Variable|Description|
|---|---|
| `tunnel_name` |  Name for this tunnel, used to set descriptions and construct other descriptors e.g ACL's, transform sets, etc  
| `seq` | sequence number for this tunnel
| `peer_ip` | peer address
| `transform_encryption` |  encryption scheme used in transform set
| `transform_auth` | authentication scheme used in transform set
| `isakmp_encr` | isakmp encryption
| `isakmp_auth` | isakmp authentication
| `isakmp_key` | isakmp psk
| `acl_lines` | list of ACL entries for crypto proxy

Example inventory
-----------------

```

all:
  hosts:
    vpnrtr1:
      ansible_host: 10.94.241.230
      crypto_map: VPN
      crypto_map_interface: GigabitEthernet2
      crypto_map_source_interface: Loopback0

      ipsec_tunnels:

        - tunnel_name: headend
          seq: 20
          peer_ip: 172.16.252.0
          transform_encryption: esp-3des
          transform_auth: esp-md5-hmac
          isakmp_encr: aes
          isakmp_auth: pre-share
          isakmp_key: cisco
          acl_lines:
            - permit ip 192.168.1.0 0.0.0.255 192.168.0.0 0.0.0.255

```



Example Playbook
----------------

```
- name: Configure IPSec Tunnel
  hosts: vpnrtr1
  connection: local
  vars:
    cli:
      host: "{{ ansible_host }}"
  roles:
    - vpn-router
```

License
-------

BSD

Author Information
------------------

Kevin Corbin - kecorbin@cisco.com
