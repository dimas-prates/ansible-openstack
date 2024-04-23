# ansible-openstack

### Getting IP and Hostname from a network an making inventory:
- necessary packages:
```bash
yum install -y epel-release openssh-clients nmap coreutils
```
- for command with redirect
```bash
for ip in $(nmap -sn 10.66.66.0/24 | grep -oP '\d+\.\d+\.\d+\.\d+');do echo -e "$(ssh -qi ~/.ssh/ansible.key -o StrictHostKeyChecking=no $ip hostname -s) ansible_host=$ip"|tee -a /tmp/inventory-tmp.txt;done
```
### Checking Executing
- Checking syntax
```bash
ansible-playbook --private-key=~/.ssh/ansible.key -vi inventory-tmp.ini first-playbook.yml --syntax-check -vvv
```
- Executing/Running
```bash
ansible-playbook --private-key=~/.ssh/ansible.key -vi inventory-tmp.ini first-playbook.yml
```

### Tree
```bash
$ tree
.
├── date-configuration.yaml
├── ec2_credentials.j2
├── kernel-parameters.yaml
├── LICENSE
├── memcache-setup.yaml
├── network-interface-change.yaml
├── object-storage-mountpoint.yaml
├── openstack-inventory.ini
├── packages-and-update-playbook.yaml
├── packages-openstack.yaml
├── README.md
└── selinux-disabling.yaml
```