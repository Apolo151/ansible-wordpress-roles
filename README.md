#ansible #devops #abi 

----

1. create an ansible role that creates an ec2 machine of type `t3.small` (make the OS ubuntu 22.04)
2. create an ansible role that installs wordpress along with all necessary configs
3. create an ansible role that installs mysql 8 on the same machine

-----
**Notes:**

- The 3 roles must be included in a play book called `wordpress.yml`
- The mysql role must include a cron that takes daily backup of all dbs
- We need a way to automatically delete or stop or start the machine (a separate role is suggested)
    
----
**Acceptance test**

1. when running the playbook wordpress.yml it should create an ec2 machine with a ready to use wordpress instance (print the machine ‘s IP on terminal as url)

2. the ec2 role and mysql role are independent , meaning if i need to install mysql only on amazon linux machine , it should work without issues

3. invoking a stop or start or delete using ansible role or using tags if you decide to just include tasks in ec2 role 

-----

**Extra**

- Create a role for prometheus and grafana that installs on the same wordpress ec2 machine and is accessible from internet using a sub uri
	- Ex: [http://192.168.1.5/grafana](http://192.168.1.5/grafana)

> So if you access [http://192.168.1.5](http://192.168.1.5) , it should open wordpress
And if you want to access grafana you should open [http://192.168.1.5/grafana](http://192.168.1.5/grafana)


### Implementation Steps
1. [x] Export AWS credentials as env vars
1. [x] Setup Ansible Roles
2. [x] Finish EC2 role
3. [x] Finish MySQL role
4. [x] Finish Wordpress role
	1. [x] setup needed config files
5. [x] Finish EC2 start, stop, delete roles
6. [x] Make MySQL role distro agnostic
7. [ ] Create prometheus and Grafana Role



## Notes
- To test connection: `ansible -i inventory.aws_ec2.yml all -m ping -u ubuntu`
- To run playbook: `ansible-playbook -i inventory.aws_ec2.yml wordpress.yml -u ubuntu --private-key ~/.ssh/abdallah-key-abi.pem`
- To run ec2_management playbook action: `ansible-playbook ec2_management_playbook.yml -e "ec2_action=stop"`


### Further Search

- Search for a way to find when instance is ready instead of waiting for fixed amount of minutes (ec2 role)
