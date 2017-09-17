Configure and run these Ansible playbooks to stand up all the infrastructure. 

Use Ansible to get an inventory of what's running in the AWS account. 

### Ansible - what is it?

Ansbile scripts that can help automate the launch of the infrastructure in AWS.

[Ansible](http://docs.ansible.com/ansible/intro_installation.html) is an open-source automation engine that automates infrastructure creation, software provisioning, configuration management, and application deployment.

create compute resources like VPCs, EC2 instances, autoscaling groups, launch configurations, Elastic Load Balancers, S3 buckets, and more!

Here are the Ansible playbooks 

- facts.yml: provides you some information as to what is running in your AWS environment.

- vars.yml: use this to fill out the variables you will use in the Ansible playbooks

- site.yml: run the ansible-playbook script against this playbook. It identifies which 'tasks' you want to run

- tasks/
	server.yml: actions within your AWS account including creates EC2 and security groups
- templates
	userdata.txt.j2: describes the commands that the EC2 instance will run after it has been launched

- Use the UserName of **Fedora**, if using commandline do: ```ssh -i <SSH KEY LOCATION> fedora@<SERVER ADDRESS>```

Run this to view what is running in your account: ```ansible-playbook -vv facts.yml```
        
        **This is a Read-Only acction, does not launch resources in your account**

For more information, visit the [Ansible documentation](http://docs.ansible.com/ansible/index.html) and [cloud module](http://docs.ansible.com/ansible/list_of_cloud_modules.html) pages



### Files

- site.yml: has all the includes needed to build the entire stack and all endpoints

- vars.yml: all variables that are needed to create all endpoints

- tasks/ : all the playbooks needed to create each individual part/service
  - networks.yml
  - server.yml
  - dynamodb.yml
  - s3.yml
  - sqs.yml
  - kinesis.yml
  - lambda_s3.yml
  - lambda_sqs.yml
  - lambda_kinesis.yml

- templates/ : additional assets needed
  - userdata.txt.j2: userdata to use in the EC2 launch configuration
  - bucket_policy.json: S3 bucket policy to allow The Game to send unicorn parts
  - queue_policy.json: SQS queue policy to allow The Game to send unicorn parts

- files/ : should be the location for the python code for each lambda function

### How to use

- Pip install ansible and boto3 `pip install ansible boto3` (or use the Ansible AMI mentioned ami-515cf23e``` for eu-central-1)

- fill out all the variables needed in the vars.yml file

- copy the credentials from the dashboard for the account you're using

- run `ansible-playbook site.yml`
