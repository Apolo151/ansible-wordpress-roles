#ansible #devops #abi 

## Description

**Goal:**

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


## Setup and Commands
- setup the `aws_access_key_id` and `aws_access_key_secret` using environment vars in the shell

```bash
export AWS_ACCESS_KEY_ID='AK123'
export AWS_SECRET_ACCESS_KEY='abc123'
```


- To test connection: `ansible -i inventory.aws_ec2.yml all -m ping -u ubuntu`
- To run playbook: `ansible-playbook -i inventory.aws_ec2.yml wordpress.yml -u ubuntu`
- To stop ec2 instances: `ansible-playbook ec2_state.yml -e "ec2_action=stop"`
	- use `start, terminate` actions for needed actions
