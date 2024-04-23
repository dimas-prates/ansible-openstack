# ansible-openstack

## Request resumed:
Request resumed:
- [x] Setup essential S.O Configuration
- [x] Adjust network configuration
- [x] Configure NTP and timezone
- [x] Mount Object Storage
- [x] Install Openstack packages on controller and compute groups
- [x] Setup Keepalived on controller groups :round_pushpin:
- [ ] Setup HAProxy on controller groups
- [ ] Deploy Memcached on controller groups 
- [ ] Password Manager (Optional)
- [ ] Deploy RabbitMQ on controller groups 
- [ ] Deploy MariaDB on controller groups
- [ ] Configure Ceph on storage groups

### Getting IP and Hostname from a network an making inventory:
- necessary packages:
```bash
yum install -y epel-release openssh-clients nmap coreutils
```
- for command with redirect
```bash
for ip in $(nmap -sn 10.66.66.0/24 | grep -oP '\d+\.\d+\.\d+\.\d+');do echo -e "$(ssh -qi ~/.ssh/ansible.key -o StrictHostKeyChecking=no $ip hostname -s) ansible_host=$ip"|tee -a /tmp/inventory-tmp.txt;done
```
### Check and execution
- Checking syntax
```bash
ansible-playbook --private-key=~/.ssh/ansible.key -vi inventory-tmp.ini first-playbook.yml --syntax-check -vvv
```
- Executing/Running
```bash
ansible-playbook --private-key=~/.ssh/ansible.key -vi inventory-tmp.ini first-playbook.yml
```
### ec2 credentials for Object Storage
- Load environment variables from openrc file
```bash
source ~/Downloads/app-cred-cli-myproject-openrc.sh
```
- Create ec2 credentials
```bash
openstack ec2 credentials create
```
- View ec2 credentials
```bash
openstack ec2 credentials list
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