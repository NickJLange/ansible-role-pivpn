PiVPN
=========

This role install and configure OpenVPN in a Raspberry Pi with Raspbian.

Requirements
------------

This role requires Ansible 2.0 or higher and a clean installation of Raspbian. Eth0 must be configured with a static IP.

Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows.

([defaults/main.yml](defaults/main.yml))

```yaml
certificate:
  key_size: 1024 # If you are paranoid you can change for 2048
  key_country: "ES" # Country Name (2 letter code)
  key_province: "Seville" # State or Province Name (full name)
  key_city: "" # Locality Name (eg, city)
  key_org: "ACME Ltd." # Organization Name (eg, company)
  key_email: "" # Email Address
  key_ou: "" # Organizational Unit Name (eg, section)


openvpn:
  protocol: udp # UDP is recommended. You can change fot TCP.
  port: 1194 # This is the default OpenVPN port. Remember open this port in your router to allow the VPN connection from Internet.
  server_subnet: 10.8.0.0 # The subnet you want to use for the OpenVPN clients
  server_netmask: 255.255.255.0 # The netmask for the OpenVPN client subnet
  server_tun0: 10.8.0.1 # The IP for the OpenVPN tunnel interface
  server_tun0_ptp: 10.8.0.2 # The IP for the OpenVPN tunnel point-to-point alias
  local_subnet: 192.168.0.0 # The local subnet where the Raspberry Pi is connected
  local_netmask: 255.255.255.0 # The local netmask for the Raspberry Pi subnet
  dns_ip: 192.168.0.1 # If your router does not do DNS, you can use Google DNS 8.8.8.8

```

([defaults/credentials.yml](defaults/credentials.yml))

```yaml
# If you want to create an initial client, complete the variables
client:
  username: "" # OpenVPN client username
  password: "" # OpenVPN client password

```

Dependencies
------------

None

Example Playbook
----------------

If you encrypt the credentials.yml file, remember to run your playbook with the flag '--ask-vault-pass'.

    - hosts: pi
      role: pipoe2h.pivpn

License
-------

MIT

Author Information
------------------

* [Jose Gomez](https://github.com/pipoe2h) | [www](http://www.joseluisgomez.com) | [twitter](http://twitter.com/pipoe2h)
