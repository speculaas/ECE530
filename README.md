# ECE530 HW1-report

Name: Yie-Sheng Chen
ID: 101944761
e-mail: tallpik3@unm.edu

## Abstract

## Description of the format and some details of the report
* About deployment details: the commands and their console outputs are listed in monospaced sections. And below the commands and outputs are comments, observation and references.
* About the screenshots: there are two type of console screenshots. One is of the physical thinkpad machine. Another is of ssh terminal of MacOS.

## Troubleshooting processes
* initial login to mariadb failed
* cannot connect to db


# ECE530 HW1-report - checklist
## Keystone:
1. Generate	token
2. Create	demo and	admin	user
3. Retrieve	user	list
4. Retrieve	role	list

```
# . admin-openrc
# openstack token issue
/usr/lib/python3/dist-packages/secretstorage/dhcrypto.py:15: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/secretstorage/util.py:19: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field      | Value                                                                                                                                                                                   |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| expires    | 2023-04-12T03:10:43+0000                                                                                                                                                                |
| id         | gAAAAABkNhMj7uTybQveNQwUfsVkeyqL8TvJhMO7_YspXrITefZCky29w_nURxRaav_Wv87V0ES9j0zrGeX9E97svGOLDXYLV68huNfX2mP7sKzp-bC3K9yVzwJOxmO4RpLZqNIYX4IhETZys61A68nHT0p0xgI9olPO4BFuplPVvjFXlE69aYI |
| project_id | dd1bd9e23e7440f0ab943dedfb5aefbc                                                                                                                                                        |
| user_id    | b08a3a4ea5cb474f893835ce0c0722ae                                                                                                                                                        |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

# openstack user create --domain default --password-prompt demo
/usr/lib/python3/dist-packages/secretstorage/dhcrypto.py:15: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/secretstorage/util.py:19: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
User Password:
Repeat User Password:
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| enabled             | True                             |
| id                  | cc7498b106314a3abc45045f96dedfef |
| name                | demo                             |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+


# openstack user list
/usr/lib/python3/dist-packages/secretstorage/dhcrypto.py:15: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/secretstorage/util.py:19: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
+----------------------------------+-----------+
| ID                               | Name      |
+----------------------------------+-----------+
| b08a3a4ea5cb474f893835ce0c0722ae | admin     |
| e2e915e124c24ff9adf94966a856d5ec | myuser    |
| 19a1a5467888435ea3b272824109caea | glance    |
| e7119b9a9b124ac4863058380142146f | placement |
| 13b30c88746640d3ab77930a175858b7 | nova      |
| 87ab44f576024fe7ba7c2a8719c1af10 | neutron   |
| f057d7c5f56048719de673c47f902f34 | cinder    |
+----------------------------------+-----------+

# openstack role list
/usr/lib/python3/dist-packages/secretstorage/dhcrypto.py:15: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/secretstorage/util.py:19: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
+----------------------------------+--------+
| ID                               | Name   |
+----------------------------------+--------+
| 0bab649ade9440e09d245452a2f4f532 | reader |
| 1ed58e4603dd49b3a4dfdd9f3892a9d5 | member |
| 4c05f47a9be943afadb36621570cf348 | admin  |
| ccf8a8e9ee0c45f0b3520225ac6f1ade | myrole |
+----------------------------------+--------+
```
![](https://i.imgur.com/wewWSog.png)

![](https://i.imgur.com/FnWJE7N.png)

![](https://i.imgur.com/Jj64Zso.png)

![](https://i.imgur.com/V701utJ.png)



## Glance:
1. Import	Cirros	OS	image
2. Retrieve	image	list

```
# openstack image create CIRROS_IMAGE --disk-format qcow2 --file cirros-0.4.0-x86_64-disk.img 
+------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
| Field            | Value                                                                                                                                            |
+------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
| container_format | bare                                                                                                                                             |
| created_at       | 2023-04-12T02:33:05Z                                                                                                                             |
| disk_format      | qcow2                                                                                                                                            |
| file             | /v2/images/d2b08ca8-6b09-406b-86a1-ef3dd2aff0ca/file                                                                                             |
| id               | d2b08ca8-6b09-406b-86a1-ef3dd2aff0ca                                                                                                             |
| min_disk         | 0                                                                                                                                                |
| min_ram          | 0                                                                                                                                                |
| name             | CIRROS_IMAGE                                                                                                                                     |
| owner            | dd1bd9e23e7440f0ab943dedfb5aefbc                                                                                                                 |
| properties       | os_hidden='False', owner_specified.openstack.md5='', owner_specified.openstack.object='images/CIRROS_IMAGE', owner_specified.openstack.sha256='' |
| protected        | False                                                                                                                                            |
| schema           | /v2/schemas/image                                                                                                                                |
| status           | queued                                                                                                                                           |
| tags             |                                                                                                                                                  |
| updated_at       | 2023-04-12T02:33:05Z                                                                                                                             |
| visibility       | shared                                                                                                                                           |
+------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+


# openstack image list

+--------------------------------------+-----------------------+--------+
| ID                                   | Name                  | Status |
+--------------------------------------+-----------------------+--------+
| d2b08ca8-6b09-406b-86a1-ef3dd2aff0ca | CIRROS_IMAGE          | active |
| cbec07a3-9360-4662-8ea5-7c8c2f2f71bc | COOKBOOK_UBUNTU_IMAGE | active |
| d6fc5ad0-4076-4cc3-83b3-33ef4a8efecd | cirros                | active |
+--------------------------------------+-----------------------+--------+

```
![](https://i.imgur.com/M2Z1o1U.png)

![](https://i.imgur.com/VU4JtcZ.png)

* OpenStack Cloud Computing Cookbook 4th ed. 2018
  * openstack image list


## Nova:
1. Retrieve	VM	list
2. Create	a	VM
3. Login	in	VM

```
# openstack subnet show provider
+----------------------+--------------------------------------+
| Field                | Value                                |
+----------------------+--------------------------------------+
| allocation_pools     | 203.0.113.101-203.0.113.250          |
| cidr                 | 203.0.113.0/24                       |
| created_at           | 2023-04-12T03:24:03Z                 |
| description          |                                      |
| dns_nameservers      | 8.8.4.4                              |
| dns_publish_fixed_ip | None                                 |
| enable_dhcp          | True                                 |
| gateway_ip           | 203.0.113.1                          |
| host_routes          |                                      |
| id                   | b30131cc-c9f0-4aa2-92e5-964574271de8 |
| ip_version           | 4                                    |
| ipv6_address_mode    | None                                 |
| ipv6_ra_mode         | None                                 |
| name                 | provider                             |
| network_id           | 6f3497ee-0a0a-4256-9db4-0f2a804fea74 |
| project_id           | dd1bd9e23e7440f0ab943dedfb5aefbc     |
| revision_number      | 0                                    |
| segment_id           | None                                 |
| service_types        |                                      |
| subnetpool_id        | None                                 |
| tags                 |                                      |
| updated_at           | 2023-04-12T03:24:03Z                 |
+----------------------+--------------------------------------+
# cat /etc/resolv.conf | grep -e nameserver
nameserver 127.0.0.53
# openstack subnet create --network selfservice \
>   --dns-nameserver 127.0.0.53 --gateway 203.0.113.1 \
>   --subnet-range 172.16.1.0/24 selfservice
+----------------------+--------------------------------------+
| Field                | Value                                |
+----------------------+--------------------------------------+
| allocation_pools     | 172.16.1.1-172.16.1.254              |
| cidr                 | 172.16.1.0/24                        |
| created_at           | 2023-04-12T04:19:19Z                 |
| description          |                                      |
| dns_nameservers      | 127.0.0.53                           |
| dns_publish_fixed_ip | None                                 |
| enable_dhcp          | True                                 |
| gateway_ip           | 203.0.113.1                          |
| host_routes          |                                      |
| id                   | f0420b0f-f9cd-4fd0-9374-e0dcd3ffc38f |
| ip_version           | 4                                    |
| ipv6_address_mode    | None                                 |
| ipv6_ra_mode         | None                                 |
| name                 | selfservice                          |
| network_id           | a6cc384b-efe4-408e-b713-927397416e53 |
| project_id           | 7926c5914b78451d9faff81ba6791d61     |
| revision_number      | 0                                    |
| segment_id           | None                                 |
| service_types        |                                      |
| subnetpool_id        | None                                 |
| tags                 |                                      |
| updated_at           | 2023-04-12T04:19:19Z                 |
+----------------------+--------------------------------------+
# . demo-openrc
# openstack router create router
+-------------------------+--------------------------------------+
| Field                   | Value                                |
+-------------------------+--------------------------------------+
| admin_state_up          | UP                                   |
| availability_zone_hints |                                      |
| availability_zones      |                                      |
| created_at              | 2023-04-12T04:19:57Z                 |
| description             |                                      |
| external_gateway_info   | null                                 |
| flavor_id               | None                                 |
| id                      | 1d43ac10-1a1b-4815-95bf-2f57b8b51cde |
| name                    | router                               |
| project_id              | 7926c5914b78451d9faff81ba6791d61     |
| revision_number         | 1                                    |
| routes                  |                                      |
| status                  | ACTIVE                               |
| tags                    |                                      |
| updated_at              | 2023-04-12T04:19:57Z                 |
+-------------------------+--------------------------------------+
# openstack flavor create --id 0 --vcpus 1 --ram 64 --disk 1 m1.nano
+----------------------------+---------+
| Field                      | Value   |
+----------------------------+---------+
| OS-FLV-DISABLED:disabled   | False   |
| OS-FLV-EXT-DATA:ephemeral  | 0       |
| description                | None    |
| disk                       | 1       |
| id                         | 0       |
| name                       | m1.nano |
| os-flavor-access:is_public | True    |
| properties                 |         |
| ram                        | 64      |
| rxtx_factor                | 1.0     |
| swap                       |         |
| vcpus                      | 1       |
+----------------------------+---------+
# . demo-openrc
# ssh-keygen -q -N ""
# openstack keypair create --public-key ~/.ssh/id_rsa.pub mykey
+-------------+-------------------------------------------------+
| Field       | Value                                           |
+-------------+-------------------------------------------------+
| created_at  | None                                            |
| fingerprint | cd:f6:d9:f5:c4:7b:51:57:7a:72:69:4c:7f:2a:97:ae |
| id          | mykey                                           |
| is_deleted  | None                                            |
| name        | mykey                                           |
| type        | ssh                                             |
| user_id     | e2e915e124c24ff9adf94966a856d5ec                |
+-------------+-------------------------------------------------+
# openstack keypair list
+-------+-------------------------------------------------+------+
| Name  | Fingerprint                                     | Type |
+-------+-------------------------------------------------+------+
| mykey | cd:f6:d9:f5:c4:7b:51:57:7a:72:69:4c:7f:2a:97:ae | ssh  |
+-------+-------------------------------------------------+------+
# openstack security group rule create --proto icmp default
+-------------------------+--------------------------------------+
| Field                   | Value                                |
+-------------------------+--------------------------------------+
| created_at              | 2023-04-12T04:27:35Z                 |
| description             |                                      |
| direction               | ingress                              |
| ether_type              | IPv4                                 |
| id                      | a0bbabdc-7c82-4e81-9e9a-e6a889ae9cf2 |
| name                    | None                                 |
| port_range_max          | None                                 |
| port_range_min          | None                                 |
| project_id              | 7926c5914b78451d9faff81ba6791d61     |
| protocol                | icmp                                 |
| remote_address_group_id | None                                 |
| remote_group_id         | None                                 |
| remote_ip_prefix        | 0.0.0.0/0                            |
| revision_number         | 0                                    |
| security_group_id       | 0e78add4-28d0-4d3e-b88c-71244cc8f174 |
| tags                    | []                                   |
| tenant_id               | 7926c5914b78451d9faff81ba6791d61     |
| updated_at              | 2023-04-12T04:27:35Z                 |
+-------------------------+--------------------------------------+
# openstack security group rule create --proto tcp --dst-port 22 default
+-------------------------+--------------------------------------+
| Field                   | Value                                |
+-------------------------+--------------------------------------+
| created_at              | 2023-04-12T04:28:02Z                 |
| description             |                                      |
| direction               | ingress                              |
| ether_type              | IPv4                                 |
| id                      | 0674d74a-d8f3-48a8-b739-0beca26bd804 |
| name                    | None                                 |
| port_range_max          | 22                                   |
| port_range_min          | 22                                   |
| project_id              | 7926c5914b78451d9faff81ba6791d61     |
| protocol                | tcp                                  |
| remote_address_group_id | None                                 |
| remote_group_id         | None                                 |
| remote_ip_prefix        | 0.0.0.0/0                            |
| revision_number         | 0                                    |
| security_group_id       | 0e78add4-28d0-4d3e-b88c-71244cc8f174 |
| tags                    | []                                   |
| tenant_id               | 7926c5914b78451d9faff81ba6791d61     |
| updated_at              | 2023-04-12T04:28:02Z                 |
+-------------------------+--------------------------------------+
```
* https://docs.openstack.org/neutron/queens/admin/deploy-ovs-selfservice.html

```
# openstack flavor list
+----+---------+-----+------+-----------+-------+-----------+
| ID | Name    | RAM | Disk | Ephemeral | VCPUs | Is Public |
+----+---------+-----+------+-----------+-------+-----------+
| 0  | m1.nano |  64 |    1 |         0 |     1 | True      |
+----+---------+-----+------+-----------+-------+-----------+
# openstack image list
+--------------------------------------+--------+--------+
| ID                                   | Name   | Status |
+--------------------------------------+--------+--------+
| d6fc5ad0-4076-4cc3-83b3-33ef4a8efecd | cirros | active |
+--------------------------------------+--------+--------+
```
* https://docs.openstack.org/install-guide/launch-instance-selfservice.html
* 
```
# openstack network list
+--------------------------------------+-------------+--------------------------------------+
| ID                                   | Name        | Subnets                              |
+--------------------------------------+-------------+--------------------------------------+
| 6f3497ee-0a0a-4256-9db4-0f2a804fea74 | provider    | b30131cc-c9f0-4aa2-92e5-964574271de8 |
| a6cc384b-efe4-408e-b713-927397416e53 | selfservice | f0420b0f-f9cd-4fd0-9374-e0dcd3ffc38f |
+--------------------------------------+-------------+--------------------------------------+
# openstack security group list
+--------------------------------------+---------+------------------------+----------------------------------+------+
| ID                                   | Name    | Description            | Project                          | Tags |
+--------------------------------------+---------+------------------------+----------------------------------+------+
| 0e78add4-28d0-4d3e-b88c-71244cc8f174 | default | Default security group | 7926c5914b78451d9faff81ba6791d61 | []   |
+--------------------------------------+---------+------------------------+----------------------------------+------+
# openstack server create --flavor m1.nano --image cirros \
>   --nic net-id=a6cc384b-efe4-408e-b713-927397416e53 --security-group default \
>   --key-name mykey selfservice-instance
+-----------------------------+-----------------------------------------------+
| Field                       | Value                                         |
+-----------------------------+-----------------------------------------------+
| OS-DCF:diskConfig           | MANUAL                                        |
| OS-EXT-AZ:availability_zone |                                               |
| OS-EXT-STS:power_state      | NOSTATE                                       |
| OS-EXT-STS:task_state       | scheduling                                    |
| OS-EXT-STS:vm_state         | building                                      |
| OS-SRV-USG:launched_at      | None                                          |
| OS-SRV-USG:terminated_at    | None                                          |
| accessIPv4                  |                                               |
| accessIPv6                  |                                               |
| addresses                   |                                               |
| adminPass                   | m8hMeEtEb8dL                                  |
| config_drive                |                                               |
| created                     | 2023-04-12T04:33:05Z                          |
| flavor                      | m1.nano (0)                                   |
| hostId                      |                                               |
| id                          | 70b5c231-a7a9-4b77-8367-6b0e42007505          |
| image                       | cirros (d6fc5ad0-4076-4cc3-83b3-33ef4a8efecd) |
| key_name                    | mykey                                         |
| name                        | selfservice-instance                          |
| progress                    | 0                                             |
| project_id                  | 7926c5914b78451d9faff81ba6791d61              |
| properties                  |                                               |
| security_groups             | name='0e78add4-28d0-4d3e-b88c-71244cc8f174'   |
| status                      | BUILD                                         |
| updated                     | 2023-04-12T04:33:05Z                          |
| user_id                     | e2e915e124c24ff9adf94966a856d5ec              |
| volumes_attached            |                                               |
+-----------------------------+-----------------------------------------------+
# openstack server list
+--------------------------------------+----------------------+--------+-------------------------+--------+---------+
| ID                                   | Name                 | Status | Networks                | Image  | Flavor  |
+--------------------------------------+----------------------+--------+-------------------------+--------+---------+
| 70b5c231-a7a9-4b77-8367-6b0e42007505 | selfservice-instance | ACTIVE | selfservice=172.16.1.64 | cirros | m1.nano |
+--------------------------------------+----------------------+--------+-------------------------+--------+---------+
# openstack console url show selfservice-instance
+----------+-------------------------------------------------------------------------------------------+
| Field    | Value                                                                                     |
+----------+-------------------------------------------------------------------------------------------+
| protocol | vnc                                                                                       |
| type     | novnc                                                                                     |
| url      | http://controller:6080/vnc_auto.html?path=%3Ftoken%3D36cab490-8236-4af6-aa9c-74f67874e31e |
+----------+-------------------------------------------------------------------------------------------+
# openstack floating ip create provider
+---------------------+--------------------------------------+
| Field               | Value                                |
+---------------------+--------------------------------------+
| created_at          | 2023-04-12T04:35:00Z                 |
| description         |                                      |
| dns_domain          | None                                 |
| dns_name            | None                                 |
| fixed_ip_address    | None                                 |
| floating_ip_address | 203.0.113.102                        |
| floating_network_id | 6f3497ee-0a0a-4256-9db4-0f2a804fea74 |
| id                  | 2f0d2ffd-ed1a-414d-8bb9-603cde946daf |
| name                | 203.0.113.102                        |
| port_details        | None                                 |
| port_id             | None                                 |
| project_id          | 7926c5914b78451d9faff81ba6791d61     |
| qos_policy_id       | None                                 |
| revision_number     | 0                                    |
| router_id           | None                                 |
| status              | DOWN                                 |
| subnet_id           | None                                 |
| tags                | []                                   |
| updated_at          | 2023-04-12T04:35:00Z                 |
+---------------------+--------------------------------------+
```
* https://docs.openstack.org/install-guide/launch-instance-selfservice.html

## Neutron:
1. Create	a	Network

```
# openstack network create COOKBOOK_PROVIDER_NET \
> --provider-network-type vlan \
> --provider-physical-network vlan \
> --provider-segment 200
Error while executing command: BadRequestException: 400, Invalid input for operation: physical_network 'vlan' unknown for VLAN provider network.

# openstack network create  --share --external \
>   --provider-physical-network provider \
>   --provider-network-type flat provider
+---------------------------+--------------------------------------+
| Field                     | Value                                |
+---------------------------+--------------------------------------+
| admin_state_up            | UP                                   |
| availability_zone_hints   |                                      |
| availability_zones        |                                      |
| created_at                | 2023-04-12T03:10:37Z                 |
| description               |                                      |
| dns_domain                | None                                 |
| id                        | 6f3497ee-0a0a-4256-9db4-0f2a804fea74 |
| ipv4_address_scope        | None                                 |
| ipv6_address_scope        | None                                 |
| is_default                | False                                |
| is_vlan_transparent       | None                                 |
| mtu                       | 1500                                 |
| name                      | provider                             |
| port_security_enabled     | True                                 |
| project_id                | dd1bd9e23e7440f0ab943dedfb5aefbc     |
| provider:network_type     | flat                                 |
| provider:physical_network | provider                             |
| provider:segmentation_id  | None                                 |
| qos_policy_id             | None                                 |
| revision_number           | 1                                    |
| router:external           | External                             |
| segments                  | None                                 |
| shared                    | True                                 |
| status                    | ACTIVE                               |
| subnets                   |                                      |
| tags                      |                                      |
| updated_at                | 2023-04-12T03:10:37Z                 |
+---------------------------+--------------------------------------+

# cat /etc/neutron/plugins/ml2/linuxbridge_agent.ini | grep -n -e "\[linux_bridge" -A 2
189:[linux_bridge]
190-physical_interface_mappings = provider:eth2


# openstack subnet create --network provider \
>   --allocation-pool start=203.0.113.101,end=203.0.113.250 \
>   --dns-nameserver 8.8.4.4 --gateway 203.0.113.1 \
>   --subnet-range 203.0.113.0/24 provider
+----------------------+--------------------------------------+
| Field                | Value                                |
+----------------------+--------------------------------------+
| allocation_pools     | 203.0.113.101-203.0.113.250          |
| cidr                 | 203.0.113.0/24                       |
| created_at           | 2023-04-12T03:24:03Z                 |
| description          |                                      |
| dns_nameservers      | 8.8.4.4                              |
| dns_publish_fixed_ip | None                                 |
| enable_dhcp          | True                                 |
| gateway_ip           | 203.0.113.1                          |
| host_routes          |                                      |
| id                   | b30131cc-c9f0-4aa2-92e5-964574271de8 |
| ip_version           | 4                                    |
| ipv6_address_mode    | None                                 |
| ipv6_ra_mode         | None                                 |
| name                 | provider                             |
| network_id           | 6f3497ee-0a0a-4256-9db4-0f2a804fea74 |
| project_id           | dd1bd9e23e7440f0ab943dedfb5aefbc     |
| revision_number      | 0                                    |
| segment_id           | None                                 |
| service_types        |                                      |
| subnetpool_id        | None                                 |
| tags                 |                                      |
| updated_at           | 2023-04-12T03:24:03Z                 |
+----------------------+--------------------------------------+

```
![](https://i.imgur.com/Zn8QNYk.png)

* OpenStack Cloud Computing Cookbook 4th ed. 2018
  * openstack network create COOKBOOK_PROVIDER_NET --provider-network-type vlan --provider-physical-network vlan --provider-segment 200
* https://docs.openstack.org/newton/install-guide-rdo/launch-instance-networks-provider.html
  * openstack network create  --share --external   --provider-physical-network provider   --provider-network-type flat provider
* https://docs.openstack.org/newton/install-guide-rdo/launch-instance.html
  * If you chose option 2, create the provider and self-service networks.
* https://docs.openstack.org/neutron/yoga/install/ovn/manual_install.html


## Horizon:
1. Login	with	proper	account
2. Retrieve	service	information

![](https://i.imgur.com/PSupb8O.png)

![](https://i.imgur.com/xYKCmR9.png)
```
```


## Cinder:
1. Create	a	volume
2. Retrieve	volume	list

```
# openstack image list
+--------------------------------------+-----------------------+--------+
| ID                                   | Name                  | Status |
+--------------------------------------+-----------------------+--------+
| d2b08ca8-6b09-406b-86a1-ef3dd2aff0ca | CIRROS_IMAGE          | active |
| cbec07a3-9360-4662-8ea5-7c8c2f2f71bc | COOKBOOK_UBUNTU_IMAGE | active |
| d6fc5ad0-4076-4cc3-83b3-33ef4a8efecd | cirros                | active |
+--------------------------------------+-----------------------+--------+
# openstack availability zone list
+-----------+-------------+
| Zone Name | Zone Status |
+-----------+-------------+
| internal  | available   |
| nova      | available   |
| nova      | available   |
| nova      | available   |
| nova      | available   |
+-----------+-------------+
# openstack volume create --image d2b08ca8-6b09-406b-86a1-ef3dd2aff0ca  --size 8 --availability-zone nova my-new-volume
+---------------------+--------------------------------------+
| Field               | Value                                |
+---------------------+--------------------------------------+
| attachments         | []                                   |
| availability_zone   | nova                                 |
| bootable            | false                                |
| consistencygroup_id | None                                 |
| created_at          | 2023-04-12T04:57:33.158574           |
| description         | None                                 |
| encrypted           | False                                |
| id                  | ffa3bb99-5c15-49e6-9a29-dcfaac771ff2 |
| migration_status    | None                                 |
| multiattach         | False                                |
| name                | my-new-volume                        |
| properties          |                                      |
| replication_status  | None                                 |
| size                | 8                                    |
| snapshot_id         | None                                 |
| source_volid        | None                                 |
| status              | creating                             |
| type                | __DEFAULT__                          |
| updated_at          | None                                 |
| user_id             | b08a3a4ea5cb474f893835ce0c0722ae     |
+---------------------+--------------------------------------+

# openstack volume list
+--------------------------------------+---------------+-----------+------+-------------+
| ID                                   | Name          | Status    | Size | Attached to |
+--------------------------------------+---------------+-----------+------+-------------+
| ffa3bb99-5c15-49e6-9a29-dcfaac771ff2 | my-new-volume | available |    8 |             |
+--------------------------------------+---------------+-----------+------+-------------+
```
![](https://i.imgur.com/IMY1LJu.png)
* https://docs.openstack.org/cinder/latest/cli/cli-manage-volumes.html
* 

## Swift:
1. Create	a	container
2. Upload	and	download	file

```
```


## Extra	Point:
1. Create	a	VM	with	public	network	connected
2. Import	and	create	VM	with	Ubuntu	image	(inside	OpenStack)
3. Attach	volume	to	a	VM
4. Install	one	extra	service	(Ceilometer,	Heat	etc.)

```
# wget https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-disk1.img
# openstack image create COOKBOOK_UBUNTU_IMAGE --disk-format qcow2 --file xenial-server-cloudimg-amd64-disk1.img 
+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field            | Value                                                                                                                                                     |
+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
| container_format | bare                                                                                                                                                      |
| created_at       | 2023-04-12T02:30:32Z                                                                                                                                      |
| disk_format      | qcow2                                                                                                                                                     |
| file             | /v2/images/cbec07a3-9360-4662-8ea5-7c8c2f2f71bc/file                                                                                                      |
| id               | cbec07a3-9360-4662-8ea5-7c8c2f2f71bc                                                                                                                      |
| min_disk         | 0                                                                                                                                                         |
| min_ram          | 0                                                                                                                                                         |
| name             | COOKBOOK_UBUNTU_IMAGE                                                                                                                                     |
| owner            | dd1bd9e23e7440f0ab943dedfb5aefbc                                                                                                                          |
| properties       | os_hidden='False', owner_specified.openstack.md5='', owner_specified.openstack.object='images/COOKBOOK_UBUNTU_IMAGE', owner_specified.openstack.sha256='' |
| protected        | False                                                                                                                                                     |
| schema           | /v2/schemas/image                                                                                                                                         |
| status           | queued                                                                                                                                                    |
| tags             |                                                                                                                                                           |
| updated_at       | 2023-04-12T02:30:32Z                                                                                                                                      |
| visibility       | shared                                                                                                                                                    |
+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
```
![](https://i.imgur.com/ClZTOgV.png)

* OpenStack Cloud Computing Cookbook 4th ed. 2018
  * https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-disk1.img
  * openstack image create COOKBOOK_UBUNTU_IMAGE --disk-format qcow2 --file /tmp/xenial-server-cloudimg-amd64-disk1.img
  * The qcow2 format is popular among OpenStack-based clouds running QEMU/KVM hypervisors


## environment

* host physical machine:
  * cpu:
  * RAM: 16G
  * enabled AMD-v in BIOS
* host vm: 
  * vagrant
  * Virtualbox: bento/ubuntu-20.04

### vagrant

#### Vagrantfile
```
~/unm/S23/ECE530/HW1/vagrant$ cat Vagrantfile 
# -*- mode: ruby -*-
# vi: set ft=ruby :

require_relative 'config' rescue LoadError

Vagrant.configure("2") do |config|

  OS = "bento/ubuntu-20.04"

  def configVMCapacity(vb, cpus, memory)
    vb.gui = false
    vb.memory = memory
    vb.cpus = cpus
  end

  def setVMForwardedPort(df, name, ports)
    if ports
      ports.each do |port|
        df.vm.network :forwarded_port, guest: port[:NODE_PORT], host: port[:TARGET_PORT], host_ip: "0.0.0.0", id: "#{name}:#{port[:NODE_PORT]}", auto_correct: true
      end
    end
  end

  config.vm.provider "virtualbox"
  config.vm.box = "#{OS}"

  VMS.each do |vm|
    config.vm.define "develop-#{vm[:NAME]}" do |df|
      df.vm.hostname = "#{vm[:NAME]}"
      df.vm.network :private_network, ip: vm[:IP],  auto_config: true
      setVMForwardedPort(df, vm[:NAME], vm[:PORT])
      df.vm.network "public_network", auto_config: false
      df.vm.provider :virtualbox do |vb, override|
        configVMCapacity(vb, vm[:CPUS], vm[:MEMORY_MB])
      end
    end
  end
end
```

#### config.rb
```
$ cat config.rb 
VMS = [
    {
      :NAME => "controller",
      :IP => "192.168.56.101",
      :MEMORY_MB => 6144,
      :CPUS => 2,
      :PORT => [
        {
          :NODE_PORT => 5000,
          :TARGET_PORT => 30001,
        }
      ]
    },
    {
      :NAME => "compute",
      :IP => "192.168.56.151",
      :MEMORY_MB => 8192,
      :CPUS => 4,
      :PORT => [
        {
          :NODE_PORT => 30001,
          :TARGET_PORT => 30002,
        }
      ]
    },
    {
      :NAME => "controller2",
      :IP => "192.168.56.102",
      :MEMORY_MB => 8192,
      :CPUS => 4,
      :PORT => [
        {
          :NODE_PORT => 30001,
          :TARGET_PORT => 30003,
        }
      ]
    }
  ]
```

#### vagrant commands and console outputs on physical host machine
```
$ vagrant up
==> vagrant: A new version of Vagrant is available: 2.3.4 (installed version: 2.2.14)!
==> vagrant: To upgrade visit: https://www.vagrantup.com/downloads.html
==> develop-controller: Adding box 'bento/ubuntu-20.04' (v202303.13.0) for provider: virtualbox
    develop-controller: Downloading: https://vagrantcloud.com/bento/boxes/ubuntu-20.04/versions/202303.13.0/providers/virtualbox.box
Download redirected to host: vagrantcloud-files-production.s3-accelerate.amazonaws.com
```

![](https://i.imgur.com/cdzQwh0.png)

### 
```
```
![](https://i.imgur.com/p0i8SyI.png)

![](https://i.imgur.com/BpkddAk.png)

### controller node
```
sudo apt install chrony
sudo service chrony restart
```

* https://docs.openstack.org/install-guide/environment-ntp-controller.html
* 

![](https://i.imgur.com/ezrRzBh.png)

### other nodes (compute, ..)
```
sudo apt install chrony
sudo vim /etc/chrony/chrony.conf
sudo service chrony restart
systemctl status chrony
chronyc sources
```
![](https://i.imgur.com/piHXqCM.png)

### all nodes
```
sudo add-apt-repository cloud-archive:yoga
sudo apt install python3-openstackclient
```
* https://docs.openstack.org/install-guide/environment-packages-ubuntu.html
* 

### controller:
```
sudo apt install mariadb-server python3-pymysql
sudo vim /etc/mysql/mariadb.conf.d/99-openstack.cnf
sudo service mysql restart
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';
sudo apt-get purge mariadb-* 

```

![](https://i.imgur.com/T47LJ7c.png)

![](https://i.imgur.com/hoUa0PF.png)

![](https://i.imgur.com/CBoLSq0.png)


* https://docs.openstack.org/install-guide/environment-sql-database.html
* https://docs.openstack.org/install-guide/environment-sql-database-ubuntu.html
* https://stackoverflow.com/questions/36099028/error-1064-42000-you-have-an-error-in-your-sql-syntax-want-to-configure-a-pa
* https://stackoverflow.com/questions/60345231/completely-remove-mariadb-10-01-in-ubuntu-18-04
* https://stackoverflow.com/questions/41645309/mysql-error-access-denied-for-user-rootlocalhost
* 

### controller:
```
sudo apt install rabbitmq-server
sudo rabbitmqctl add_user openstack rabbit
sudo rabbitmqctl set_permissions openstack ".*" ".*" ".*"

sudo apt install memcached python3-memcache
sudo vim /etc/memcached.conf
sudo service memcached restart

sudo apt install etcd
sudo vim /etc/default/etcd
cat /etc/default/etcd | grep -e ETCD_INITIAL_CLUSTER -e ETCD_INITIAL_ADVERTISE_PEER_URLS -e ETCD_ADVERTISE_CLIENT_URLS -e ETCD_LISTEN_CLIENT_URLS -n -e ETCD_NAME -e ETCD_DATA_DIR -e ETCD_INITIAL_CLUSTER_STATE -e ETCD_INITIAL_CLUSTER_TOKEN
sudo systemctl restart etcd
sudo systemctl enable etcd
sudo systemctl restart etcd
systemctl status etcd
```
![](https://i.imgur.com/zghXDNi.png)

![](https://i.imgur.com/0WmHy79.png)

![](https://i.imgur.com/Zpemue7.png)


* https://docs.openstack.org/install-guide/environment-messaging-ubuntu.html
* https://docs.openstack.org/install-guide/environment-memcached-ubuntu.html
* https://docs.openstack.org/install-guide/environment-etcd-ubuntu.html
* 

## keystone
```
sudo -i
mysql -u root -p
apt install keystone
cat /etc/keystone/keystone.conf 
cat /etc/keystone/keystone.conf  | grep -n -e "connection ="
vim /etc/keystone/keystone.conf
cat /etc/keystone/keystone.conf  | grep -n -e "connection =" -B 3
cat /etc/keystone/keystone.conf  | grep -n -e "provider = "
cat /etc/keystone/keystone.conf  | grep -n -e "provider = " -e "\[ token"
cat /etc/keystone/keystone.conf  | grep -n -e "provider = " -e "\[token"
vim /etc/keystone/keystone.conf
su -s /bin/sh -c "keystone-manage db_sync" keystone
keystone-manage fernet_setup --keystone-user keystone --keystone-group keystone
keystone-manage credential_setup --keystone-user keystone --keystone-group keystone
keystone-manage bootstrap --bootstrap-password ADMIN_PASS   --bootstrap-admin-url http://controller:5000/v3/   --bootstrap-internal-url http://controller:5000/v3/   --bootstrap-public-url http://controller:5000/v3/   --bootstrap-region-id RegionOne
vim /etc/apache2/apache2.conf
service apache2 restart
systemctl status apache2
```
![](https://i.imgur.com/I0Dk2ug.png)

### keystone - Create a domain, projects, users, and roles
```
export OS_USERNAME=admin
export OS_PASSWORD=ADMIN_PASS
export OS_PROJECT_NAME=admin
export OS_USER_DOMAIN_NAME=Default
export OS_PROJECT_DOMAIN_NAME=Default
export OS_AUTH_URL=http://controller:5000/v3
export OS_IDENTITY_API_VERSION=3

# apt install python3-openstackclient
# openstack project create --domain default   --description "Service Project" service
# openstack project create --domain default   --description "Demo Project" myproject

# openstack user create --domain default   --password-prompt myuser
User Password:user
Repeat User Password:user
openstack role create myrole
```


```
# openstack domain create --description "An Example Domain" example
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | An Example Domain                |
| enabled     | True                             |
| id          | ba2c558cae944214b8e18b33c0d4126a |
| name        | example                          |
| options     | {}                               |
| tags        | []                               |
+-------------+----------------------------------+
```
* https://docs.openstack.org/keystone/yoga/install/keystone-users-ubuntu.html 
* https://docs.openstack.org/keystone/yoga/install/keystone-install-ubuntu.html
* 

### keystone - Verify operation
```
# openstack --os-auth-url http://controller:5000/v3   --os-project-domain-name Default --os-user-domain-name Default   --os-project-name admin --os-username admin token issue
Password: 
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field      | Value                                                                                                                                                                                   |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| expires    | 2023-04-03T07:51:44+0000                                                                                                                                                                |
| id         | gAAAAABkKneA7p5rHKnGFu-0sB-asHxusxRnRicpo5vfDrKEgYrAaOor9-KiiigWC5wuuvdoXBUY9PjMhpnYBBsfvbJUDU4_ODS53c4YRqBQ4ZthGVjo1WviYFVcatVu6iMa1tVNjuDW_Sqa5ZVoY5tR4DOe8sRTmpfcvdDETsZQDdN-KRgYE9I |
| project_id | dd1bd9e23e7440f0ab943dedfb5aefbc                                                                                                                                                        |
| user_id    | b08a3a4ea5cb474f893835ce0c0722ae                                                                                                                                                        |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```
* https://docs.openstack.org/keystone/yoga/install/keystone-verify-ubuntu.html
* 

```
# openstack --os-auth-url http://controller:5000/v3 \
>   --os-project-domain-name Default --os-user-domain-name Default \
>   --os-project-name myproject --os-username myuser token issue
Password: 
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field      | Value                                                                                                                                                                                   |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| expires    | 2023-04-03T08:00:56+0000                                                                                                                                                                |
| id         | gAAAAABkKnmo64_mFYdTh1_xfxfVVqCydnyf1TnMHT1A6QbPrvTHq8XL8HZfd1ePKz99EWTCflwyrE4INNYANgUIt0fWc8HoHay4gkwNsReAkbohgnmwCzz-TzHuPSaEL0oG-_THJMkjdYjjCJrBPBnWKnTOKcmci6yUSEU7r-yxdPyYNbCz6eY |
| project_id | 7926c5914b78451d9faff81ba6791d61                                                                                                                                                        |
| user_id    | e2e915e124c24ff9adf94966a856d5ec                                                                                                                                                        |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```


```
$ openstack --os-auth-url http://controller:5000/v3 \
>   --os-project-domain-name Default --os-user-domain-name Default \
>   --os-project-name admin --os-username admin token issue
Password: 
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field      | Value                                                                                                                                                                                   |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| expires    | 2023-04-04T21:25:08+0000                                                                                                                                                                |
| id         | gAAAAABkLIeklbI5p4ayljGdO2pyHM77xp1Nrd_FJ18-42ewLiZX2gexh4iMtOVVKYWmlct_voKzRwP0RG8xLd2cU2XuGRB8yUhDZ3XP9pBnFIa3VYHk9lFiP53CZ5Vr_uTtzFrR3z-5q1KhmnnmpVm20x60b1Er5eAGokhjWNP8lxCpV6AkyCM |
| project_id | dd1bd9e23e7440f0ab943dedfb5aefbc                                                                                                                                                        |
| user_id    | b08a3a4ea5cb474f893835ce0c0722ae                                                                                                                                                        |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

### Create OpenStack client environment scripts
```
# vim admin-openrc
# vim demo-openrc
# . admin-openrc
# openstack token issue
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field      | Value                                                                                                                                                                                   |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| expires    | 2023-04-04T21:45:27+0000                                                                                                                                                                |
| id         | gAAAAABkLIxn8OaDiUL1oGbrpW-wJzp2PuAoXUliVjwj7TefjZOdJBynR_FHgV_8GckXR2zMHT7uiIRacpgOgk-RqPJAEFzIpO-zEkkBrW1Z6898WHVZsLOVpdI5gJ6KGyViiAgpVFku_PBQlQuoW2nRtocU32W9MIEJEGNPj28U54482Wdz5-0 |
| project_id | dd1bd9e23e7440f0ab943dedfb5aefbc                                                                                                                                                        |
| user_id    | b08a3a4ea5cb474f893835ce0c0722ae                                                                                                                                                        |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

```
* https://docs.openstack.org/keystone/yoga/install/keystone-openrc-ubuntu.html
* 


```
$ openstack user list
+----------------------------------+--------+
| ID                               | Name   |
+----------------------------------+--------+
| b08a3a4ea5cb474f893835ce0c0722ae | admin  |
| e2e915e124c24ff9adf94966a856d5ec | myuser |
+----------------------------------+--------+

$ openstack role list
+----------------------------------+--------+
| ID                               | Name   |
+----------------------------------+--------+
| 0bab649ade9440e09d245452a2f4f532 | reader |
| 1ed58e4603dd49b3a4dfdd9f3892a9d5 | member |
| 4c05f47a9be943afadb36621570cf348 | admin  |
| ccf8a8e9ee0c45f0b3520225ac6f1ade | myrole |
+----------------------------------+--------+
```

## glance (Yoga)
### Install and configure (Debian)
```
$ mysql -u root -p
$ . admin-openrc
$ openstack user create --domain default --password-prompt glance
$ openstack role add --project service --user glance admin
$ openstack service create --name glance \
>   --description "OpenStack Image" image
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | OpenStack Image                  |
| enabled     | True                             |
| id          | 5e176e9436334afd8a047ffb9ad806e4 |
| name        | glance                           |
| type        | image                            |
+-------------+----------------------------------+

$ openstack endpoint create --region RegionOne \
>   image public http://controller:9292
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 9f2e43ca97fb4ef8b0f934e69234d297 |
| interface    | public                           |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 5e176e9436334afd8a047ffb9ad806e4 |
| service_name | glance                           |
| service_type | image                            |
| url          | http://controller:9292           |
+--------------+----------------------------------+

$ openstack endpoint create --region RegionOne \
>   image internal http://controller:9292
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 35f35d2dd4244dca9eaac95ca3761fde |
| interface    | internal                         |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 5e176e9436334afd8a047ffb9ad806e4 |
| service_name | glance                           |
| service_type | image                            |
| url          | http://controller:9292           |
+--------------+----------------------------------+

$ openstack endpoint create --region RegionOne \
>   image admin http://controller:9292
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 6c47243220154acf99750d83d9e97110 |
| interface    | admin                            |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 5e176e9436334afd8a047ffb9ad806e4 |
| service_name | glance                           |
| service_type | image                            |
| url          | http://controller:9292           |
+--------------+----------------------------------+

```
![](https://i.imgur.com/dH93j4F.png)

```
$ sudo -i
root@controller:~# apt install glance
E: Failed to fetch http://ubuntu-cloud.archive.canonical.com/ubuntu/pool/main/c/ceph/librados2_17.2.0-0ubuntu0.22.04.2~cloud0_amd64.deb  404  Not Found [IP: 185.125.190.36 80]
E: Failed to fetch http://ubuntu-cloud.archive.canonical.com/ubuntu/pool/main/c/ceph/librbd1_17.2.0-0ubuntu0.22.04.2~cloud0_amd64.deb  404  Not Found [IP: 185.125.190.36 80]
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?

# apt-get update
# apt install glance

# cat /etc/glance/glance-api.conf | grep -n -e "\[database" -e "connection = "
1746:[database]
1747:connection = sqlite:////var/lib/glance/glance.sqlite
1766:#connection = <None>
1770:#slave_connection = <None>

# cat /etc/glance/glance-api.conf | grep -n -e "\[keystone_authtoken" -e "\[paste_deploy"
4966:[keystone_authtoken]
4979:# Deprecated group/name - [keystone_authtoken]/auth_uri
5040:# Deprecated group/name - [keystone_authtoken]/memcache_servers
5120:# Deprecated group/name - [keystone_authtoken]/auth_plugin
5661:[paste_deploy]

# cat /etc/glance/glance-api.conf | grep -n -e "\[glance_store"
3140:[glance_store]
```
![](https://i.imgur.com/sqG2wrn.png)

* https://docs.openstack.org/glance/yoga/install/install-debian.html
* GRANT ALL PRIVILEGES ON glance.* TO 'glance'@'%' IDENTIFIED BY 'GLANCE_DBPASS';


```
% git log -S "ENDPOINT_ID" --format=%h%cd%ae%s
1409cc94bTue Sep 27 03:01:13 2022 +0200cyril@redhat.comQuota configuration: improve example oslo_limit section
da771fce2Fri Jul 2 08:29:07 2021 -0700dansmith@redhat.comAdd unified quotas documentation

. /home/vagrant/admin-openrc
# openstack role add --user MY_SERVICE --user-domain Default --system all reader
# openstack role add --user glance --user-domain Default --system all reader
```
* url = https://github.com/openstack/glance
* 

### Populate the Image service database:
```
root@controller:~# vim  /etc/glance/glance-api.conf
root@controller:~# su -s /bin/sh -c "glance-manage db_sync" glance
2023-04-06 03:10:28.343 120962 INFO alembic.runtime.migration [-] Context impl MySQLImpl.
2023-04-06 03:10:28.344 120962 INFO alembic.runtime.migration [-] Will assume non-transactional DDL.
2023-04-06 03:10:28.349 120962 INFO alembic.runtime.migration [-] Context impl MySQLImpl.
2023-04-06 03:10:28.349 120962 INFO alembic.runtime.migration [-] Will assume non-transactional DDL.
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> liberty, liberty initial
INFO  [alembic.runtime.migration] Running upgrade liberty -> mitaka01, add index on created_at and updated_at columns of 'images' table
INFO  [alembic.runtime.migration] Running upgrade mitaka01 -> mitaka02, update metadef os_nova_server
INFO  [alembic.runtime.migration] Running upgrade mitaka02 -> ocata_expand01, add visibility to images
INFO  [alembic.runtime.migration] Running upgrade ocata_expand01 -> pike_expand01, empty expand for symmetry with pike_contract01
INFO  [alembic.runtime.migration] Running upgrade pike_expand01 -> queens_expand01
INFO  [alembic.runtime.migration] Running upgrade queens_expand01 -> rocky_expand01, add os_hidden column to images table
INFO  [alembic.runtime.migration] Running upgrade rocky_expand01 -> rocky_expand02, add os_hash_algo and os_hash_value columns to images table
INFO  [alembic.runtime.migration] Running upgrade rocky_expand02 -> train_expand01, empty expand for symmetry with train_contract01
INFO  [alembic.runtime.migration] Running upgrade train_expand01 -> ussuri_expand01, empty expand for symmetry with ussuri_expand01
INFO  [alembic.runtime.migration] Running upgrade ussuri_expand01 -> wallaby_expand01, add image_id, request_id, user columns to tasks table"
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
Upgraded database to: wallaby_expand01, current revision(s): wallaby_expand01
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
Database migration is up to date. No migration needed.
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade mitaka02 -> ocata_contract01, remove is_public from images
INFO  [alembic.runtime.migration] Running upgrade ocata_contract01 -> pike_contract01, drop glare artifacts tables
INFO  [alembic.runtime.migration] Running upgrade pike_contract01 -> queens_contract01
INFO  [alembic.runtime.migration] Running upgrade queens_contract01 -> rocky_contract01
INFO  [alembic.runtime.migration] Running upgrade rocky_contract01 -> rocky_contract02
INFO  [alembic.runtime.migration] Running upgrade rocky_contract02 -> train_contract01
INFO  [alembic.runtime.migration] Running upgrade train_contract01 -> ussuri_contract01
INFO  [alembic.runtime.migration] Running upgrade ussuri_contract01 -> wallaby_contract01
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
Upgraded database to: wallaby_contract01, current revision(s): wallaby_contract01
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
Database is synced successfully.
root@controller:~#

# systemctl status glance-api
● glance-api.service - OpenStack Image Service API
     Loaded: loaded (/lib/systemd/system/glance-api.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2023-04-06 03:15:36 UTC; 2s ago
       Docs: man:glance-api(1)
   Main PID: 121218 (glance-api)
      Tasks: 3 (limit: 7021)
     Memory: 107.4M
     CGroup: /system.slice/glance-api.service
             ├─121218 /usr/bin/python3 /usr/bin/glance-api --config-file=/etc/glance/glance-api.conf --config-dir=/etc/glance/ --log-file=/var/log/glance/glance-api.log
```

### download cirros image
```
root@controller:~# wget http://download.cirros-cloud.net/0.4.0/cirros-0.4.0-x86_64-disk.img
--2023-04-06 03:17:29--  http://download.cirros-cloud.net/0.4.0/cirros-0.4.0-x86_64-disk.img
Resolving download.cirros-cloud.net (download.cirros-cloud.net)... 64.90.42.85, 2607:f298:6:a036::bd6:a72a
Connecting to download.cirros-cloud.net (download.cirros-cloud.net)|64.90.42.85|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://github.com/cirros-dev/cirros/releases/download/0.4.0/cirros-0.4.0-x86_64-disk.img [following]
--2023-04-06 03:17:30--  https://github.com/cirros-dev/cirros/releases/download/0.4.0/cirros-0.4.0-x86_64-disk.img
Resolving github.com (github.com)... 140.82.114.4
Connecting to github.com (github.com)|140.82.114.4|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/219785102/b2074f00-411a-11ea-9620-afb551cf9af3?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230406%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230406T031730Z&X-Amz-Expires=300&X-Amz-Signature=01e32d631fb80c315d71709b74019d5a65221be5bf8edffa7b2caec21a229654&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=219785102&response-content-disposition=attachment%3B%20filename%3Dcirros-0.4.0-x86_64-disk.img&response-content-type=application%2Foctet-stream [following]
--2023-04-06 03:17:31--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/219785102/b2074f00-411a-11ea-9620-afb551cf9af3?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230406%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230406T031730Z&X-Amz-Expires=300&X-Amz-Signature=01e32d631fb80c315d71709b74019d5a65221be5bf8edffa7b2caec21a229654&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=219785102&response-content-disposition=attachment%3B%20filename%3Dcirros-0.4.0-x86_64-disk.img&response-content-type=application%2Foctet-stream
Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.110.133, 185.199.111.133, 185.199.108.133, ...
Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 12716032 (12M) [application/octet-stream]
Saving to: ‘cirros-0.4.0-x86_64-disk.img’

cirros-0.4.0-x86_64-disk.img                  100%[=================================================================================================>]  12.13M  7.25MB/s    in 1.7s    

2023-04-06 03:17:33 (7.25 MB/s) - ‘cirros-0.4.0-x86_64-disk.img’ saved [12716032/12716032]

. /home/vagrant/admin-openrc 
# glance image-create --name "cirros"   --file cirros-0.4.0-x86_64-disk.img   --disk-format qcow2 --container-format bare   --visibility=public
Invalid OpenStack Identity credentials.

# cat /var/log/glance/glance-api.log
2023-04-06 03:24:14.691 121247 WARNING keystonemiddleware.auth_token [-] Identity response: {"error":{"code":401,"message":"The request you have made requires authentication.","title":"Unauthorized"}}
: keystoneauth1.exceptions.http.Unauthorized: The request you have made requires authentication. (HTTP 401) (Request-ID: req-c776f729-33bf-43f0-851e-5eaf193add31)

# cat /etc/glance/glance-api.conf | grep -n -e "\[keystone_authtoken" -A 10
4980-username = glance
4981-password = GLANCE_PASS

openstack user set --password glance
openstack user set --password GLANCE_PASS glance

# glance image-create --name "cirros"   --file cirros-0.4.0-x86_64-disk.img   --disk-format qcow2 --container-format bare   --visibility=public
File cirros-0.4.0-x86_64-disk.img does not exist or user does not have read privileges to it

# glance image-create --name "cirros"   --file cirros-0.4.0-x86_64-disk.img   --disk-format qcow2 --container-format bare   --visibility=public
HTTP 500 Internal Server Error: The server has either erred or is incapable of performing the requested operation.
```
* https://docs.openstack.org/glance/yoga/install/verify.html
* https://docs.openstack.org/python-openstackclient/queens/cli/command-objects/user.html
* 


```
MariaDB [(none)]> show grants;
+---------------------------------------------------------------------------------------------------------------+
| Grants for glance@localhost                                                                                   |
+---------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `glance`@`localhost` IDENTIFIED BY PASSWORD '*C0CE56F2C0C7234791F36D89700B02691C1CAB8E' |
| GRANT ALL PRIVILEGES ON `glance`.* TO `glance`@`localhost`                                                    |
+---------------------------------------------------------------------------------------------------------------+
```
![](https://i.imgur.com/mWpjoUV.png)

* https://stackoverflow.com/questions/46663801/openstack-glance-sync-error
* 

```
. /home/vagrant/admin-openrc 
openstack role add --user glance  --user-domain Default --system all reader
su -s /bin/sh -c "glance-manage db_sync" glance
mysql -h controller -u glance -p
mysql -u glance -p
sudo lsof -i -P -n | grep LISTEN'
sudo lsof -i -P -n | grep LISTEN
```

```
openstack service create --name glance --description "OpenStack Image" image
internal a6e4b153c2ae4c919eccfdbb7dceb5d2

# cat /etc/glance/glance-api.conf | grep -n -e "\[oslo_lim" -A 10
5141:[oslo_limit]
5142-auth_url = http://controller:5000
5143-auth_type = password
5144-user_domain_id = default
5145-username = glance
5146-system_scope = all
5147-password = MY_PASSWORD
5148-endpoint_id = ENDPOINT_ID
5149-region_name = RegionOne

service glance-api restart

# cat /etc/glance/glance-api.conf | grep -n -e "\[database" -e "connection = "
1748:[database]
1749:connection = mysql+pymysql://glance:GLANCE_DBPASS@controller/glance

# cat /etc/glance/glance-api.conf | grep -n -e "\[database" -e "connection = "
1748:[database]
1749:connection = mysql+pymysql://glance:GLANCE_DBPASS@controller/glance

mysql -u glance -p

```


```
# glance image-create --name "cirros" \
>   --file cirros-0.4.0-x86_64-disk.img \
>   --disk-format qcow2 --container-format bare \
>   --visibility=public
+------------------+----------------------------------------------------------------------------------+
| Property         | Value                                                                            |
+------------------+----------------------------------------------------------------------------------+
| checksum         | 443b7623e27ecf03dc9e01ee93f67afe                                                 |
| container_format | bare                                                                             |
| created_at       | 2023-04-06T17:57:53Z                                                             |
| disk_format      | qcow2                                                                            |
| id               | d6fc5ad0-4076-4cc3-83b3-33ef4a8efecd                                             |
| min_disk         | 0                                                                                |
| min_ram          | 0                                                                                |
| name             | cirros                                                                           |
| os_hash_algo     | sha512                                                                           |
| os_hash_value    | 6513f21e44aa3da349f248188a44bc304a3653a04122d8fb4535423c8e1d14cd6a153f735bb0982e |
|                  | 2161b5b5186106570c17a9e58b64dd39390617cd5a350f78                                 |
| os_hidden        | False                                                                            |
| owner            | dd1bd9e23e7440f0ab943dedfb5aefbc                                                 |
| protected        | False                                                                            |
| size             | 12716032                                                                         |
| status           | active                                                                           |
| tags             | []                                                                               |
| updated_at       | 2023-04-06T17:57:53Z                                                             |
| virtual_size     | 46137344                                                                         |
| visibility       | public                                                                           |
+------------------+----------------------------------------------------------------------------------+
```
* https://docs.openstack.org/glance/yoga/configuration/index.html
* 

## placement
* https://docs.openstack.org/install-guide/openstack-services.html#minimal-deployment-for-yoga
* https://docs.openstack.org/placement/yoga/install/
* 

### Controller
```
# apt-get install python3-pip

# pip3 install python-openstackclient
Requirement already satisfied: python-openstackclient in /usr/lib/python3/dist-packages (5.8.0)

# mysql -h controller -u root -p
# mysql -u root -p

# openstack user create --domain default --password-prompt placement
User Password:
Repeat User Password:
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| enabled             | True                             |
| id                  | e7119b9a9b124ac4863058380142146f |
| name                | placement                        |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+

# openstack role add --project service --user placement admin

# openstack service create --name placement \
>   --description "Placement API" placement
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | Placement API                    |
| enabled     | True                             |
| id          | c7e3b27998564de8871f62d6285fd6a3 |
| name        | placement                        |
| type        | placement                        |
+-------------+----------------------------------

# openstack endpoint create --region RegionOne \
>   placement public http://controller:8778
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 98101368e143403ab64e5c93f0188d41 |
| interface    | public                           |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | c7e3b27998564de8871f62d6285fd6a3 |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+

# openstack endpoint create --region RegionOne \
>   placement internal http://controller:8778
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | ca55dbd9293f4cf8841d76fe869ca182 |
| interface    | internal                         |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | c7e3b27998564de8871f62d6285fd6a3 |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+

# openstack endpoint create --region RegionOne \
>   placement admin http://controller:8778
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | b8fc42cf8a5f44eb95998245514f9703 |
| interface    | admin                            |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | c7e3b27998564de8871f62d6285fd6a3 |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+

# pip3 install openstack-placement pymysql

# mkdir /etc/placement/
# vim /etc/placement/placement.conf
# cat /etc/placement/placement.conf
[placement_database]
connection = mysql+pymysql://placement:PLACEMENT_DBPASS@controller/placement

[api]
auth_strategy = keystone  # use noauth2 if not using keystone

[keystone_authtoken]
www_authenticate_uri = http://controller:5000/
auth_url = http://controller:5000/
memcached_servers = controller:11211
auth_type = password
project_domain_name = Default
user_domain_name = Default
project_name = service
username = placement
password = PLACEMENT_PASS

# placement-manage db sync
# pip3  install uwsgi
Building wheels for collected packages: uwsgi
  Building wheel for uwsgi (setup.py) ... done
  Created wheel for uwsgi: filename=uWSGI-2.0.21-cp38-cp38-linux_x86_64.whl size=516424 sha256=148dc44a2d10efd51c098bd3fe00f32ebbe438a2c1e175888548ed18b8089f05
  Stored in directory: /root/.cache/pip/wheels/ff/1f/b4/8bd0ceee591f1fdbbff1b106e279b74db7f8df386291b2e79b
Successfully built uwsgi
Installing collected packages: uwsgi
Successfully installed uwsgi-2.0.21

# uwsgi -M --http :8778 --wsgi-file /usr/local/bin/placement-api \
>         --processes 2 --threads 10
*** Starting uWSGI 2.0.21 (64bit) on [Thu Apr  6 22:41:40 2023] ***
compiled with version: 9.4.0 on 06 April 2023 22:40:08
os: Linux-5.4.0-144-generic #161-Ubuntu SMP Fri Feb 3 14:49:04 UTC 2023

nodename: controller
machine: x86_64
clock source: unix
detected number of CPU cores: 2
current working directory: /home/vagrant
detected binary path: /usr/local/bin/uwsgi
!!! no internal routing support, rebuild with pcre support !!!
uWSGI running as root, you can use --uid/--gid/--chroot options
*** WARNING: you are running uWSGI as root !!! (use the --uid flag) *** 
your processes number limit is 23406
your memory page size is 4096 bytes
detected max file descriptor number: 1024
lock engine: pthread robust mutexes
thunder lock: disabled (you can enable it with --thunder-lock)
uWSGI http bound on :8778 fd 4
uwsgi socket 0 bound to TCP address 127.0.0.1:38007 (port auto-assigned) fd 3
uWSGI running as root, you can use --uid/--gid/--chroot options

2023-04-06 22:41:41.231 32778 CRITICAL placement [-] Unhandled error: oslo_config.cfg.ConfigFileValueError: Value for option auth_strategy from LocationInfo(location=<Locations.user: (4, True)>, detail='/etc/placement/placement.conf') is not valid: Valid values are [keystone, noauth2], but found 'keystone  # use noauth2 if not using keystone'
2023-04-06 22:41:41.231 32778 ERROR placement ValueError: Valid values are [keystone, noauth2], but found 'keystone  # use noauth2 if not using keystone'

root@compute:~# curl http://controller:8778/
{"versions": [{"id": "v1.0", "max_version": "1.39", "min_version": "1.0", "status": "CURRENT", "links": [{"rel": "self", "href": ""}]}]}

Further interactions with the system can be made with osc-placement.

```
* https://docs.openstack.org/install-guide/overview.html
* https://docs.openstack.org/install-guide/_images/network1-services.png
* https://docs.openstack.org/placement/yoga/install/from-pypi.html
* User Password:PLACEMENT_PASS
* 


```
# apt install placement-api
...
Configuration file '/etc/placement/placement.conf'
 ==> File on system created by you or by a script.
 ==> File also in package provided by package maintainer.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** placement.conf (Y/I/N/O/D/Z) [default=N] ? 
Adding system user `placement' (UID 121) ...
Adding new user `placement' (UID 121) with group `placement' ...
Not creating home directory `/var/lib/placement'.
Setting up python3-os-resource-classes (1.1.0-0ubuntu1~cloud0) ...
Setting up python3-placement (1:7.0.0-0ubuntu1~cloud0) ...
Setting up placement-api (1:7.0.0-0ubuntu1~cloud0) ...
apache2_invoke: Enable site placement-api.conf

# su -s /bin/sh -c "placement-manage db sync" placement
# service apache2 restart

```
* https://docs.openstack.org/placement/yoga/install/install-ubuntu.html
* 

```
# placement-status upgrade check
+-------------------------------------------+
| Upgrade Check Results                     |
+-------------------------------------------+
| Check: Missing Root Provider IDs          |
| Result: Success                           |
| Details: None                             |
+-------------------------------------------+
| Check: Incomplete Consumers               |
| Result: Success                           |
| Details: None                             |
+-------------------------------------------+
| Check: Policy File JSON to YAML Migration |
| Result: Success                           |
| Details: None                             |
+-------------------------------------------+

# pip3 install osc-placement
Collecting osc-placement
  Downloading osc_placement-4.1.0-py3-none-any.whl (64 kB)
Requirement already satisfied: oslo.utils>=3.37.0 in /usr/lib/python3/dist-packages (from osc-placement) (4.12.2)
Requirement already satisfied: simplejson>=3.16.0 in /usr/lib/python3/dist-packages (from osc-placement) (3.16.0)
Requirement already satisfied: osc-lib>=1.2.0 in /usr/lib/python3/dist-packages (from osc-placement) (2.5.0)
Requirement already satisfied: keystoneauth1>=3.3.0 in /usr/lib/python3/dist-packages (from osc-placement) (4.4.0)
Requirement already satisfied: pbr>=2.0.0 in /usr/lib/python3/dist-packages (from osc-placement) (5.8.0)
Installing collected packages: osc-placement
Successfully installed osc-placement-4.1.0


# openstack --os-placement-api-version 1.2 resource class list --sort-column name
+----------------------------------------+
| name                                   |
+----------------------------------------+
| DISK_GB                                |
| FPGA                                   |
| IPV4_ADDRESS                           |
| MEMORY_MB                              |
| MEM_ENCRYPTION_CONTEXT                 |
| NET_BW_EGR_KILOBIT_PER_SEC             |
| NET_BW_IGR_KILOBIT_PER_SEC             |
| NET_PACKET_RATE_EGR_KILOPACKET_PER_SEC |
| NET_PACKET_RATE_IGR_KILOPACKET_PER_SEC |
| NET_PACKET_RATE_KILOPACKET_PER_SEC     |
| NUMA_CORE                              |
| NUMA_MEMORY_MB                         |
| NUMA_SOCKET                            |
| NUMA_THREAD                            |
| PCI_DEVICE                             |
| PCPU                                   |
| PGPU                                   |
| SRIOV_NET_VF                           |
| VCPU                                   |
| VGPU                                   |
| VGPU_DISPLAY_HEAD                      |
+----------------------------------------+

# openstack --os-placement-api-version 1.6 trait list --sort-column name
+---------------------------------------+
| name                                  |
+---------------------------------------+
| COMPUTE_ACCELERATORS                  |
| COMPUTE_ADDRESS_SPACE_EMULATED        |
| COMPUTE_ADDRESS_SPACE_PASSTHROUGH     |
| COMPUTE_ARCH_AARCH64                  |
| COMPUTE_ARCH_MIPSEL                   |
| COMPUTE_ARCH_PPC64LE                  |
| COMPUTE_ARCH_RISCV64                  |
| COMPUTE_ARCH_S390X                    |
| COMPUTE_ARCH_X86_64                   |
| COMPUTE_CONFIG_DRIVE_REGENERATION     |
| COMPUTE_DEVICE_TAGGING                |
| COMPUTE_EPHEMERAL_ENCRYPTION          |
| COMPUTE_EPHEMERAL_ENCRYPTION_LUKS     |
| COMPUTE_EPHEMERAL_ENCRYPTION_LUKSV2   |
| COMPUTE_EPHEMERAL_ENCRYPTION_PLAIN    |
| COMPUTE_FIRMWARE_BIOS                 |


```
* https://docs.openstack.org/placement/yoga/install/verify.html
  * This example uses PyPI and pip but if you are using distribution packages you can install the package from their repository. With the move to python3 you will need to specify pip3 or install python3-osc-placement from your distribution.
* https://docs.openstack.org/placement/yoga/admin/index.html
* 


## nova
```
# mysql -u root -p
# openstack user create --domain default --password-prompt nova
User Password:
Repeat User Password:
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| enabled             | True                             |
| id                  | 13b30c88746640d3ab77930a175858b7 |
| name                | nova                             |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+

# openstack role add --project service --user nova admin
# openstack service create --name nova \
>   --description "OpenStack Compute" compute
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | OpenStack Compute                |
| enabled     | True                             |
| id          | 2f5b228097dc43b8acb089ed283ea4da |
| name        | nova                             |
| type        | compute                          |
+-------------+----------------------------------+

# openstack endpoint create --region RegionOne \
>   compute public http://controller:8774/v2.1
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 674da6680b384142abe7b3a3b7c7a9b3 |
| interface    | public                           |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 2f5b228097dc43b8acb089ed283ea4da |
| service_name | nova                             |
| service_type | compute                          |
| url          | http://controller:8774/v2.1      |
+--------------+----------------------------------+

# openstack endpoint create --region RegionOne \
>   compute internal http://controller:8774/v2.1
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | a0b09784cefd4d139c83a48678b90077 |
| interface    | internal                         |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 2f5b228097dc43b8acb089ed283ea4da |
| service_name | nova                             |
| service_type | compute                          |
| url          | http://controller:8774/v2.1      |
+--------------+----------------------------------+

# openstack endpoint create --region RegionOne \
>   compute admin http://controller:8774/v2.1
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | dc744033b81d4ef485ec79ec7b1ac44f |
| interface    | admin                            |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 2f5b228097dc43b8acb089ed283ea4da |
| service_name | nova                             |
| service_type | compute                          |
| url          | http://controller:8774/v2.1      |
+--------------+----------------------------------+

# apt install nova-api nova-conductor nova-novncproxy nova-scheduler
...
Setting up adwaita-icon-theme (3.36.1-2ubuntu0.20.04.2) ...
update-alternatives: using /usr/share/icons/Adwaita/cursor.theme to provide /usr/share/icons/default/index.theme (x-cursor-theme) in auto mode
Setting up libgtk-3-0:amd64 (3.24.20-0ubuntu1.1) ...
Setting up libgtk-3-bin (3.24.20-0ubuntu1.1) ...
Setting up libvte-2.91-0:amd64 (0.60.3-0ubuntu1~20.04) ...
Setting up humanity-icon-theme (0.6.15) ...
Setting up qemu-system-gui:amd64 (1:4.2-3ubuntu6.24) ...
Setting up ubuntu-mono (19.04-0ubuntu3) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
Processing triggers for libgdk-pixbuf2.0-0:amd64 (2.40.0+dfsg-3ubuntu0.4) ...

# cat  /etc/nova/nova.conf | grep -n -e "\[api_database" -e "\[database" -e "connection = " -e "\[api" -e "\[keystone_authtoken"
880:[api]
1087:[api_database]
1088:connection = sqlite:////var/lib/nova/nova_api.sqlite
1112:#connection = <None>
1116:#slave_connection = <None>
1784:[database]
1785:connection = sqlite:////var/lib/nova/nova.sqlite
1808:#connection = <None>
1812:#slave_connection = <None>
2721:[keystone_authtoken]

# cat  /etc/nova/nova.conf | grep -n -e "\[keystone_authtoken" -e "www_authenticate_uri"
2725:[keystone_authtoken]
2738:# Deprecated group/name - [keystone_authtoken]/auth_uri
2739:#www_authenticate_uri = <None>

# ip a | grep inet
    inet 127.0.0.1/8 scope host lo
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
    inet 192.168.56.101/24 brd 192.168.56.255 scope global eth1

# cat  /etc/nova/nova.conf | grep -n -e "\[vnc"
5391:[vnc]

# su -s /bin/sh -c "nova-manage api_db sync" nova
2023-04-08 06:27:59.010 135906 INFO alembic.runtime.migration [-] Context impl MySQLImpl.
2023-04-08 06:27:59.011 135906 INFO alembic.runtime.migration [-] Will assume non-transactional DDL.
2023-04-08 06:27:59.018 135906 INFO alembic.runtime.migration [-] Running upgrade  -> d67eeaabee36, Initial version
2023-04-08 06:27:59.303 135906 INFO alembic.runtime.migration [-] Running upgrade d67eeaabee36 -> b30f573d3377, Remove unused build_requests columns

# su -s /bin/sh -c "nova-manage cell_v2 map_cell0" nova

# su -s /bin/sh -c "nova-manage cell_v2 create_cell --name=cell1 --verbose" nova
--transport-url not provided in the command line, using the value [DEFAULT]/transport_url from the configuration file
--database_connection not provided in the command line, using the value [database]/connection from the configuration file
7b34bb8e-43d5-4566-861a-e8f15f0b3485

# su -s /bin/sh -c "nova-manage db sync" nova
ERROR: Could not access cell0.
Has the nova_api database been created?
Has the nova_cell0 database been created?
Has "nova-manage api_db sync" been run?
Has "nova-manage cell_v2 map_cell0" been run?
Is [api_database]/connection set in nova.conf?
Is the cell0 database connection URL correct?
Error: (pymysql.err.OperationalError) (1044, "Access denied for user 'nova'@'%' to database 'nova_cell0'")
(Background on this error at: https://sqlalche.me/e/14/e3q8)
```
* https://docs.openstack.org/nova/yoga/install/
* https://docs.openstack.org/nova/yoga/install/overview.html
* https://docs.openstack.org/nova/yoga/install/get-started-compute.html
* https://docs.openstack.org/nova/yoga/install/controller-install.html
* https://docs.openstack.org/nova/yoga/install/controller-install-ubuntu.html
* Replace NOVA_DBPASS with a suitable password.
* NOVA_PASS
* sudo rabbitmqctl add_user openstack rabbit
* https://linuxconfig.org/how-to-find-my-ip-address-on-ubuntu-20-04-focal-fossa-linux
* 

```
# su -s /bin/sh -c "nova-manage db sync" nova
ERROR: Could not access cell0.
Has the nova_api database been created?
Has the nova_cell0 database been created?
Has "nova-manage api_db sync" been run?
Has "nova-manage cell_v2 map_cell0" been run?
Is [api_database]/connection set in nova.conf?
Is the cell0 database connection URL correct?
Error: (pymysql.err.OperationalError) (1044, "Access denied for user 'nova'@'%' to database 'nova_cell0'")
(Background on this error at: https://sqlalche.me/e/14/e3q8)
root@controller:~# history | grep -e "nova-manage api_db sync" -e "nova-manage cell_v2 map_cell0"
  435  su -s /bin/sh -c "nova-manage api_db sync" nova
  436  su -s /bin/sh -c "nova-manage cell_v2 map_cell0" nova
  454  su -s /bin/sh -c "nova-manage cell_v2 map_cell0" nova
  463  history | grep -e "nova-manage api_db sync" -e "nova-manage cell_v2 map_cell0"
```


```
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 list_cells"
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
|  Name |                 UUID                 |              Transport URL               |               Database Connection               | Disabled |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
| cell0 | 00000000-0000-0000-0000-000000000000 |                  none:/                  | mysql+pymysql://nova:****@controller/nova_cell0 |  False   |
| cell1 | 7b34bb8e-43d5-4566-861a-e8f15f0b3485 | rabbit://openstack:****@controller:5672/ |    mysql+pymysql://nova:****@controller/nova    |  False   |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 delete_cell --cell_uuid 00000000-0000-0000-0000-000000000000"
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 list_cells"
+-------+--------------------------------------+------------------------------------------+-------------------------------------------+----------+
|  Name |                 UUID                 |              Transport URL               |            Database Connection            | Disabled |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------+----------+
| cell1 | 7b34bb8e-43d5-4566-861a-e8f15f0b3485 | rabbit://openstack:****@controller:5672/ | mysql+pymysql://nova:****@controller/nova |  False   |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------+----------+
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 delete_cell --cell_uuid 7b34bb8e-43d5-4566-861a-e8f15f0b3485"
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 list_cells"
+------+------+---------------+---------------------+----------+
| Name | UUID | Transport URL | Database Connection | Disabled |
+------+------+---------------+---------------------+----------+
+------+------+---------------+---------------------+----------+
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 map_cell0 --database_connection mysql+pymysql://nova:NOVA_DBPASS@controller/nova_cell0" nova
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 list_cells"
+-------+--------------------------------------+---------------+-------------------------------------------------+----------+
|  Name |                 UUID                 | Transport URL |               Database Connection               | Disabled |
+-------+--------------------------------------+---------------+-------------------------------------------------+----------+
| cell0 | 00000000-0000-0000-0000-000000000000 |     none:/    | mysql+pymysql://nova:****@controller/nova_cell0 |  False   |
+-------+--------------------------------------+---------------+-------------------------------------------------+----------+
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 create_cell --name=cell1 --verbose" nova
--transport-url not provided in the command line, using the value [DEFAULT]/transport_url from the configuration file
--database_connection not provided in the command line, using the value [database]/connection from the configuration file
81d81bac-c47d-41be-bab1-d33322449b6b
root@controller:~# su -s /bin/sh -c "nova-manage cell_v2 list_cells"
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
|  Name |                 UUID                 |              Transport URL               |               Database Connection               | Disabled |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
| cell0 | 00000000-0000-0000-0000-000000000000 |                  none:/                  | mysql+pymysql://nova:****@controller/nova_cell0 |  False   |
| cell1 | 81d81bac-c47d-41be-bab1-d33322449b6b | rabbit://openstack:****@controller:5672/ |    mysql+pymysql://nova:****@controller/nova    |  False   |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
```


```
# su -s /bin/sh -c "nova-manage db sync --local_cell" nova
2023-04-08 08:48:49.810 165942 INFO alembic.runtime.migration [-] Context impl MySQLImpl.
2023-04-08 08:48:49.811 165942 INFO alembic.runtime.migration [-] Will assume non-transactional DDL.
2023-04-08 08:48:49.816 165942 INFO alembic.runtime.migration [-] Running upgrade  -> 8f2f1571d55b, Initial version
2023-04-08 08:48:50.686 165942 INFO alembic.runtime.migration [-] Running upgrade 8f2f1571d55b -> 16f1fbcab42b, Resolve shadow table diffs
```


### compute
```
Get:294 http://us.archive.ubuntu.com/ubuntu focal-updates/main amd64 ovmf all 0~20191122.bd85bf54-2ubuntu3.4 [6,256 kB]                                                                    
Fetched 71.8 MB in 14s (5,126 kB/s)                                                                                                                                                        
E: Failed to fetch http://ubuntu-cloud.archive.canonical.com/ubuntu/pool/main/c/ceph/librados2_17.2.0-0ubuntu0.22.04.2~cloud0_amd64.deb  404  Not Found [IP: 185.125.190.36 80]
E: Failed to fetch http://ubuntu-cloud.archive.canonical.com/ubuntu/pool/main/c/ceph/librbd1_17.2.0-0ubuntu0.22.04.2~cloud0_amd64.deb  404  Not Found [IP: 185.125.190.36 80]
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
```
* https://docs.openstack.org/nova/yoga/install/compute-install-ubuntu.html
  * For simplicity, this configuration uses the Quick EMUlator (QEMU) hypervisor with the kernel-based VM (KVM) extension on compute nodes that support hardware acceleration for virtual machines. On legacy hardware, this configuration uses the generic QEMU hypervisor. You can follow these instructions with minor modifications to horizontally scale your environment with additional compute nodes.
  * 
* 

### compute
```
# cat  /etc/nova/nova.conf| grep -n -e "\[api" -e "\[keystone_authtoken"
881:[api]
1088:[api_database]
2722:[keystone_authtoken]
root@compute:~# vim /etc/nova/nova.conf
root@compute:~# cat  /etc/nova/nova.conf| grep -n -e "\[placement"
4353:[placement]

root@compute:~# service nova-compute restart
root@compute:~# systemctl status nova-compute 
● nova-compute.service - OpenStack Compute
     Loaded: loaded (/lib/systemd/system/nova-compute.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2023-04-08 09:08:00 UTC; 14s ago
   Main PID: 31636 (nova-compute)
      Tasks: 2 (limit: 9440)
     Memory: 120.5M
     CGroup: /system.slice/nova-compute.service
             └─31636 /usr/bin/python3 /usr/bin/nova-compute --config-file=/etc/nova/nova.conf --config-file=/etc/nova/nova-compute.conf --log-file=/var/log/nova/nova-compute.log

Apr 08 09:08:05 compute nova-compute[31636]:   File "/usr/lib/python3/dist-packages/eventlet/hubs/poll.py", line 111, in wait
Apr 08 09:08:05 compute nova-compute[31636]:     listener.cb(fileno)
Apr 08 09:08:05 compute nova-compute[31636]:   File "/usr/lib/python3/dist-packages/eventlet/greenthread.py", line 221, in main
Apr 08 09:08:05 compute nova-compute[31636]:     result = function(*args, **kwargs)
Apr 08 09:08:05 compute nova-compute[31636]:   File "/usr/lib/python3/dist-packages/nova/utils.py", line 656, in context_wrapper
Apr 08 09:08:05 compute nova-compute[31636]:     return func(*args, **kwargs)
Apr 08 09:08:05 compute nova-compute[31636]:   File "/usr/lib/python3/dist-packages/nova/context.py", line 427, in gather_result
Apr 08 09:08:05 compute nova-compute[31636]:     result = e.__class__(e.args)
Apr 08 09:08:05 compute nova-compute[31636]: TypeError: __init__() missing 2 required positional arguments: 'params' and 'orig'
Apr 08 09:08:05 compute nova-compute[31636]: Removing descriptor: 12
root@compute:~# cat /var/log/nova/nova-compute.log
2023-04-08 08:59:23.226 30886 INFO os_vif [-] Loaded VIF plugins: linux_bridge, noop, ovs
2023-04-08 08:59:23.293 30886 ERROR oslo.messaging._drivers.impl_rabbit [req-2978fd22-df49-4bb3-8e60-06b327b46ad5 - - - - -] Connection failed: [Errno 111] ECONNREFUSED (retrying in 1.0 seconds): ConnectionRefusedError: [Errno 111] ECONNREFUSED
2023-04-08 08:59:24.297 30886 ERROR oslo.messaging._drivers.impl_rabbit [req-2978fd22-df49-4bb3-8e60-06b327b46ad5 - - - - -] Connection failed: [Errno 111] ECONNREFUSED (retrying in 3.0 seconds): ConnectionRefusedError: [Errno 111] ECONNREFUSED
2023-04-08 08:59:27.322 30886 ERROR oslo.messaging._drivers.impl_rabbit [req-2978fd22-df49-4bb3-8e60-06b327b46ad5 - - - - -] Connection failed: [Errno 111] ECONNREFUSED (retrying in 5.0 seconds): ConnectionRefusedError: [Errno 111] ECONNREFUSED
```

### compute node ; after controller node is fixed
```
root@compute:~# systemctl status nova-compute 
● nova-compute.service - OpenStack Compute
     Loaded: loaded (/lib/systemd/system/nova-compute.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2023-04-08 09:18:37 UTC; 4s ago
   Main PID: 31861 (nova-compute)
      Tasks: 3 (limit: 9440)
     Memory: 120.6M
     CGroup: /system.slice/nova-compute.service
             └─31861 /usr/bin/python3 /usr/bin/nova-compute --config-file=/etc/nova/nova.conf --config-file=/etc/nova/nova-compute.conf --log-file=/var/log/nova/nova-compute.log

Apr 08 09:18:39 compute nova-compute[31861]:   File "/usr/lib/python3/dist-packages/eventlet/hubs/poll.py", line 111, in wait
Apr 08 09:18:39 compute nova-compute[31861]:     listener.cb(fileno)
Apr 08 09:18:39 compute nova-compute[31861]:   File "/usr/lib/python3/dist-packages/eventlet/greenthread.py", line 221, in main
Apr 08 09:18:39 compute nova-compute[31861]:     result = function(*args, **kwargs)
Apr 08 09:18:39 compute nova-compute[31861]:   File "/usr/lib/python3/dist-packages/nova/utils.py", line 656, in context_wrapper
Apr 08 09:18:39 compute nova-compute[31861]:     return func(*args, **kwargs)
Apr 08 09:18:39 compute nova-compute[31861]:   File "/usr/lib/python3/dist-packages/nova/context.py", line 427, in gather_result
Apr 08 09:18:39 compute nova-compute[31861]:     result = e.__class__(e.args)
Apr 08 09:18:39 compute nova-compute[31861]: TypeError: __init__() missing 2 required positional arguments: 'params' and 'orig'
Apr 08 09:18:39 compute nova-compute[31861]: Removing descriptor: 12
root@compute:~# service nova-compute restart
root@compute:~# systemctl status nova-compute 
● nova-compute.service - OpenStack Compute
     Loaded: loaded (/lib/systemd/system/nova-compute.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2023-04-08 09:24:52 UTC; 1s ago
   Main PID: 31928 (nova-compute)
      Tasks: 1 (limit: 9440)
     Memory: 96.3M
     CGroup: /system.slice/nova-compute.service
             └─31928 /usr/bin/python3 /usr/bin/nova-compute --config-file=/etc/nova/nova.conf --config-file=/etc/nova/nova-compute.conf --log-file=/var/log/nova/nova-compute.log

Apr 08 09:24:52 compute systemd[1]: Started OpenStack Compute.
```

### controller node
```
  584  openstack compute service list --service nova-compute
  585  su -s /bin/sh -c "nova-manage db purge" nova
  586  su -s /bin/sh -c "nova-manage db purge --all" nova
  587  history
  588  su -s /bin/sh -c "nova-manage cell_v2 delete_cell --cell_uuid 00000000-0000-0000-0000-000000000000"
  589  su -s /bin/sh -c "nova-manage cell_v2 list_cells" nova
  590  su -s /bin/sh -c "nova-manage cell_v2 delete_cell --cell_uuid 13f0f23b-9ead-4e9b-9ec8-bfcf31723c48"
  591  su -s /bin/sh -c "nova-manage db purge" nova
  592  su -s /bin/sh -c "nova-manage db purge --all" nova
  593  su -s /bin/sh -c "nova-manage api_db sync" nova
  594  su -s /bin/sh -c "nova-manage cell_v2 map_cell0" nova
  595  su -s /bin/sh -c "nova-manage cell_v2 create_cell --name=cell1"
  596  su -s /bin/sh -c "nova-manage db sync" nova
  597  history
root@controller:/home/vagrant# su -s /bin/sh -c "nova-manage cell_v2 list_cells" nova
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
|  Name |                 UUID                 |              Transport URL               |               Database Connection               | Disabled |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
| cell0 | 00000000-0000-0000-0000-000000000000 |                  none:/                  | mysql+pymysql://nova:****@controller/nova_cell0 |  False   |
| cell1 | 4561ddd3-166a-417b-a45d-f6fb149fb4f5 | rabbit://openstack:****@controller:5672/ |    mysql+pymysql://nova:****@controller/nova    |  False   |
+-------+--------------------------------------+------------------------------------------+-------------------------------------------------+----------+
root@controller:/home/vagrant# service nova-api restart
root@controller:/home/vagrant# service nova-scheduler restart
root@controller:/home/vagrant# service nova-conductor restart
root@controller:/home/vagrant# service nova-novncproxy restart
root@controller:/home/vagrant# openstack compute service list --service nova-compute
+--------------------------------------+--------------+---------+------+---------+-------+----------------------------+
| ID                                   | Binary       | Host    | Zone | Status  | State | Updated At                 |
+--------------------------------------+--------------+---------+------+---------+-------+----------------------------+
| da72a0bf-9f9b-4458-aa98-796a33585c6e | nova-compute | compute | nova | enabled | up    | 2023-04-08T09:25:09.000000 |
+--------------------------------------+--------------+---------+------+---------+-------+----------------------------+
root@controller:/home/vagrant# su -s /bin/sh -c "nova-manage cell_v2 discover_hosts --verbose" nova
Found 2 cell mappings.
Skipping cell0 since it does not contain hosts.
Getting computes from cell 'cell1': 4561ddd3-166a-417b-a45d-f6fb149fb4f5
Checking host mapping for compute host 'compute': b7ac7f82-fdf3-4ab7-aebf-0ed782dedaae
Creating host mapping for compute host 'compute': b7ac7f82-fdf3-4ab7-aebf-0ed782dedaae
Found 1 unmapped computes in cell: 4561ddd3-166a-417b-a45d-f6fb149fb4f5
root@controller:/home/vagrant# 

```


### nova - Verify operation
```
root@controller:/home/vagrant# openstack compute service list
+--------------------------------------+----------------+------------+----------+---------+-------+----------------------------+
| ID                                   | Binary         | Host       | Zone     | Status  | State | Updated At                 |
+--------------------------------------+----------------+------------+----------+---------+-------+----------------------------+
| a6a84c90-4532-4551-92ec-af8e1f3f2315 | nova-scheduler | controller | internal | enabled | up    | 2023-04-08T09:32:03.000000 |
| c7a648e0-b1c7-4627-beae-841a5f17abd1 | nova-conductor | controller | internal | enabled | up    | 2023-04-08T09:32:06.000000 |
| da72a0bf-9f9b-4458-aa98-796a33585c6e | nova-compute   | compute    | nova     | enabled | up    | 2023-04-08T09:32:10.000000 |
+--------------------------------------+----------------+------------+----------+---------+-------+----------------------------+

root@compute:/home/vagrant# openstack compute service list
+--------------------------------------+----------------+------------+----------+---------+-------+----------------------------+
| ID                                   | Binary         | Host       | Zone     | Status  | State | Updated At                 |
+--------------------------------------+----------------+------------+----------+---------+-------+----------------------------+
| a6a84c90-4532-4551-92ec-af8e1f3f2315 | nova-scheduler | controller | internal | enabled | up    | 2023-04-08T09:34:13.000000 |
| c7a648e0-b1c7-4627-beae-841a5f17abd1 | nova-conductor | controller | internal | enabled | up    | 2023-04-08T09:34:16.000000 |
| da72a0bf-9f9b-4458-aa98-796a33585c6e | nova-compute   | compute    | nova     | enabled | up    | 2023-04-08T09:34:10.000000 |
+--------------------------------------+----------------+------------+----------+---------+-------+----------------------------+
root@compute:/home/vagrant# openstack catalog list
+-----------+-----------+-----------------------------------------+
| Name      | Type      | Endpoints                               |
+-----------+-----------+-----------------------------------------+
| nova      | compute   | RegionOne                               |
|           |           |   public: http://controller:8774/v2.1   |
|           |           | RegionOne                               |
|           |           |   internal: http://controller:8774/v2.1 |
|           |           | RegionOne                               |
|           |           |   admin: http://controller:8774/v2.1    |
|           |           |                                         |
| glance    | image     | RegionOne                               |
|           |           |   internal: http://controller:9292      |
|           |           | RegionOne                               |
|           |           |   public: http://controller:9292        |
|           |           | RegionOne                               |
|           |           |   admin: http://controller:9292         |
|           |           | RegionOne                               |
|           |           |   public: http://controller:9292        |
|           |           |                                         |
| placement | placement | RegionOne                               |
|           |           |   public: http://controller:8778        |
|           |           | RegionOne                               |
|           |           |   admin: http://controller:8778         |
|           |           | RegionOne                               |
|           |           |   internal: http://controller:8778      |
|           |           |                                         |
| keystone  | identity  | RegionOne                               |
|           |           |   internal: http://controller:5000/v3/  |
|           |           | RegionOne                               |
|           |           |   public: http://controller:5000/v3/    |
|           |           | RegionOne                               |
|           |           |   admin: http://controller:5000/v3/     |
|           |           |                                         |
+-----------+-----------+-----------------------------------------+

# openstack image list
+--------------------------------------+--------+--------+
| ID                                   | Name   | Status |
+--------------------------------------+--------+--------+
| d6fc5ad0-4076-4cc3-83b3-33ef4a8efecd | cirros | active |
+--------------------------------------+--------+--------+

```
* https://docs.openstack.org/nova/yoga/install/verify.html
* 
### solved the "nova_cell0 access denied" error by executing the related sql again
```
  546  su -s /bin/sh -c "nova-manage cell_v2 create_cell --name=cell1 --database_connection mysql+pymysql://nova:NOVA_DBPASS@controller/nova_cell1?charset=utf8 --transport-url rabbit://openstack:rabbit@controller:5672/nova_cell1  --verbose" nova
  573  history | grep mysql
root@controller:/home/vagrant# mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 143
Server version: 10.3.38-MariaDB-0ubuntu0.20.04.1 Ubuntu 20.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CREATE DATABASE nova_cell0;
ERROR 1007 (HY000): Can't create database 'nova_cell0'; database exists
MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova_cell0.* TO 'nova'@'localhost' \
    ->   IDENTIFIED BY 'NOVA_DBPASS';
Query OK, 0 rows affected (0.000 sec)

MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova_cell0.* TO 'nova'@'%' \
    ->   IDENTIFIED BY 'NOVA_DBPASS';
Query OK, 0 rows affected (0.000 sec)

MariaDB [(none)]> quit
Bye
root@controller:/home/vagrant# su -s /bin/sh -c "nova-manage db sync" nova
```

## neutron
```
$ vagrant --version
Vagrant 2.2.14

$ git commit -m "fixed MEMORY_GB, add controller2"
[master f4c07ff] fixed MEMORY_GB, add controller2
 2 files changed, 18 insertions(+), 5 deletions(-)


```
* https://docs.openstack.org/neutron/yoga/install/
* https://docs.openstack.org/install-guide/openstack-services.html#minimal-deployment-for-yoga
* https://docs.openstack.org/neutron/yoga/install/concepts.html
  * Additionally, you can allocate IP addresses on external networks to ports on the internal network. Whenever something is connected to a subnet, that connection is called a port. You can associate external network IP addresses with ports to VMs. This way, entities on the outside network can access VMs.
  * Virtual Networking Infrastructure (VNI)
  * Each plug-in that Networking uses has its own concepts. While not vital to operating the VNI and OpenStack environment, understanding these concepts can help you set up Networking. All Networking installations use a core plug-in and a security group plug-in (or just the No-Op security group plug-in).
* https://stackoverflow.com/questions/23957752/vagrant-how-to-configure-multiple-nics-within-a-vagrantfile
* https://docs.openstack.org/neutron/yoga/install/environment-networking-controller-ubuntu.html
* https://docs.openstack.org/install-guide/environment-networking-controller.html
* 

```
vim Vagrantfile
      df.vm.network "public_network", auto_config: false

# nova-status upgrade check

vim /etc/netplan/50-vagrant.yaml 
netplan generate
netplan apply
```
* https://unix.stackexchange.com/questions/128439/good-detailed-explanation-of-etc-network-interfaces-syntax
* https://manpages.ubuntu.com/manpages/focal/man8/netplan-generate.8.html
* https://netplan.io/examples
* 

### compute node
```
root@controller:/home/vagrant# openstack compute service list

root@compute:~# ping -c 4 controller
PING controller (192.168.56.101) 56(84) bytes of data.
64 bytes from controller (192.168.56.101): icmp_seq=1 ttl=64 time=0.251 ms
64 bytes from controller (192.168.56.101): icmp_seq=2 ttl=64 time=0.367 ms
64 bytes from controller (192.168.56.101): icmp_seq=3 ttl=64 time=0.304 ms
64 bytes from controller (192.168.56.101): icmp_seq=4 ttl=64 time=0.360 ms
```
* https://docs.openstack.org/neutron/yoga/install/environment-networking-compute-ubuntu.html
* 

### controller node
```
# mysql -u root -p

CREATE DATABASE neutron;
GRANT ALL PRIVILEGES ON neutron.* TO 'neutron'@'localhost' \
  IDENTIFIED BY 'NEUTRON_DBPASS';
GRANT ALL PRIVILEGES ON neutron.* TO 'neutron'@'%' \
  IDENTIFIED BY 'NEUTRON_DBPASS';

# . admin-openrc
# openstack user create --domain default --password-prompt neutron
User Password:
Repeat User Password:
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| enabled             | True                             |
| id                  | 87ab44f576024fe7ba7c2a8719c1af10 |
| name                | neutron                          |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+

# openstack role add --project service --user neutron admin
# openstack service create --name neutron \
>   --description "OpenStack Networking" network
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | OpenStack Networking             |
| enabled     | True                             |
| id          | 7e3e46fa4d824ac2885e305021047c2e |
| name        | neutron                          |
| type        | network                          |
+-------------+----------------------------------+
# openstack endpoint create --region RegionOne \
>   network public http://controller:9696
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 27d7f1fe2bab498dbd282920626309d5 |
| interface    | public                           |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 7e3e46fa4d824ac2885e305021047c2e |
| service_name | neutron                          |
| service_type | network                          |
| url          | http://controller:9696           |
+--------------+----------------------------------+

# openstack endpoint create --region RegionOne \
>   network internal http://controller:9696
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 64dd00e938fd40fd90b495c664c30334 |
| interface    | internal                         |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 7e3e46fa4d824ac2885e305021047c2e |
| service_name | neutron                          |
| service_type | network                          |
| url          | http://controller:9696           |
+--------------+----------------------------------+

# openstack endpoint create --region RegionOne \
>   network admin http://controller:9696
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 45ff3edb6048412fb07f035f21544732 |
| interface    | admin                            |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 7e3e46fa4d824ac2885e305021047c2e |
| service_name | neutron                          |
| service_type | network                          |
| url          | http://controller:9696           |
+--------------+----------------------------------+

```
* https://docs.openstack.org/neutron/yoga/install/controller-install-ubuntu.html
* NEUTRON_PASS
* 

```
# apt install neutron-server neutron-plugin-ml2 \
  neutron-linuxbridge-agent neutron-l3-agent neutron-dhcp-agent \
  neutron-metadata-agent
Setting up neutron-l3-agent (2:20.2.0-0ubuntu1~cloud0) ...
Created symlink /etc/systemd/system/multi-user.target.wants/neutron-l3-agent.service → /lib/systemd/system/neutron-l3-agent.service.
Processing triggers for rsyslog (8.2001.0-1ubuntu1.3) ...
Processing triggers for systemd (245.4-4ubuntu3.20) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for dbus (1.12.16-2ubuntu2.3) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...

# cat /etc/neutron/neutron.conf | grep -e "\[database" -n -e "connection = "
819:[database]
820:connection = sqlite:////var/lib/neutron/neutron.sqlite
846:#connection = <None>
850:#slave_connection = <None>

# vim /etc/neutron/plugins/ml2/ml2_conf.ini
# cat /etc/neutron/plugins/ml2/ml2_conf.ini | grep -n -e "\[ml2" -e "type_drivers = " -e "tenant_network_types ="
153:[ml2]
154:type_drivers = flat,vlan,vxlan
155:tenant_network_types = vxlan
164:#type_drivers = local,flat,vlan,gre,vxlan,geneve
169:#tenant_network_types = local
205:[ml2_type_flat]
217:[ml2_type_geneve]
236:[ml2_type_gre]
247:[ml2_type_vlan]
261:[ml2_type_vxlan]

# vim /etc/neutron/plugins/ml2/linuxbridge_agent.ini

root@controller:/home/vagrant# sysctl net.bridge.bridge-nf-call-iptables
net.bridge.bridge-nf-call-iptables = 1
root@controller:/home/vagrant# sysctl net.bridge.bridge-nf-call-ip6tables
net.bridge.bridge-nf-call-ip6tables = 1

# vim  /etc/neutron/l3_agent.ini
# vim /etc/neutron/dhcp_agent.ini

```
* https://docs.openstack.org/neutron/yoga/install/controller-install-ubuntu.html
  * Choose one of the following networking options to configure services specific to it. Afterwards, return here and proceed to Configure the metadata agent.
* https://docs.openstack.org/neutron/yoga/install/controller-install-option2-ubuntu.html
* 

```
# vim /etc/neutron/metadata_agent.ini

# cat /etc/nova/nova.conf | grep -n -e "\[neutron" -e "auth_url = "

# vim /etc/nova/nova.conf
# cat /etc/nova/nova.conf | grep -n -e "\[neutron" -e "auth_url = " -e "\[notifications"
...
3550:[neutron]
3551:auth_url = http://controller:5000
3637:# Deprecated group/name - [neutron]/auth_plugin
3644:#auth_url = <None>
3684:# Deprecated group/name - [neutron]/user_name
3739:[notifications]
4373:auth_url = http://controller:5000/v3
...

# su -s /bin/sh -c "neutron-db-manage --config-file /etc/neutron/neutron.conf \
>   --config-file /etc/neutron/plugins/ml2/ml2_conf.ini upgrade head" neutron
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
  Running upgrade for neutron ...
INFO  [alembic.runtime.migration] Context impl MySQLImpl.
INFO  [alembic.runtime.migration] Will assume non-transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> kilo
INFO  [alembic.runtime.migration] Running upgrade kilo -> 354db87e3225
INFO  [alembic.runtime.migration] Running upgrade 354db87e3225 -> 599c6a226151
INFO  [alembic.runtime.migration] Running upgrade 599c6a226151 -> 52c5312f6baf
INFO  [alembic.runtime.migration] Running upgrade 52c5312f6baf -> 313373c0ffee
INFO  [alembic.runtime.migration] Running upgrade 313373c0ffee -> 8675309a5c4f
INFO  [alembic.runtime.migration] Running upgrade 8675309a5c4f -> 45f955889773
INFO  [alembic.runtime.migration] Running upgrade 45f955889773 -> 26c371498592
INFO  [alembic.runtime.migration] Running upgrade 26c371498592 -> 1c844d1677f7
INFO  [alembic.runtime.migration] Running upgrade 1c844d1677f7 -> 1b4c6e320f79
INFO  [alembic.runtime.migration] Running upgrade 1b4c6e320f79 -> 48153cb5f051
INFO  [alembic.runtime.migration] Running upgrade 48153cb5f051 -> 9859ac9c136
INFO  [alembic.runtime.migration] Running upgrade 9859ac9c136 -> 34af2b5c5a59
...
INFO  [alembic.runtime.migration] Running upgrade 61663558142c -> 867d39095bf4, port forwarding
INFO  [alembic.runtime.migration] Running upgrade 867d39095bf4 -> d72db3e25539, modify uniq port forwarding
INFO  [alembic.runtime.migration] Running upgrade d72db3e25539 -> cada2437bf41
INFO  [alembic.runtime.migration] Running upgrade cada2437bf41 -> 195176fb410d, router gateway IP QoS
...
INFO  [alembic.runtime.migration] Running upgrade 8df53b0d2c0e -> 1bb3393de75d, add qos policy rule Packet Rate Limit
INFO  [alembic.runtime.migration] Running upgrade 1bb3393de75d -> c181bb1d89e4
INFO  [alembic.runtime.migration] Running upgrade c181bb1d89e4 -> ba859d649675
INFO  [alembic.runtime.migration] Running upgrade ba859d649675 -> e981acd076d3
INFO  [alembic.runtime.migration] Running upgrade e981acd076d3 -> 76df7844a8c6, add Local IP tables
INFO  [alembic.runtime.migration] Running upgrade 76df7844a8c6 -> 1ffef8d6f371, migrate RBAC registers from "target_tenant" to "target_project"
INFO  [alembic.runtime.migration] Running upgrade 1ffef8d6f371 -> 8160f7a9cebb, drop portbindingports table
INFO  [alembic.runtime.migration] Running upgrade 8160f7a9cebb -> cd9ef14ccf87
INFO  [alembic.runtime.migration] Running upgrade cd9ef14ccf87 -> 34cf8b009713
INFO  [alembic.runtime.migration] Running upgrade 7d9d8eeec6ad -> a8b517cff8ab
INFO  [alembic.runtime.migration] Running upgrade a8b517cff8ab -> 3b935b28e7a0
INFO  [alembic.runtime.migration] Running upgrade 3b935b28e7a0 -> b12a3ef66e62
INFO  [alembic.runtime.migration] Running upgrade b12a3ef66e62 -> 97c25b0d2353
INFO  [alembic.runtime.migration] Running upgrade 97c25b0d2353 -> 2e0d7a8a1586
INFO  [alembic.runtime.migration] Running upgrade 2e0d7a8a1586 -> 5c85685d616d
  OK

# service nova-api restart
root@controller:/home/vagrant# systemctl status nova-api
● nova-api.service - OpenStack Compute API
     Loaded: loaded (/lib/systemd/system/nova-api.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:05:26 UTC; 8s ago
       Docs: man:nova-api(1)
   Main PID: 39405 (nova-api)
      Tasks: 5 (limit: 7021)
     Memory: 217.3M
     CGroup: /system.slice/nova-api.service
             ├─39405 /usr/bin/python3 /usr/bin/nova-api --config-file=/etc/nova/nova.conf --log-file=/var/log/nova/nova-api.log
             ├─39427 /usr/bin/python3 /usr/bin/nova-api --config-file=/etc/nova/nova.conf --log-file=/var/log/nova/nova-api.log
             ├─39428 /usr/bin/python3 /usr/bin/nova-api --config-file=/etc/nova/nova.conf --log-file=/var/log/nova/nova-api.log
             ├─39429 /usr/bin/python3 /usr/bin/nova-api --config-file=/etc/nova/nova.conf --log-file=/var/log/nova/nova-api.log
             └─39430 /usr/bin/python3 /usr/bin/nova-api --config-file=/etc/nova/nova.conf --log-file=/var/log/nova/nova-api.log

Apr 10 08:05:26 controller systemd[1]: Started OpenStack Compute API.

# service neutron-server restart
# service neutron-linuxbridge-agent restart
# service neutron-dhcp-agent restart
# systemctl status neutron-dhcp-agent
● neutron-dhcp-agent.service - OpenStack Neutron DHCP agent
     Loaded: loaded (/lib/systemd/system/neutron-dhcp-agent.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:06:46 UTC; 13s ago
       Docs: man:neutron-dhcp-agent(1)
   Main PID: 39597 (neutron-dhcp-ag)
      Tasks: 3 (limit: 7021)
     Memory: 107.8M
     CGroup: /system.slice/neutron-dhcp-agent.service
             └─39597 neutron-dhcp-agent (/usr/bin/python3 /usr/bin/neutron-dhcp-agent --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/dhcp_agent.ini --log-file=/v>

Apr 10 08:06:46 controller systemd[1]: Started OpenStack Neutron DHCP agent.

# service neutron-metadata-agent restart
# systemctl status neutron-metadata-agent
● neutron-metadata-agent.service - OpenStack Neutron Metadata Agent
     Loaded: loaded (/lib/systemd/system/neutron-metadata-agent.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:07:43 UTC; 11s ago
       Docs: man:neutron-metadata-agent(1)
   Main PID: 39676 (neutron-metadat)
      Tasks: 3 (limit: 7021)
     Memory: 116.7M
     CGroup: /system.slice/neutron-metadata-agent.service
             ├─39676 neutron-metadata-agent (/usr/bin/python3 /usr/bin/neutron-metadata-agent --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/metadata_agent.ini ->
             └─39703 neutron-metadata-agent (/usr/bin/python3 /usr/bin/neutron-metadata-agent --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/metadata_agent.ini ->

Apr 10 08:07:43 controller systemd[1]: Started OpenStack Neutron Metadata Agent.

# service neutron-l3-agent restart
# systemctl status neutron-l3-agent
● neutron-l3-agent.service - OpenStack Neutron L3 agent
     Loaded: loaded (/lib/systemd/system/neutron-l3-agent.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:08:42 UTC; 22s ago
       Docs: man:neutron-l3-agent(1)
   Main PID: 39753 (neutron-l3-agen)
      Tasks: 4 (limit: 7021)
     Memory: 176.4M
     CGroup: /system.slice/neutron-l3-agent.service
             ├─39753 neutron-l3-agent (/usr/bin/python3 /usr/bin/neutron-l3-agent --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/l3_agent.ini --log-file=/var/log>
             └─39788 /usr/bin/python3 /bin/privsep-helper --config-file /etc/neutron/neutron.conf --config-file /etc/neutron/l3_agent.ini --privsep_context neutron.privileged.namesp>

Apr 10 08:08:42 controller systemd[1]: Started OpenStack Neutron L3 agent.
Apr 10 08:08:43 controller sudo[39784]:  neutron : TTY=unknown ; PWD=/var/lib/neutron ; USER=root ; COMMAND=/usr/bin/neutron-rootwrap /etc/neutron/rootwrap.conf privsep-helper --con>
Apr 10 08:08:43 controller sudo[39784]: pam_unix(sudo:session): session opened for user root by (uid=0)
Apr 10 08:08:43 controller sudo[39784]: pam_unix(sudo:session): session closed for user root

```
* https://docs.openstack.org/neutron/yoga/install/controller-install-ubuntu.html
* https://docs.openstack.org/nova/yoga/install/controller-install-ubuntu.html
  * Configure the [neutron] section of /etc/nova/nova.conf. Refer to the Networking service install guide for more information.
* 

### compute node
```
# apt install neutron-linuxbridge-agent
...
Adding system user `neutron' (UID 120) ...
Adding new user `neutron' (UID 120) with group `neutron' ...
Not creating home directory `/var/lib/neutron'.
Setting up python3-neutron-lib (2.20.0-0ubuntu1~cloud0) ...
Setting up python3-neutron (2:20.2.0-0ubuntu1~cloud0) ...
Setting up neutron-linuxbridge-agent (2:20.2.0-0ubuntu1~cloud0) ...
Created symlink /etc/systemd/system/multi-user.target.wants/neutron-linuxbridge-cleanup.service → /lib/systemd/system/neutron-linuxbridge-cleanup.service.
Created symlink /etc/systemd/system/multi-user.target.wants/neutron-linuxbridge-agent.service → /lib/systemd/system/neutron-linuxbridge-agent.service.
Processing triggers for systemd (245.4-4ubuntu3.20) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...

# cat /etc/neutron/neutron.conf | grep -n -e "\[database" -e "connection "
...
819:[database]
820:connection = sqlite:////var/lib/neutron/neutron.sqlite
841:# The SQLAlchemy connection string to use to connect to the database. (string
846:#connection = <None>

```
* https://docs.openstack.org/neutron/yoga/install/compute-install-ubuntu.html

### Networking Option 2: Self-service networks
```
# cat /etc/neutron/plugins/ml2/linuxbridge_agent.ini | grep -n -e "\[linux_bridge"
# cat /etc/neutron/plugins/ml2/linuxbridge_agent.ini | grep -n -e "\[securitygroup"
# vim /etc/neutron/plugins/ml2/linuxbridge_agent.ini
# sysctl net.bridge.bridge-nf-call-iptables
# sysctl net.bridge.bridge-nf-call-ip6tables
```
* https://docs.openstack.org/neutron/yoga/install/compute-install-option2-ubuntu.html
* 

```
# cat /etc/nova/nova.conf  | grep -n -e "\[neutron" -e "auth_url = "
...
2727:auth_url = http://controller:5000/
3547:[neutron]
3623:# Deprecated group/name - [neutron]/auth_plugin
3630:#auth_url = <None>
3670:# Deprecated group/name - [neutron]/user_name
4359:auth_url = http://controller:5000/v3

# vim /etc/nova/nova.conf
# cat /etc/nova/nova.conf  | grep -n -e "\[neutron" -e "auth_url = "
...
2727:auth_url = http://controller:5000/
3547:[neutron]
3548:auth_url = http://controller:5000
3632:# Deprecated group/name - [neutron]/auth_plugin

# service nova-compute restart
# systemctl status nova-compute
● nova-compute.service - OpenStack Compute
     Loaded: loaded (/lib/systemd/system/nova-compute.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:46:02 UTC; 9s ago
   Main PID: 3106 (nova-compute)
      Tasks: 24 (limit: 9440)
     Memory: 122.3M
     CGroup: /system.slice/nova-compute.service
             └─3106 /usr/bin/python3 /usr/bin/nova-compute --config-file=/etc/nova/nova.conf --config-file=/etc/nova/nova-compute.conf --log-file=/var/log/nova/nova-compute.log

Apr 10 08:46:02 compute systemd[1]: Started OpenStack Compute.

# service neutron-linuxbridge-agent restart
# systemctl status neutron-linuxbridge-agent
● neutron-linuxbridge-agent.service - Openstack Neutron Linux Bridge Agent
     Loaded: loaded (/lib/systemd/system/neutron-linuxbridge-agent.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:46:58 UTC; 11s ago
    Process: 3171 ExecStartPre=/bin/mkdir -p /var/lock/neutron /var/log/neutron /var/lib/neutron (code=exited, status=0/SUCCESS)
    Process: 3174 ExecStartPre=/bin/chown neutron:neutron /var/lock/neutron /var/log/neutron /var/lib/neutron (code=exited, status=0/SUCCESS)
    Process: 3191 ExecStartPre=/sbin/modprobe br_netfilter (code=exited, status=0/SUCCESS)
   Main PID: 3195 (neutron-linuxbr)
      Tasks: 7 (limit: 9440)
     Memory: 249.3M
     CGroup: /system.slice/neutron-linuxbridge-agent.service
             ├─3195 neutron-linuxbridge-agent (/usr/bin/python3 /usr/bin/neutron-linuxbridge-agent --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/lin>
             ├─3218 /usr/bin/python3 /bin/privsep-helper --config-file /etc/neutron/neutron.conf --config-file /etc/neutron/plugins/ml2/linuxbridge_agent.ini --privsep_context neutr>
             └─3248 /usr/bin/python3 /bin/privsep-helper --config-file /etc/neutron/neutron.conf --config-file /etc/neutron/plugins/ml2/linuxbridge_agent.ini --privsep_context neutr>

Apr 10 08:46:58 compute systemd[1]: Starting Openstack Neutron Linux Bridge Agent...
Apr 10 08:46:58 compute systemd[1]: Started Openstack Neutron Linux Bridge Agent.
Apr 10 08:47:00 compute sudo[3211]:  neutron : TTY=unknown ; PWD=/var/lib/neutron ; USER=root ; COMMAND=/usr/bin/neutron-rootwrap /etc/neutron/rootwrap.conf privsep-helper --config->
Apr 10 08:47:00 compute sudo[3211]: pam_unix(sudo:session): session opened for user root by (uid=0)
Apr 10 08:47:00 compute sudo[3211]: pam_unix(sudo:session): session closed for user root
Apr 10 08:47:01 compute sudo[3239]:  neutron : TTY=unknown ; PWD=/var/lib/neutron ; USER=root ; COMMAND=/usr/bin/neutron-rootwrap /etc/neutron/rootwrap.conf privsep-helper --config->
Apr 10 08:47:01 compute sudo[3239]: pam_unix(sudo:session): session opened for user root by (uid=0)
Apr 10 08:47:01 compute sudo[3239]: pam_unix(sudo:session): session closed for user root

```
* https://docs.openstack.org/neutron/yoga/install/compute-install-ubuntu.html
* 

```
# apt install openvswitch
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package openvswitch
# apt install ovn-central
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  ovn-common
The following NEW packages will be installed:
  ovn-central ovn-common
0 upgraded, 2 newly installed, 0 to remove and 27 not upgraded.
Need to get 2,633 kB of archives.
After this operation, 13.0 MB of additional disk space will be used.
Do you want to continue? [Y/n] 
Get:1 http://ubuntu-cloud.archive.canonical.com/ubuntu focal-updates/yoga/main amd64 ovn-common amd64 22.03.0-0ubuntu1~cloud0 [1,658 kB]
Get:2 http://ubuntu-cloud.archive.canonical.com/ubuntu focal-updates/yoga/main amd64 ovn-central amd64 22.03.0-0ubuntu1~cloud0 [975 kB]
...
Setting up ovn-common (22.03.0-0ubuntu1~cloud0) ...
Setting up ovn-central (22.03.0-0ubuntu1~cloud0) ...
Created symlink /etc/systemd/system/ovn-sb-ovsdb.service → /lib/systemd/system/ovn-ovsdb-server-sb.service.
Created symlink /etc/systemd/system/ovn-nb-ovsdb.service → /lib/systemd/system/ovn-ovsdb-server-nb.service.
Created symlink /etc/systemd/system/multi-user.target.wants/ovn-central.service → /lib/systemd/system/ovn-central.service.
ovn-northd.service is a disabled or a static unit, not starting it.
Processing triggers for man-db (2.9.1-1) ...

# apt install ovn-host
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  openvswitch-switch
The following NEW packages will be installed:
  openvswitch-switch ovn-host
0 upgraded, 2 newly installed, 0 to remove and 27 not upgraded.
Need to get 2,630 kB of archives.
After this operation, 11.4 MB of additional disk space will be used.
...
Created symlink /etc/systemd/system/multi-user.target.wants/openvswitch-switch.service → /lib/systemd/system/openvswitch-switch.service.
Created symlink /etc/systemd/system/openvswitch-switch.service.requires/ovs-record-hostname.service → /lib/systemd/system/ovs-record-hostname.service.
Setting up ovn-host (22.03.0-0ubuntu1~cloud0) ...
Created symlink /etc/systemd/system/multi-user.target.wants/ovn-host.service → /lib/systemd/system/ovn-host.service.
ovn-controller.service is a disabled or a static unit, not starting it.
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.20) ...

# apt install ovn-docker
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  ovn-docker
0 upgraded, 1 newly installed, 0 to remove and 27 not upgraded.
Need to get 33.0 kB of archives.
After this operation, 72.7 kB of additional disk space will be used.
Get:1 http://ubuntu-cloud.archive.canonical.com/ubuntu focal-updates/yoga/main amd64 ovn-docker amd64 22.03.0-0ubuntu1~cloud0 [33.0 kB]
Fetched 33.0 kB in 1s (35.3 kB/s)     
Selecting previously unselected package ovn-docker.
(Reading database ... 96444 files and directories currently installed.)
Preparing to unpack .../ovn-docker_22.03.0-0ubuntu1~cloud0_amd64.deb ...
Unpacking ovn-docker (22.03.0-0ubuntu1~cloud0) ...
Setting up ovn-docker (22.03.0-0ubuntu1~cloud0) ...

# apt install ovn-common
Reading package lists... Done
Building dependency tree       
Reading state information... Done
ovn-common is already the newest version (22.03.0-0ubuntu1~cloud0).
ovn-common set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 27 not upgraded.

# systemctl status openvswitch
Unit openvswitch.service could not be found.

# systemctl status openvswitch-switch
● openvswitch-switch.service - Open vSwitch
     Loaded: loaded (/lib/systemd/system/openvswitch-switch.service; enabled; vendor preset: enabled)
     Active: active (exited) since Mon 2023-04-10 08:56:44 UTC; 9min ago
   Main PID: 42659 (code=exited, status=0/SUCCESS)
      Tasks: 0 (limit: 7021)
     Memory: 0B
     CGroup: /system.slice/openvswitch-switch.service

Apr 10 08:56:44 controller systemd[1]: Starting Open vSwitch...
Apr 10 08:56:44 controller systemd[1]: Finished Open vSwitch.
# systemctl status ovs-vswitchd
● ovs-vswitchd.service - Open vSwitch Forwarding Unit
     Loaded: loaded (/lib/systemd/system/ovs-vswitchd.service; static; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:56:43 UTC; 9min ago
   Main PID: 42571 (ovs-vswitchd)
      Tasks: 4 (limit: 7021)
     Memory: 28.2M
     CGroup: /system.slice/ovs-vswitchd.service
             └─42571 ovs-vswitchd unix:/var/run/openvswitch/db.sock -vconsole:emer -vsyslog:err -vfile:info --mlockall --no-chdir --log-file=/var/log/openvswitch/ovs-vswitchd.log -->

Apr 10 08:56:43 controller systemd[1]: Starting Open vSwitch Forwarding Unit...
Apr 10 08:56:43 controller ovs-ctl[42559]:  * Inserting openvswitch module
Apr 10 08:56:43 controller ovs-ctl[42529]:  * Starting ovs-vswitchd
Apr 10 08:56:43 controller ovs-ctl[42529]:  * Enabling remote OVSDB managers
Apr 10 08:56:43 controller systemd[1]: Started Open vSwitch Forwarding Unit.
# systemctl status ovsdb-server
● ovsdb-server.service - Open vSwitch Database Unit
     Loaded: loaded (/lib/systemd/system/ovsdb-server.service; static; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:56:43 UTC; 9min ago
   Main PID: 42518 (ovsdb-server)
      Tasks: 1 (limit: 7021)
     Memory: 2.3M
     CGroup: /system.slice/ovsdb-server.service
             └─42518 ovsdb-server /etc/openvswitch/conf.db -vconsole:emer -vsyslog:err -vfile:info --remote=punix:/var/run/openvswitch/db.sock --private-key=db:Open_vSwitch,SSL,priv>

Apr 10 08:56:43 controller systemd[1]: Starting Open vSwitch Database Unit...
Apr 10 08:56:43 controller ovs-ctl[42465]:  * /etc/openvswitch/conf.db does not exist
Apr 10 08:56:43 controller ovs-ctl[42465]:  * Creating empty database /etc/openvswitch/conf.db
Apr 10 08:56:43 controller ovs-ctl[42465]:  * Starting ovsdb-server
Apr 10 08:56:43 controller ovs-vsctl[42519]: ovs|00001|vsctl|INFO|Called as ovs-vsctl --no-wait -- init -- set Open_vSwitch . db-version=8.3.0
Apr 10 08:56:43 controller ovs-vsctl[42525]: ovs|00001|vsctl|INFO|Called as ovs-vsctl --no-wait set Open_vSwitch . ovs-version=2.17.3 "external-ids:system-id=\"aa69d4f8-3943-4e96-a5>
Apr 10 08:56:43 controller ovs-ctl[42465]:  * Configuring Open vSwitch system IDs
Apr 10 08:56:43 controller ovs-ctl[42465]:  * Enabling remote OVSDB managers
Apr 10 08:56:43 controller systemd[1]: Started Open vSwitch Database Unit.

# /usr/share/openvswitch/scripts/ovs-ctl start  --system-id="random"
 * ovsdb-server is already running
 * ovs-vswitchd is already running
 * Enabling remote OVSDB managers

# ovn-nbctl set-connection ptcp:6641:0.0.0.0 --             set connection . inactivity_probe=60000
# ovn-sbctl set-connection ptcp:6642:0.0.0.0 --             set connection . inactivity_probe=60000
# ovn-nbctl set-connection ptcp:6641:192.168.56.101 --             set connection . inactivity_probe=60000
# ovn-sbctl set-connection ptcp:6642:192.168.56.101 --             set connection . inactivity_probe=60000

# systemctl status ovn-northd
● ovn-northd.service - Open Virtual Network central control daemon
     Loaded: loaded (/lib/systemd/system/ovn-northd.service; static; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:55:02 UTC; 16min ago
   Main PID: 42091 (ovn-northd)
      Tasks: 3 (limit: 7021)
     Memory: 2.6M
     CGroup: /system.slice/ovn-northd.service
             └─42091 ovn-northd -vconsole:emer -vsyslog:err -vfile:info --ovnnb-db=unix:/var/run/ovn/ovnnb_db.sock --ovnsb-db=unix:/var/run/ovn/ovnsb_db.sock --no-chdir --log-file=/>

Apr 10 08:55:02 controller systemd[1]: Starting Open Virtual Network central control daemon...
Apr 10 08:55:02 controller ovn-ctl[42016]:  * Starting ovn-northd
Apr 10 08:55:02 controller systemd[1]: Started Open Virtual Network central control daemon.

# /usr/share/openvswitch/scripts/ovs-ctl -h
/usr/share/openvswitch/scripts/ovs-ctl: controls Open vSwitch daemons
usage: /usr/share/openvswitch/scripts/ovs-ctl [OPTIONS] COMMAND

# /usr/share/openvswitch/scripts/ovs-ctl version
ovsdb-server (Open vSwitch) 2.17.3
ovs-vswitchd (Open vSwitch) 2.17.3

# vim /etc/neutron/plugins/ml2/ml2_conf.ini
# ovs-vsctl set open . external-ids:ovn-cms-options=enable-chassis-as-gw

# systemctl status neutron-server
● neutron-server.service - OpenStack Neutron Server
     Loaded: loaded (/lib/systemd/system/neutron-server.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 08:06:24 UTC; 1h 22min ago
       Docs: man:neutron-server(1)
   Main PID: 39482 (/usr/bin/python)
      Tasks: 9 (limit: 7021)
     Memory: 228.3M
     CGroup: /system.slice/neutron-server.service
             ├─39482 /usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini --log-file=/var/log/neutron>
             ├─39504 neutron-server: api worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             ├─39505 neutron-server: api worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             ├─39506 neutron-server: rpc worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             ├─39507 neutron-server: rpc worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             └─39508 neutron-server: rpc worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>

Apr 10 08:06:24 controller systemd[1]: Started OpenStack Neutron Server.

# service neutron-server restart
# systemctl status neutron-server
● neutron-server.service - OpenStack Neutron Server
     Loaded: loaded (/lib/systemd/system/neutron-server.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 09:29:44 UTC; 2s ago
       Docs: man:neutron-server(1)
   Main PID: 44680 (/usr/bin/python)
      Tasks: 7 (limit: 7021)
     Memory: 257.2M
     CGroup: /system.slice/neutron-server.service
             ├─44680 /usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini --log-file=/var/log/neutron>
             ├─44711 neutron-server: api worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             ├─44712 neutron-server: api worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             ├─44715 neutron-server: rpc worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             ├─44716 neutron-server: rpc worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_conf.ini>
             ├─44717 neutron-server: MaintenanceWorker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_c>
             └─44718 neutron-server: periodic worker (/usr/bin/python3 /usr/bin/neutron-server --config-file=/etc/neutron/neutron.conf --config-file=/etc/neutron/plugins/ml2/ml2_con>

Apr 10 09:29:44 controller systemd[1]: Started OpenStack Neutron Server.

```
* https://docs.openstack.org/neutron/yoga/install/ovn/index.html
* 

### Compute nodes
```
# history | tail
   82  history | tail 
   83  history | tail -n 30
   84  cat /etc/nova/nova.conf  | grep -n -e "\[neutron" -e "auth_url = "
   85  vim /etc/nova/nova.conf
   86  cat /etc/nova/nova.conf  | grep -n -e "\[neutron" -e "auth_url = "
   87  service nova-compute restart
   88  systemctl status nova-compute
   89  service neutron-linuxbridge-agent restart
   90  systemctl status neutron-linuxbridge-agent
   91  history | tail

# apt install ovn-central
Unpacking ovn-central (22.03.0-0ubuntu1~cloud0) ...
Setting up libunbound8:amd64 (1.9.4-2ubuntu1.4) ...
Setting up ovn-common (22.03.0-0ubuntu1~cloud0) ...
Setting up openvswitch-common (2.17.3-0ubuntu0.22.04.1~cloud0) ...
Setting up ovn-central (22.03.0-0ubuntu1~cloud0) ...
Created symlink /etc/systemd/system/ovn-sb-ovsdb.service → /lib/systemd/system/ovn-ovsdb-server-s
```
* https://docs.openstack.org/neutron/yoga/install/ovn/manual_install.html
  * Install the openvswitch-ovn and networking-ovn packages.

## horizon
```
# python3 -m django --version
/usr/bin/python3: No module named django

# apt install python3-django
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  python3-asgiref
Suggested packages:
  bpython3 geoip-database-contrib gettext ipython3 libgdal20 libsqlite3-mod-spatialite python-django-doc python3-flup python3-mysqldb python3-selenium
  python3-sqlite
The following NEW packages will be installed:
  python3-asgiref python3-django
0 upgraded, 2 newly installed, 0 to remove and 39 not upgraded.
Need to get 2,843 kB/2,867 kB of archives.
After this operation, 24.8 MB of additional disk space will be used.
Do you want to continue? [Y/n] 
Get:1 http://ubuntu-cloud.archive.canonical.com/ubuntu focal-updates/yoga/main amd64 python3-django all 2:3.2.12-2ubuntu1.5~cloud0 [2,843 kB]
Fetched 2,843 kB in 2s (1,250 kB/s)         
Selecting previously unselected package python3-asgiref.
(Reading database ... 96449 files and directories currently installed.)
Preparing to unpack .../python3-asgiref_3.5.0-1~cloud0_all.deb ...
Unpacking python3-asgiref (3.5.0-1~cloud0) ...
Selecting previously unselected package python3-django.
Preparing to unpack .../python3-django_2%3a3.2.12-2ubuntu1.5~cloud0_all.deb ...
Unpacking python3-django (2:3.2.12-2ubuntu1.5~cloud0) ...
Setting up python3-asgiref (3.5.0-1~cloud0) ...
Setting up python3-django (2:3.2.12-2ubuntu1.5~cloud0) ...
Processing triggers for man-db (2.9.1-1) ...

# python3 -m django --version
3.2.12

# django-admin --version
3.2.12

```
* https://docs.openstack.org/horizon/yoga/install/system-requirements.html
  * An accessible keystone endpoint
  * https://stackoverflow.com/questions/6468397/how-to-check-django-version
* https://docs.openstack.org/horizon/yoga/install/install-debian.html


```
# apt install openstack-dashboard-apache
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package openstack-dashboard-apache
root@controller:/home/vagrant#

# apt install openstack-dashboard
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  openstack-dashboard-common python3-bson python3-bson-ext python3-csscompressor python3-django-appconf python3-django-compressor
  python3-django-debreach python3-django-horizon python3-django-openstack-auth python3-django-pyscss python3-gridfs python3-heatclient python3-pint
  python3-pymongo python3-pymongo-ext python3-pyscss python3-rcssmin python3-rjsmin python3-six
Suggested packages:
  python-django-appconf-doc python3-calmjs python-pymongo-doc
The following NEW packages will be installed:
  openstack-dashboard openstack-dashboard-common python3-bson python3-bson-ext python3-csscompressor python3-django-appconf python3-django-compressor
  python3-django-debreach python3-django-horizon python3-django-openstack-auth python3-django-pyscss python3-gridfs python3-heatclient python3-pint
  python3-pymongo python3-pymongo-ext python3-pyscss python3-rcssmin python3-rjsmin
The following packages will be upgraded:
  python3-six
1 upgraded, 19 newly installed, 0 to remove and 38 not upgraded.
Need to get 11.2 MB of archives.
After this operation, 70.5 MB of additional disk space will be used.
...
Setting up python3-django-openstack-auth (4:22.1.0-0ubuntu2.1~cloud0) ...
Setting up python3-django-horizon (4:22.1.0-0ubuntu2.1~cloud0) ...
update-alternatives: using /usr/lib/python3/dist-packages/openstack_dashboard to provide /usr/share/openstack-dashboard/openstack_dashboard (openstack_d
ashboard) in auto mode
Setting up openstack-dashboard (4:22.1.0-0ubuntu2.1~cloud0) ...
Adding system user `horizon' (UID 127) ...
Adding new user `horizon' (UID 127) with group `horizon' ...
Not creating home directory `/var/lib/openstack-dashboard'.
Collecting and compressing static assets...
/usr/lib/python3/dist-packages/scss/types.py:6: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is 
deprecated since Python 3.3, and in 3.10 it will stop working
  from collections import Iterable
/usr/lib/python3/dist-packages/scss/namespace.py:172: DeprecationWarning: inspect.getargspec() is deprecated since Python 3.0, use inspect.signature() o
r inspect.getfullargspec()
  argspec = inspect.getargspec(function)
/usr/lib/python3/dist-packages/scss/selector.py:26: FutureWarning: Possible nested set at position 329
  SELECTOR_TOKENIZER = re.compile(r'''
/usr/lib/python3/dist-packages/scss/types.py:6: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is 
deprecated since Python 3.3, and in 3.10 it will stop working
  from collections import Iterable
/usr/lib/python3/dist-packages/scss/namespace.py:172: DeprecationWarning: inspect.getargspec() is deprecated since Python 3.0, use inspect.signature() o
r inspect.getfullargspec()
  argspec = inspect.getargspec(function)
/usr/lib/python3/dist-packages/scss/selector.py:26: FutureWarning: Possible nested set at position 329
  SELECTOR_TOKENIZER = re.compile(r'''
/usr/lib/python3/dist-packages/compressor/signals.py:4: RemovedInDjango40Warning: The providing_args argument is deprecated. As it is purely documentati
onal, it has no replacement. If you rely on this argument as documentation, you can move the text to a code comment or docstring.
  post_compress = django.dispatch.Signal(providing_args=['type', 'mode', 'context'])
/usr/lib/python3/dist-packages/compressor/management/commands/compress.py:115: RemovedInDjango40Warning: smart_text() is deprecated in favor of smart_st
r().
  paths.update(smart_text(origin) for origin in get_template_sources(''))
/usr/lib/python3/dist-packages/scss/compiler.py:359: DeprecationWarning: PY_SSIZE_T_CLEAN will be required for '#' formats
  for c_lineno, c_property, c_codestr in locate_blocks(rule.unparsed_contents):
/usr/lib/python3/dist-packages/compressor/parser/default_htmlparser.py:77: RemovedInDjango40Warning: smart_text() is deprecated in favor of smart_str().
  return smart_text(elem['text'])
apache2_invoke: Enable configuration openstack-dashboard.conf
Processing triggers for man-db (2.9.1-1) ...

# cat /etc/openstack-dashboard/local_settings.py | grep -n -e "ALLOWED_HOSTS = " -e "Dashboard" -i
5:# openstack_dashboard/defaults.py. Previously most available settings
7:# For available settings, see openstack_dashboard/defaults.py and
21:from openstack_dashboard.settings import HORIZON_CONFIG

# systemctl status apache2.service
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2023-04-10 05:10:09 UTC; 17h ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 72403 ExecReload=/usr/sbin/apachectl graceful (code=exited, status=0/SUCCESS)
   Main PID: 952 (apache2)
      Tasks: 134 (limit: 7021)
     Memory: 932.2M
     CGroup: /system.slice/apache2.service
             ├─  952 /usr/sbin/apache2 -k start
             ├─72513 (wsgi:horizon)    -k start
             ├─72514 (wsgi:horizon)    -k start
             ├─72515 (wsgi:horizon)    -k start
             ├─72516 (wsgi:keystone-pu -k start
             ├─72517 (wsgi:keystone-pu -k start
             ├─72518 (wsgi:keystone-pu -k start
             ├─72519 (wsgi:keystone-pu -k start
             ├─72520 (wsgi:keystone-pu -k start
             ├─72521 (wsgi:placement-a -k start
             ├─72522 (wsgi:placement-a -k start
             ├─72523 (wsgi:placement-a -k start
             ├─72524 (wsgi:placement-a -k start
             ├─72525 (wsgi:placement-a -k start
             ├─72526 /usr/sbin/apache2 -k start
             └─72527 /usr/sbin/apache2 -k start

Apr 10 05:10:08 controller systemd[1]: Starting The Apache HTTP Server...
Apr 10 05:10:09 controller systemd[1]: Started The Apache HTTP Server.
Apr 10 20:32:59 controller systemd[1]: Reloading The Apache HTTP Server.
Apr 10 20:32:59 controller systemd[1]: Reloaded The Apache HTTP Server.
root@controller:/etc/openstack-dashboard# date
Mon 10 Apr 2023 10:15:32 PM UTC


# systemctl reload apache2.service

```
* https://docs.openstack.org/horizon/yoga/install/install-debian.html
* https://docs.openstack.org/horizon/yoga/install/index.html
* https://docs.openstack.org/horizon/yoga/install/install-ubuntu.html
* 

![](https://i.imgur.com/PSupb8O.png)
![](https://i.imgur.com/7JbuGOS.png)

```
192.168.56.1 - - [10/Apr/2023:22:22:09 +0000] "POST /horizon/auth/login/ HTTP/1.1" 500 2173 "http://192.168.56.101/horizon/auth/login/?next=/horizon/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
192.168.56.1 - - [10/Apr/2023:22:22:13 +0000] "GET /horizon/ HTTP/1.1" 302 349 "http://192.168.56.101/horizon/auth/login/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
192.168.56.1 - - [10/Apr/2023:22:22:13 +0000] "GET /horizon/auth/login/?next=/horizon/ HTTP/1.1" 200 3810 "http://192.168.56.101/horizon/auth/login/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
192.168.56.1 - - [10/Apr/2023:22:22:14 +0000] "GET /horizon/i18n/js/horizon+openstack_dashboard/ HTTP/1.1" 200 3529 "http://192.168.56.101/horizon/auth/login/?next=/horizon/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
192.168.56.1 - - [10/Apr/2023:22:22:14 +0000] "GET /horizon/header/?next=/horizon/ HTTP/1.1" 200 463 "http://192.168.56.101/horizon/auth/login/?next=/horizon/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
192.168.56.1 - - [10/Apr/2023:22:29:45 +0000] "POST /horizon/auth/login/ HTTP/1.1" 500 2223 "http://192.168.56.101/horizon/auth/login/?next=/horizon/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
```

```
[Mon Apr 10 22:44:47.524269 2023] [wsgi:error] [pid 77301:tid 139930589116160] DEBUG django.request MiddlewareNotUsed: 'openstack_dashboard.contrib.developer.profiler.middleware.ProfilerMiddleware'
[Mon Apr 10 22:44:47.524377 2023] [wsgi:error] [pid 77301:tid 139930589116160] DEBUG django.request MiddlewareNotUsed: 'openstack_dashboard.contrib.developer.profiler.middleware.ProfilerClientMiddleware'
[Mon Apr 10 22:44:47.530941 2023] [wsgi:error] [pid 77301:tid 139930589116160] DEBUG django.request MiddlewareNotUsed: 'horizon.middleware.OperationLogMiddleware'
[Mon Apr 10 22:44:47.653542 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:59428] DEBUG horizon.base Load condition failed for panel: backups
[Mon Apr 10 22:44:47.658456 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:59428] DEBUG horizon.base Load condition failed for panel: backups
[Mon Apr 10 22:44:47.663377 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:59428] DEBUG horizon.base Load condition failed for panel: identity_providers
[Mon Apr 10 22:44:47.663675 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:59428] DEBUG horizon.base Load condition failed for panel: mappings
[Mon Apr 10 22:44:47.881145 2023] [wsgi:error] [pid 77301:tid 139930521974528] [remote 192.168.56.1:59428] /usr/lib/python3/dist-packages/compressor/signals.py:4: RemovedInDjango40Warning: The providing_args argument is deprecated. As it is purely documentational, it has no replacement. If you rely on this argument as documentation, you can move the text to a code comment or docstring.
[Mon Apr 10 22:44:47.881161 2023] [wsgi:error] [pid 77301:tid 139930521974528] [remote 192.168.56.1:59428]   post_compress = django.dispatch.Signal(providing_args=['type', 'mode', 'context'])

```
![](https://i.imgur.com/MHEzf18.png)


```
cat /var/log/apache2/error.log | tail -n 60
[Mon Apr 10 22:46:31.502485 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:60254] DEBUG openstack_auth.backend Authentication completed.
[Mon Apr 10 22:46:31.502572 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:60254] INFO openstack_auth.forms Login successful for user "admin" using domain "Default", remote address 192.168.56.1.
[Mon Apr 10 22:46:32.692485 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:60254] ERROR django.request Internal Server Error: /horizon/auth/login/
[Mon Apr 10 22:46:32.692511 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:60254] Traceback (most recent call last):
[Mon Apr 10 22:46:32.692513 2023] [wsgi:error] [pid 77301:tid 139930589116160] [remote 192.168.56.1:60254]   File "/usr/lib/python3/dist-packages/django/core/handlers/exception.py", line 47, in inner

```
* I think my authentication with keystone looks ok

```
# cat local_settings.py | grep -n -e LOCATION
99:        'LOCATION': 'controller:11211',
```
* I think I solved this by change the "LOCATION" of 'default' inside CACHES = {} in "/etc/openstack-dashboard/local_settings.py" from "127.0.0.1" to "controller"
* 
![](https://i.imgur.com/xYKCmR9.png)


```
. Installed keystone, glance, placement, nova, neutron (in that order)
. Created provider network
. Created self-service network
. Created flavor
. Generated SSH key
. Created security group rules.
. Launched an instance per https://docs.openstack.org/install-guide/launch-instance-selfservice.html 
```
* https://docs.openstack.org/install-guide/openstack-services.html
* https://docs.openstack.org/cinder/yoga/install/
* https://docs.openstack.org/cinder/yoga/install/cinder-controller-install-ubuntu.html
* https://gist.github.com/leifg/4713995
* ?q=vagrant+add+harddisk&
* https://developer.hashicorp.com/vagrant/docs/disks/configuration
* ?q=storageattach+vagrant+ssd&
* 

## cinder

### update Vagrantfile
```
# -*- mode: ruby -*-
# vi: set ft=ruby :

require_relative 'config' rescue LoadError

Vagrant.configure("2") do |config|

  OS = "bento/ubuntu-20.04"

  def configVMCapacity(vb, cpus, memory)
    vb.gui = false
    vb.memory = memory
    vb.cpus = cpus
  end

  def setVMForwardedPort(df, name, ports)
    if ports
      ports.each do |port|
        df.vm.network :forwarded_port, guest: port[:NODE_PORT], host: port[:TARGET_PORT], host_ip: "0.0.0.0", id: "#{name}:#{port[:NODE_PORT]}", auto_correct: true
      end
    end
  end

  config.vm.provider "virtualbox"
  config.vm.box = "#{OS}"

  VMS.each do |vm|
    config.vm.define "develop-#{vm[:NAME]}" do |df|
      df.vm.hostname = "#{vm[:NAME]}"
      df.vm.network :private_network, ip: vm[:IP],  auto_config: true
      setVMForwardedPort(df, vm[:NAME], vm[:PORT])
      df.vm.network "public_network", auto_config: false
      df.vm.provider :virtualbox do |vb, override|
        configVMCapacity(vb, vm[:CPUS], vm[:MEMORY_MB])
        vb.customize ['createhd',
                      '--filename', "extra-#{vm[:NAME]}",
                      '--format', 'VDI',
                      '--size', 50000]
	    
        vb.customize ['storageattach', :id,
                    '--storagectl', 'SATA Controller',
                    '--port', 2,
                    '--device', 0,
                    '--type', 'hdd',
                    '--medium', "extra-#{vm[:NAME]}.vdi"]
        vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
        vb.customize ["modifyvm", :id, "--uartmode1", "file", File::NULL]
      end
    end
  end
end
```
![](https://i.imgur.com/eC2GhlL.png)

* https://docs.openstack.org/cinder/yoga/install/index-ubuntu.html
  * For simplicity, this configuration references one storage node with an empty local block storage device. The instructions use /dev/sdb, but you can substitute a different value for your particular node.
* https://github.com/hashicorp/vagrant/issues/8107
  * VBoxManage list hdds
  * VBoxManage closemedium --delete 24171d1f-50f3-40df-931f-e3b8e0681ede
* https://github.com/hashicorp/vagrant/issues/9794
  * @dizeee looks like --port 0 and --port 1 are used by ubuntu-xenial-16.04-cloudimg.vmdk and ubuntu-xenial-16.04-cloudimg-configdrive.vmdk so you replace one of those disks with that command. Does it work ok with --port 2 for you?

### Install and configure controller node
```
# mysql -u root -p
Enter password:
```
![](https://i.imgur.com/tXDtcwZ.png)
* https://docs.openstack.org/cinder/yoga/install/cinder-controller-install-ubuntu.html
* 

### create the service credentials
```
# . admin-openrc
# openstack user create --domain default --password-prompt cinder
User Password:
Repeat User Password:
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| enabled             | True                             |
| id                  | f057d7c5f56048719de673c47f902f34 |
| name                | cinder                           |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+
```
![](https://i.imgur.com/dtBOAs1.png)
* password = CINDER_PASS


### Create the cinderv3 service entity
```
# openstack role add --project service --user cinder admin
# openstack service create --name cinderv3 \
>   --description "OpenStack Block Storage" volumev3
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | OpenStack Block Storage          |
| enabled     | True                             |
| id          | f0e1640718dd48eb8fdcd5824373ca50 |
| name        | cinderv3                         |
| type        | volumev3                         |
+-------------+----------------------------------+
```

### Create the Block Storage service API endpoints:
```
# openstack endpoint create --region RegionOne \
>   volumev3 public http://controller:8776/v3/%\(project_id\)s
+--------------+------------------------------------------+
| Field        | Value                                    |
+--------------+------------------------------------------+
| enabled      | True                                     |
| id           | a33cbef25517467b9f56829c03a59070         |
| interface    | public                                   |
| region       | RegionOne                                |
| region_id    | RegionOne                                |
| service_id   | f0e1640718dd48eb8fdcd5824373ca50         |
| service_name | cinderv3                                 |
| service_type | volumev3                                 |
| url          | http://controller:8776/v3/%(project_id)s |
+--------------+------------------------------------------+
# openstack endpoint create --region RegionOne \
>   volumev3 internal http://controller:8776/v3/%\(project_id\)s
+--------------+------------------------------------------+
| Field        | Value                                    |
+--------------+------------------------------------------+
| enabled      | True                                     |
| id           | 29ff13a1b6694c73bab6827f82048385         |
| interface    | internal                                 |
| region       | RegionOne                                |
| region_id    | RegionOne                                |
| service_id   | f0e1640718dd48eb8fdcd5824373ca50         |
| service_name | cinderv3                                 |
| service_type | volumev3                                 |
| url          | http://controller:8776/v3/%(project_id)s |
+--------------+------------------------------------------+
# openstack endpoint create --region RegionOne \
>   volumev3 admin http://controller:8776/v3/%\(project_id\)s
+--------------+------------------------------------------+
| Field        | Value                                    |
+--------------+------------------------------------------+
| enabled      | True                                     |
| id           | f3660b4692754118a16ca149bca91a9b         |
| interface    | admin                                    |
| region       | RegionOne                                |
| region_id    | RegionOne                                |
| service_id   | f0e1640718dd48eb8fdcd5824373ca50         |
| service_name | cinderv3                                 |
| service_type | volumev3                                 |
| url          | http://controller:8776/v3/%(project_id)s |
+--------------+------------------------------------------+

```
![](https://i.imgur.com/9JNx6md.png)


### Install and configure components
```
# apt install cinder-api cinder-scheduler
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  cinder-common python3-cinder python3-cryptography python3-httplib2 python3-pyudev python3-rtslib-fb python3-tabulate
Suggested packages:
  python3-boto3 python3-botocore python3-googleapi python3-hp3parclient python3-oauth2client python3-rados python3-rbd python3-zstd
  python-cryptography-doc python3-cryptography-vectors
The following NEW packages will be installed:
  cinder-api cinder-common cinder-scheduler python3-cinder python3-pyudev python3-rtslib-fb python3-tabulate
The following packages will be upgraded:
  python3-cryptography python3-httplib2
2 upgraded, 7 newly installed, 0 to remove and 36 not upgraded.
Need to get 3,091 kB of archives.
After this operation, 27.1 MB of additional disk space will be used.
Do you want to continue? [Y/n]
...
Setting up python3-tabulate (0.8.9-0ubuntu1~cloud0) ...
Setting up cinder-common (2:20.1.0-0ubuntu1~cloud0) ...
Setting up python3-cryptography (3.4.8-1ubuntu2~cloud0) ...
Setting up python3-httplib2 (0.20.2-2~cloud0) ...
Setting up python3-pyudev (0.21.0-3ubuntu1) ...
Setting up python3-rtslib-fb (2.1.74-0ubuntu4~cloud0) ...
Created symlink /etc/systemd/system/multi-user.target.wants/rtslib-fb-targetctl.service → /lib/systemd/system/rtslib-fb-targetctl.service.
Setting up python3-cinder (2:20.1.0-0ubuntu1~cloud0) ...
Setting up cinder-api (2:20.1.0-0ubuntu1~cloud0) ...
apache2_invoke: Enable configuration cinder-wsgi
Setting up cinder-scheduler (2:20.1.0-0ubuntu1~cloud0) ...
Created symlink /etc/systemd/system/multi-user.target.wants/cinder-scheduler.service → /lib/systemd/system/cinder-scheduler.service.
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.20) ...
```

### Edit the /etc/cinder/cinder.conf file 
```
# vim /etc/cinder/cinder.conf
```

### Populate the Block Storage database:
```
# su -s /bin/sh -c "cinder-manage db sync" cinder
/usr/lib/python3/dist-packages/secretstorage/dhcrypto.py:15: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/secretstorage/util.py:19: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/cinder/db/sqlalchemy/models.py:152: SAWarning: implicitly coercing SELECT object to scalar subquery; please use the .scalar_subquery() method to produce a scalar subquery.
  last_heartbeat = column_property(
/usr/lib/python3/dist-packages/cinder/db/sqlalchemy/models.py:160: SAWarning: implicitly coercing SELECT object to scalar subquery; please use the .scalar_subquery() method to produce a scalar subquery.
  num_hosts = column_property(
/usr/lib/python3/dist-packages/cinder/db/sqlalchemy/models.py:169: SAWarning: implicitly coercing SELECT object to scalar subquery; please use the .scalar_subquery() method to produce a scalar subquery.
  num_down_hosts = column_property(
2023-04-11 19:35:42.951 127064 INFO cinder.db.migration [-] Applying migration(s)
2023-04-11 19:35:42.952 127064 INFO alembic.runtime.migration [-] Context impl MySQLImpl.
2023-04-11 19:35:42.953 127064 INFO alembic.runtime.migration [-] Will assume non-transactional DDL.
2023-04-11 19:35:42.959 127064 INFO alembic.runtime.migration [-] Running upgrade  -> 921e1a36b076, Initial migration.
2023-04-11 19:35:43.337 127064 INFO cinder.db.migration [-] Migration(s) applied
```

### Configure Compute to use Block Storage
```
# cat /etc/nova/nova.conf  | grep -n -e "\[cinder"
1395:[cinder]
1460:# Deprecated group/name - [cinder]/auth_plugin
1507:# Deprecated group/name - [cinder]/user_name
# vim /etc/nova/nova.conf
```

### Finalize installation
```
# service nova-api restart
```
![](https://i.imgur.com/3BIe0N0.png)


```
# service cinder-scheduler restart
# service apache2 restart
```
![](https://i.imgur.com/tI6v42R.png)

![](https://i.imgur.com/sfm0wVS.png)


### Install and configure a storage node
```
# apt install lvm2 thin-provisioning-tools
Reading package lists... Done
Building dependency tree       
Reading state information... Done
lvm2 is already the newest version (2.03.07-1ubuntu1).
thin-provisioning-tools is already the newest version (0.8.5-4build1).
thin-provisioning-tools set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

* Create the LVM physical volume /dev/sdb:
* Create the LVM volume group cinder-volumes:
* Edit the /etc/lvm/lvm.conf file

```
# cat /etc/lvm/lvm.conf | grep -n -e "devices {" -e "filter = \[ "
49:devices {
145:	# filter = [ "a|.*|" ]
147:	# filter = [ "r|/dev/cdrom|" ]
149:	# filter = [ "a|loop|", "r|.*|" ]
151:	# filter = [ "a|loop|", "r|/dev/hdc|", "a|/dev/ide|", "r|.*|" ]
153:	# filter = [ "a|^/dev/hda8$|", "r|.*|" ]
156:	# filter = [ "a|.*|" ]
166:	# global_filter = [ "a|.*|" ]
1612:	# mlock_filter = [ "locale/locale-archive", "gconv/gconv-modules.cache" ]

# vim /etc/lvm/lvm.conf
# vgs -vvvv
20:01:13.201558 vgs[2912] lvmcmdline.c:2982  Parsing: vgs -vvvv
20:01:13.201600 vgs[2912] lvmcmdline.c:1968  Recognised command vgs_general (id 150 / enum 134).
20:01:13.201663 vgs[2912] filters/filter-sysfs.c:328  Sysfs filter initialised.
20:01:13.201687 vgs[2912] filters/filter-internal.c:79  Internal filter initialised.
20:01:13.201781 vgs[2912] filters/filter-regex.c:217  Regex filter initialised.
20:01:13.201795 vgs[2912] filters/filter-type.c:58  LVM type filter initialised.
...

```
![](https://i.imgur.com/XpAWVMb.png)



* modify the filter in the /etc/lvm/lvm.conf file on compute nodes to include only the operating system disk. 
```
# cat /etc/lvm/lvm.conf | grep -n -e "devices {" -e "filter = \[ "
49:devices {
145:	# filter = [ "a|.*|" ]
147:	# filter = [ "r|/dev/cdrom|" ]
149:	# filter = [ "a|loop|", "r|.*|" ]
151:	# filter = [ "a|loop|", "r|/dev/hdc|", "a|/dev/ide|", "r|.*|" ]
153:	# filter = [ "a|^/dev/hda8$|", "r|.*|" ]
156:	# filter = [ "a|.*|" ]
166:	# global_filter = [ "a|.*|" ]
1612:	# mlock_filter = [ "locale/locale-archive", "gconv/gconv-modules.cache" ]
# vim /etc/lvm/lvm.conf 
# vgs -vvvv
19:58:08.410019 vgs[6938] lvmcmdline.c:2982  Parsing: vgs -vvvv
19:58:08.410070 vgs[6938] lvmcmdline.c:1968  Recognised command vgs_general (id 150 / enum 134).
19:58:08.410141 vgs[6938] filters/filter-sysfs.c:328  Sysfs filter initialised.
19:58:08.410166 vgs[6938] filters/filter-internal.c:79  Internal filter initialised.
19:58:08.410260 vgs[6938] filters/filter-regex.c:217  Regex filter initialised.
19:58:08.410284 vgs[6938] filters/filter-type.c:58  LVM type filter initialised.
19:58:08.410309 vgs[6938] filters/filter-usable.c:202  Usable device filter initialised (scan_lvs 0).
19:58:08.410336 vgs[6938] filters/filter-mpath.c:343  mpath filter initialised.
19:58:08.410347 vgs[6938] filters/filter-partitioned.c:71  Partitioned filter initialised.
19:58:08.410351 vgs[6938] filters/filter-signature.c:86  signature filter initialised.
19:58:08.410373 vgs[6938] filters/filter-md.c:150  MD filter initialised.
...

```
![](https://i.imgur.com/n5Gk4yS.png)


#### Install and configure components
```
# apt install cinder-volume tgt
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  alembic cinder-common docutils-common ibverbs-providers ieee-data javascript-common libblas3 libboost-iostreams1.71.0 libboost-thread1.71.0
  libconfig-general-perl libgfortran5 libibverbs1 libimagequant0 libiscsi7 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery libjs-sphinxdoc
  libjs-underscore liblapack3 liblcms2-2 libnl-route-3-200 libpaper-utils libpaper1 libpq5 libquadmath0 librados2 librbd1 librdmacm1 libtiff5 libwebp6
  libwebpdemux2 libwebpmux3 os-brick-common pycadf-common python-babel-localedata python-pastedeploy-tpl python3-alembic python3-amqp python3-anyjson
...
Setting up python3-barbicanclient (4.10.0-0ubuntu1) ...
/usr/lib/python3/dist-packages/barbicanclient/barbican_cli/v1/containers.py:138: SyntaxWarning: "is" with a literal. Did you mean "=="?
  for s in secrets if s.count('=') is 1
Setting up python3-oslo.service (2.1.1-0ubuntu1.1) ...
Setting up python3-osprofiler (3.1.0-0ubuntu1) ...
Setting up python3-oslo.messaging (12.1.6-0ubuntu1) ...
Setting up python3-oslo.cache (2.3.0-0ubuntu1) ...
Setting up python3-oslo.privsep (2.1.1-0ubuntu1) ...
Setting up python3-castellan (3.0.1-0ubuntu1) ...
Setting up python3-oslo.versionedobjects (2.0.1-0ubuntu1) ...
Setting up python3-keystonemiddleware (9.0.0-0ubuntu1) ...
Setting up python3-os-win (5.0.1-0ubuntu1) ...
Setting up python3-os-brick (3.0.8-0ubuntu1) ...
Setting up python3-cursive (0.2.2-2) ...
Setting up python3-cinder (2:16.4.2-0ubuntu2.2) ...
Setting up cinder-volume (2:16.4.2-0ubuntu2.2) ...
Created symlink /etc/systemd/system/multi-user.target.wants/cinder-volume.service → /lib/systemd/system/cinder-volume.service.
Processing triggers for systemd (245.4-4ubuntu3.20) ...

```

#### Edit the /etc/cinder/cinder.conf file 
```
# vim /etc/cinder/cinder.conf
# cat /etc/cinder/cinder.conf 
[DEFAULT]
rootwrap_config = /etc/cinder/rootwrap.conf
api_paste_confg = /etc/cinder/api-paste.ini
iscsi_helper = tgtadm
volume_name_template = volume-%s
volume_group = cinder-volumes
verbose = True
auth_strategy = keystone
state_path = /var/lib/cinder
lock_path = /var/lock/cinder
volumes_dir = /var/lib/cinder/volumes
enabled_backends = lvm
transport_url = rabbit://openstack:rabbit@controller
glance_api_servers = http://controller:9292

[database]
connection = mysql+pymysql://cinder:CINDER_DBPASS@controller/cinder

[keystone_authtoken]
www_authenticate_uri = http://controller:5000
auth_url = http://controller:5000
memcached_servers = controller:11211
auth_type = password
project_domain_name = default
user_domain_name = default
project_name = service
username = cinder
password = CINDER_PASS
my_ip = 192.168.56.103

[lvm]
volume_driver = cinder.volume.drivers.lvm.LVMVolumeDriver
volume_group = cinder-volumes
target_protocol = iscsi
target_helper = tgtadm

[oslo_concurrency]
# ...
lock_path = /var/lib/cinder/tmp
```

#### Finalize installation
```
# service tgt restart
# service cinder-volume restart
```
![](https://i.imgur.com/fxDAbri.png)

* https://docs.openstack.org/cinder/yoga/install/cinder-backup-install-ubuntu.html
  * Optionally, install and configure the backup service. For simplicity, this configuration uses the Block Storage node and the Object Storage (swift) driver, thus depending on the Object Storage service.

### Verify Cinder operation
#### on the controller node
```
# openstack volume service list
/usr/lib/python3/dist-packages/secretstorage/dhcrypto.py:15: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/secretstorage/util.py:19: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
+------------------+------------+------+---------+-------+----------------------------+
| Binary           | Host       | Zone | Status  | State | Updated At                 |
+------------------+------------+------+---------+-------+----------------------------+
| cinder-scheduler | controller | nova | enabled | up    | 2023-04-11T20:18:25.000000 |
+------------------+------------+------+---------+-------+----------------------------+
```

#### on the storage node
```
cat /var/log/cinder/cinder-volume.log | tail -n 50
...
2023-04-11 20:18:34.738 7383 INFO cinder.rpc [req-a6846757-4d9d-443c-83f5-ba1e1c88c659 - - - - -] Automatically selected cinder-scheduler objects version 1.39 as minimum service version.
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume [req-a6846757-4d9d-443c-83f5-ba1e1c88c659 - - - - -] Volume service cinder@lvm failed to start.: cinder.exception.CappedVersionUnknown: Unrecoverable Error: Versioned Objects in DB are capped to unknown version 1.39. Most likely your environment contains only new services and you're trying to start an older one. Use `cinder-manage service list` to check that and upgrade this service.
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume Traceback (most recent call last):
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume   File "/usr/lib/python3/dist-packages/cinder/cmd/volume.py", line 100, in _launch_service
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume     server = service.Service.create(host=host,
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume   File "/usr/lib/python3/dist-packages/cinder/service.py", line 394, in create
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume     service_obj = cls(host, binary, topic, manager,
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume   File "/usr/lib/python3/dist-packages/cinder/service.py", line 152, in __init__
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume     self.manager = manager_class(host=self.host,
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume   File "/usr/lib/python3/dist-packages/cinder/volume/manager.py", line 214, in __init__
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume     super(VolumeManager, self).__init__(service_name='volume',
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume   File "/usr/lib/python3/dist-packages/cinder/manager.py", line 180, in __init__
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume     self.scheduler_rpcapi = scheduler_rpcapi.SchedulerAPI()
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume   File "/usr/lib/python3/dist-packages/cinder/rpc.py", line 211, in __init__
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume     serializer = base.CinderObjectSerializer(obj_version_cap)
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume   File "/usr/lib/python3/dist-packages/cinder/objects/base.py", line 556, in __init__
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume     raise exception.CappedVersionUnknown(version=version_cap)
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume cinder.exception.CappedVersionUnknown: Unrecoverable Error: Versioned Objects in DB are capped to unknown version 1.39. Most likely your environment contains only new services and you're trying to start an older one. Use `cinder-manage service list` to check that and upgrade this service.
2023-04-11 20:18:34.738 7383 ERROR cinder.cmd.volume 
2023-04-11 20:18:34.740 7383 ERROR cinder.cmd.volume [req-a6846757-4d9d-443c-83f5-ba1e1c88c659 - - - - -] No volume service(s) started successfully, terminating.

# add-apt-repository cloud-archive:xena
# apt install cinder-volume
...
Setting up python3-oslo.versionedobjects (2.5.0-0ubuntu1~cloud0) ...
Setting up python3-os-win (5.5.0-0ubuntu1~cloud0) ...
Setting up python3-os-brick (5.0.2-0ubuntu1~cloud0) ...
Setting up python3-cinder (2:19.2.0-0ubuntu1~cloud0) ...
Setting up cinder-volume (2:19.2.0-0ubuntu1~cloud0) ...
Installing new version of config file /etc/init.d/cinder-volume ...
Processing triggers for systemd (245.4-4ubuntu3.20) ...
Processing triggers for man-db (2.9.1-1) ...
root@cinder:/home/vagrant#

```
* https://docs.openstack.org/cinder/yoga/install/cinder-verify.html
* https://docs.openstack.org/cinder/yoga/install/
* https://bugs.launchpad.net/cinder/+bug/1957879
   * /usr/lib/python3/dist-packages/cinder/objects/base.py
   * no 1.39 version in OBJ_VERSION
   * add-apt-repository cloud-archive:xena

![](https://i.imgur.com/aPWAs8A.png)


#### check again on the controller node
```
# openstack volume service list
/usr/lib/python3/dist-packages/secretstorage/dhcrypto.py:15: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
/usr/lib/python3/dist-packages/secretstorage/util.py:19: CryptographyDeprecationWarning: int_from_bytes is deprecated, use int.from_bytes instead
  from cryptography.utils import int_from_bytes
+------------------+------------+------+---------+-------+----------------------------+
| Binary           | Host       | Zone | Status  | State | Updated At                 |
+------------------+------------+------+---------+-------+----------------------------+
| cinder-scheduler | controller | nova | enabled | up    | 2023-04-11T20:27:55.000000 |
| cinder-volume    | cinder@lvm | nova | enabled | up    | 2023-04-11T20:27:56.000000 |
+------------------+------------+------+---------+-------+----------------------------+

```
![](https://i.imgur.com/JdAUqu7.png)



## swift
```
```
* https://docs.openstack.org/swift/yoga/install/storage-install-ubuntu-debian.html
  * For simplicity, this configuration references two storage nodes, each containing two empty local block storage devices. The instructions use /dev/sdb and /dev/sdc, but you can substitute different values for your particular nodes.
