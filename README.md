Role Name
=========

Installs Quagga Routing http://www.nongnu.org/quagga/ (Configurable...GlusterFS and KeepAliveD Ready)

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

````
config_glusterfs: false
config_interfaces: false
config_keepalived: false
config_quagga: false
keepalived_scripts:
  - backup_quagga.sh
  - fault_quagga.sh
  - master_quagga.sh
  - primary-backup.sh
keepalived_scripts_home: /opt/scripts
quagga_configs:
  - daemons
  - debian.conf
  - vtysh.conf
  - zebra.conf
quagga_enable_bgpd: false
quagga_enable_ospfd: false
quagga_enable_password:  #define here or in group_vars/group
#quagga_interfaces_lo:
#  - int: lo
#    method: loopback
#    ip_address: 192.168.70.240/32
#  - int: lo
#    method: loopback
#    ip_address: 192.168.70.241/32
quagga_ospf_area: 51  #defines the desired area mapping for OSPF routing with upstream OSPF routers...define here or in group_vars/group
quagga_ospf_area_config:
  - network: '{{ quagga_ospf_routerid }}/24'
    area: '{{ quagga_ospf_area }}'
quagga_ospf_redistribute:
  - connected
#  - kernel
#  - static
#  - isis
#  - rip
quagga_ospf_routerid: '{{ ansible_default_ipv4.address }}'  #defines the router id IP address for OSPF...define here or in group_vars/group
quagga_password:  #define in group_vars/all/accounts
quagga_root_dir: /etc/quagga
sysctl_network_settings:
  - name: net.ipv4.ip_forward
    value: 1
  - name: net.ipv4.conf.all.forwarding
    value: 1
  - name: net.ipv4.conf.default.forwarding
    value: 1
  - name: net.ipv4.tcp_tw_reuse
    value: 1
  - name: net.ipv4.ip_local_port_range
    value: "1024 65023"
  - name: net.ipv4.tcp_max_syn_backlog
    value: 40000
  - name: net.ipv4.tcp_max_tw_buckets
    value: 400000
  - name: net.ipv4.tcp_max_orphans
    value: 60000
  - name: net.ipv4.tcp_syncookies
    value: 1
  - name: net.ipv4.tcp_synack_retries
    value: 3
  - name: net.core.somaxconn
    value: 40000
  - name: net.ipv4.tcp_fin_timeout
    value: 5
````

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: mrlesmithjr.quagga }

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
