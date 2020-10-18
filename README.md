ansible-role-openwrt-setup
==========================

An ansible role that sets up OpenWrt routers. Python NOT requried on OpenWrt routers.

Requirements
------------

None.

Role Variables
--------------

| variable      | Note
| ------------- | ----
| **System**
| `zonename`    | Examples: `UTC`, `America/Los Angeles`, `Asia/Hong Kong`. <br> Check all available timezones at <http://openwrt.lan/cgi-bin/luci/admin/system/system>
| **Dropbear**
| `ssh_port` | SSH port
| `ssh_public_key` | SSH public key allowed for passwordless SSH login. <br> **Note:** When a key is added, password authentication for SSH will be disabled.
| **Root/LuCI Password**
| `passwd` | The root password used for command line and LuCI.
| **Wireless** | Wireless variables apply to both 2.4G and 5G
| `ssid` | Wi-Fi Name
| `key` | Wi-Fi Password
| `encryption` | `sae`, `sae-mixed`, `psk2`, `psk-mixed`, `psk`, `wpa`, `none`
| `channel` | `auto` or channel number
| **Network**
| `ipaddr` | LAN IPv4 address
| `netmask` | LAN IPv4 netmask
| `ipv6_disabled` | Whether to disable IPv6

**Note:** All variables are undefined by default. Unless a variable is set, no related tasks will be carried out.


Dependencies
------------

This role depends on the [`gekmihesg.openwrt`](https://github.com/gekmihesg/ansible-openwrt) ansible role, so that python on OpenWrt becomes a non-requirement.

Example Inventory
----------------

**Note:** All OpenWrt hosts must be put under `openwrt` group.

```
[openwrt]
openwrt.lan
```

Example Playbook
----------------

```yml
- hosts: openwrt
  remote_user: root
  roles:
    - name: bit_kitchen.openwrt_setup
      # System
      zonename: "America/Los Angeles"

      # Dropbear
      ssh_port: 2222
      ssh_public_key: "ssh-rsa AAAAB3Nz...4Fq/k="

      # Root/LuCI Password
      passwd: "MySecretP@ss!"

      # Wireless
      ssid: "OpenWrt"
      key: "MyWiFiMyPass"
      encryption: psk2
      channel: auto

      # Network
      ipaddr: 10.20.30.1
      netmask: 255.255.255.0
```

License
-------

[MIT](LICENSE)

Author Information
------------------

[bit.kitchen](https://github.com/bit-kitchen)
