# Ansible Playbook to Setup PXE Server

The playbook can be used to setup PXE server completely. Before starting the playbook, make sure the ansible_client (PXE server) is ssh accessible from ansible controller (from where Ansible playbook is running)


## Variable to define for playbook (Few variables are pre-defined but it is advised to change the value based on environment). 

- Inventory File: **inventory/hosts**
  ```yaml
  - [ubuntu]
  - ubuntu-kickseed

  - [ubuntu:vars]
  - ansible_ssh_host=192.168.21.163
  - ansible_ssh_user=ubuntu
  - ansible_sudo_pass=root4me2```
  
- TFTP server variable: **roles/tftpserver/defaults/main.yml**
  ```yaml
  - tftp_username: tftp
  - tftp_root_directory: "/var/lib/tftpboot"
  - tftp_port: 69
  - tftp_options: "--secure"
  - tftp_daemon: "yes" ```
  
  
- DHCP server variables: **roles/dhcpserver/defaults/main.yml**
 ```yaml
  - dhcp_domain_name: example.org
  - dhcp_dns_server: ns1.example.org
  - dhcp_lease_time: 7200
  - dhcp_max_lease_time: 72000
  - dhcp_network_id: 192.168.21.0
  - dhcp_subnet_netmask: 255.255.255.0
  - dhcp_subnet_start_ip: 192.168.21.60
  - dhcp_subnet_end_ip: 192.168.21.70
  - dhcp_subnet_broadcat_ip: 192.168.21.255
  - dhcp_dns_server: 192.168.21.1
  - dhcp_subnet_gateway: 192.168.21.1 
  - host1_name: pxeclient1
  - host1_mac_address: 00:00:00:23:34:6a
  - host1_ip_address: 192.168.21.61
  - host2_name: pxeclient1
  - host2_mac_address: 00:00:00:23:44:6a
  - host2_ip_address: 192.168.21.62 
```
 
- PXE server variables: **roles/pxeserver/defaults/main.yml**
  ```yaml
  - ubuntu_version_name: bionic
  - apache_mirror_server: 192.168.21.163```
  
  
# To run the playbook
```shell
# ansible-playbook -i inventory/hosts  playbooks/setup-pxeserver.yml
```
