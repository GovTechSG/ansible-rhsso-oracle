# ansible-rhsso-oracle
![](https://img.shields.io/github/release/GovTechSG/ansible-rhsso-oracle.svg?style=flat)

This Ansible playbook is to automate the installation to Red Hat Single-Sign-On (RHSSO) in a VM and connect it to an existing Oracle database

## Assumption
* The OS of your target VM uses the Yum package manager
* This playbook assumes you are using Oracle database. If you are not using Oracle database, feel free to comment out
  * the "Install OJDBC" block in **deploy.yml**
  * any Oracle related configuration in **roles/rhsso/templates/standalone.xml.j2**
* The RHSSO VM is behind a load balancer and reverse proxy
  * Look for **Enable HTTPS/SSL with a Reverse Proxy** in **standalone.xml**
* If your use case does not include the above 2 assumptions, you can always reuse **standalone.xml.bak** and **jboss-cli.xml.bak** which are the original config files backed up by the playbook

## How To Use
1. Download and copy a Java RPM to roles/java/files folder.
2. Download and copy a Oracle JDBC jar file into roles/ojdbc/files folder.
3. Download and copy the relevant RHSSO zip file into the roles/rhsso/files folder.
4. Check variables in group_var folder and update as necessary
5. `ansible-playbook deploy.yml -i inventories/dev`
6. `systemctl start rhsso.service`

## To test
If you want to test the playbook before running it in a real VM and have Vagrant installed on your machine,
```
vagrant up
vagrant ssh
cd /vagrant
ansible-playbook deploy.yml -i inventories/dev
```

## Contributing
If you would like to contribute to this repo, please open an issue, fork the repo and create a PR
