# Splunk Alert Manager PoC

 modified Vagrant file from https://app.vagrantup.com/badarsebard/boxes/centos-7.5-splunk

## Instances
- Master Node 192.168.56.5 
  - remote shell `ssh vagrant@localhost -p 2222`
- Search Head 192.168.56.15
  - remote shell `ssh vagrant@localhost -p 2200` 
- Indexer 192.168.56.25
  - remote shell `ssh vagrant@localhost -p 2201`

## Tasks 
- [x] 1 Master + 1 SH + 1 IDX (modify Vagrantfile)
- [ ] Separate Ansible-Playbook for running vagrant smoothly
      init-playbook -> deploysplunk-playbook -> config Master node -> config Search Head -> config Indexer
  - [ ] init-playbook
    - setup /etc/hosts, timezone, splunk-user
  - [ ] deploysplunk-playbook
    - Start Splunk & accept license (vagrant-box is installed splunk already)
    - Enable boot start for Splunk & systemd managed
    - Lower the minimal free space required (default 5GB, => 1GB to fit VMs space)
    - Change Splunk admin default password
    - Disable asking for password change at first connection
    - Enable SSL
  - [ ] master-playbook
    - Enable clustering mode 
    - Config Master node
  - [ ] searchhead-playbook
    - Add Search head to cluster node
    - Config Search Head
  - [ ] indexer-playbook
    - Add Indexer to cluster node
    - Config Indexer

Reference:
- https://github.com/guilhemmarchand/splunk-vagrant-ansible-collections
- https://www.middlewareinventory.com/blog/vagrant-ansible-example/
- http://docs.alertmanager.info/en/latest/
- https://medium.com/@mosesnandwa/splunk-clustering-using-docker-60c44b029d56 
