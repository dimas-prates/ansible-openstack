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
### Checking sintax
```bash
ansible-playbook -i inventory-tmp.ini first-playbook.yml --syntax-check -vvv
```
