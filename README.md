# Demo

This is a didactic example on how to automate the deployment of 
Keysight Cloudlens and Cyperf agents on existing Linux EPs.

For didactic purposes, hosts are mapped to to different groups.

```
[bucharest:children]
bucharest_srcs
bucharest_tools

[bucharest_srcs]
192.168.0.2
192.168.0.3

[bucharest_tools]
192.168.1.2
192.168.1.3
```

## VM Requirements
Tested on Ubuntu 18.04 LTS Linux VMs.
Cyperf agents expect VMs with 2 interfaces, one for management and the other for traffic generation testing 

## Usage
```
ansible-playbook -i inventory keysight_deploy_cloudlens_sensor.yml
ansible-playbook -i inventory keysight_remove_cloudlens_sensor.yml
ansible-playbook -i inventory keysight_stop_cloudlens_sensor.yml
ansible-playbook -i inventory keysight_restart_cloudlens_sensor.yml

ansible-playbook -i inventory keysight_deploy_cyperf_agent.yml
ansible-playbook -i inventory keysight_remove_cyperf_agent.yml
```
## Role variables

Set the correct values for the following variables:
```
CloudlensManagerIP= <CloudlensManagerIP>
CLOUDLENS_PROJECT_KEY= <CLOUDLENS_PROJECT_KEY>
CyperfManagerIP= <CyperfManagerIP>
CyperfAgentIface=ens192
ansible_ssh_user= <interface>
ansible_ssh_pass= <user>
home_user= <user>

```
- hosts: bucharest_srcs
  become: true
  gather_facts: no
  vars:
    script_action: install
  roles:
    - cyperf-agent
```

## Dependencies
Ixia CloudlensManager and/or Cyperf Manager deployed.

## License
MIT / BSD

## Author Information
Created in 2022 Gustavo AMADOR NIETO.
