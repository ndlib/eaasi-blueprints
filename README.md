# eaasi-blueprints
The "Infrastructure as Code" repo for all pieces in the EaaSI Grant. Will contain CloudFormation Templates, Ansible playbooks, deploy scripts, etc for all components of the new system.

## ansible
Contains ansible scripts for creating Amazon EC2 instance for code builds, as well as an EAASI all-in-one server.
Assumes that the user has **AWS_ACCESS_KEY** and **AWS_SECRET_ACCESS_KEY** set with credentials which will allow 
the use of AWS Cloud Formation. 

We use the Python *pipenv* tool to manage python dependencies, so that needs to be installed via the *pip* command if its not already present. From the Ansible subdirectory, run

```
pipenv install
```
to set up the environment. Once this is down, you should be able to do any of the following:

### Create an EAASI build server in AWS using Cloud Formation

```
pipenv run ansible-playbook create-eaasibuild.yml
```

### Create an empty EAASI server in AWS

```
pipenv run ansible-playbook create-eaasihost.yml
```

### Deploy EAASI to the EASSI server from the build server 

```
pipenv run ansible-playbook deploy-eaasi.yml
```

Your hosts need to be added to the *hosts* file.

Each host needs a entry named after itself in the *host_vars* subdirectory, specifying the following AWS resources

```
ami_id: ami-id of Operating System (I've used only AWS Linux and Ubuntu)
subnet_id: subnet-id of your Amazon VPN
instance_type: I use t3.micro for the build and t2.2xlarge for the EAASI Server
security_groups: security group id -needs to allow public access to ports 80 and 443, and access to port 22 for you
elastic_IP_alloc: An Elastic IP address
```

