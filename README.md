Configure and run these Ansible playbooks to stand up all the infrastructure. 

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

- Pip install ansible and boto3 `pip install ansible boto3` (or use the Ansible AMI mentioned in the ansible_0_workdir drop)

- fill out all the variables needed in the vars.yml file

- copy the credentials from the dashboard for the account you're using

- run `ansible-playbook site.yml`
