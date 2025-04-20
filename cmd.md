# System Administration Commands

This repository contains a collection of the most used commands for system administration,DevOps engineers tasks. It includes commands for Nginx, grep, Docker, MySQL, and git.

## Table of Contents
- [Nginx](#nginx)
- [Grep](#grep)
- [Docker](#docker)
- [MySQL](#mysql)
- [Git](#git)
- [Linux/Bash](#linuxbash)
- [AWS CLI](#aws-cli)
- [Kubernetes](#kubernetes)
- [Ansible](#ansible)
- [Terraform](#terraform)
- .[logging](#logging)
## Nginx

### Basic Operations
```bash
# Start, stop, restart Nginx
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx  # Reload config without stopping

# Check Nginx status
sudo systemctl status nginx

# Test configuration validity
sudo nginx -t

# Display Nginx version
nginx -v
```

### Configuration
```bash
# Main configuration file locations
/etc/nginx/nginx.conf
/etc/nginx/sites-available/
/etc/nginx/sites-enabled/

# Create symbolic link from available to enabled
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/

# Remove config
sudo rm /etc/nginx/sites-enabled/example.com
```

### Logs
```bash
# Default log locations
/var/log/nginx/access.log
/var/log/nginx/error.log

# View logs in real time
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

## Grep

### Basic Usage
```bash
# Basic search in file
grep "pattern" filename

# Case insensitive search
grep -i "pattern" filename

# Recursive search in directory
grep -r "pattern" directory/

# Show line numbers
grep -n "pattern" filename

# Count matches
grep -c "pattern" filename

# Show only matching part
grep -o "pattern" filename
```

### Advanced Usage
```bash
# Extended regular expressions
grep -E "pattern1|pattern2" filename

# Invert match (show lines NOT matching)
grep -v "pattern" filename

# Show lines before/after/around match
grep -B 2 "pattern" filename  # 2 lines before
grep -A 2 "pattern" filename  # 2 lines after
grep -C 2 "pattern" filename  # 2 lines before and after

# Search for whole words only
grep -w "word" filename

# Quiet mode (just return exit status)
grep -q "pattern" filename && echo "Found" || echo "Not found"
```

## Docker

### Images
```bash
# List images
docker images

# Pull an image
docker pull image:tag

# Build an image
docker build -t name:tag .

# Remove image
docker rmi image:tag

# Clean up unused images
docker image prune
```

### Containers
```bash
# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Create and start container
docker run -d --name container_name image:tag

# Start/stop containers
docker start container_name
docker stop container_name

# Remove container
docker rm container_name

# Execute command in running container
docker exec -it container_name bash

# View container logs
docker logs container_name
docker logs -f container_name  # Follow log output
```

### Docker Compose
```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs

# Rebuild services
docker-compose build

# Scale specific service
docker-compose up -d --scale service=3
```

### Docker System
```bash
# Show Docker system info
docker info

# Check disk usage
docker system df

# Clean up
docker system prune  # Remove unused data
docker system prune -a  # Remove all unused data including volumes
```

## MySQL

### Connection
```bash
# Connect to MySQL server
mysql -u username -p

# Connect to specific database
mysql -u username -p database_name

# Connect to remote server
mysql -h hostname -u username -p database_name
```

### Database Operations
```bash
# Show databases
SHOW DATABASES;

# Create database
CREATE DATABASE dbname;

# Select database
USE dbname;

# Drop database
DROP DATABASE dbname;
```

### Table Operations
```bash
# List tables
SHOW TABLES;

# Show table structure
DESCRIBE tablename;
SHOW CREATE TABLE tablename;

# Create table
CREATE TABLE tablename (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

# Delete table
DROP TABLE tablename;
```

### Query Data
```bash
# Select data
SELECT * FROM tablename;
SELECT column1, column2 FROM tablename WHERE condition;

# Insert data
INSERT INTO tablename (column1, column2) VALUES ('value1', 'value2');

# Update data
UPDATE tablename SET column1='value1' WHERE condition;

# Delete data
DELETE FROM tablename WHERE condition;
```

### Administration
```bash
# User management
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON dbname.* TO 'username'@'localhost';
FLUSH PRIVILEGES;

# Export database (from command line)
mysqldump -u username -p database_name > backup.sql

# Import database (from command line)
mysql -u username -p database_name < backup.sql
```

## Git

### Setup & Configuration
```bash
# Set identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# List configuration
git config --list
```

### Basic Operations
```bash
# Initialize repository
git init

# Clone repository
git clone repository_url

# Check status
git status

# Stage changes
git add filename
git add .  # All files

# Commit changes
git commit -m "Commit message"
git commit -am "Commit message"  # Add & commit in one step

# View history
git log
git log --oneline
```

### Branches
```bash
# List branches
git branch

# Create branch
git branch branch_name

# Switch branch
git checkout branch_name
git switch branch_name  # Git 2.23+

# Create and switch in one command
git checkout -b branch_name
git switch -c branch_name  # Git 2.23+

# Merge branch
git merge branch_name

# Delete branch
git branch -d branch_name  # Safe delete
git branch -D branch_name  # Force delete
```

### Remote Operations
```bash
# Show remotes
git remote -v

# Add remote
git remote add origin repository_url

# Push to remote
git push origin branch_name

# Pull from remote
git pull origin branch_name

# Fetch from remote
git fetch origin
```

### Advanced Operations
```bash
# Stash changes
git stash
git stash pop
git stash list

# Create tag
git tag v1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"

# Rebase
git rebase main

# Cherry-pick
git cherry-pick commit_hash
```

## Linux/Bash

### File Operations
```bash
# List files
ls -l
ls -la  # Include hidden files

# Change directory
cd directory_name
cd ..  # Go up one level
cd ~   # Go to home directory

# Create directory
mkdir directory_name
mkdir -p path/to/nested/directory  # Create parent directories if needed

# Remove files/directories
rm filename
rm -r directory_name  # Recursive
rm -f filename  # Force
rm -rf directory_name  # Force recursive (use with caution)

# Copy files/directories
cp source destination
cp -r source_dir destination_dir  # Recursive

# Move/rename files
mv source destination

# Find files
find /path -name "pattern"
find /path -type f -name "*.txt"  # Find only files
find /path -type d -name "*dir*"  # Find only directories
```

### Text Processing
```bash
# View file content
cat filename
less filename
head -n 10 filename  # First 10 lines
tail -n 10 filename  # Last 10 lines
tail -f logfile  # Follow log file

# Search in files (see grep section)

# Word count
wc filename  # Lines, words, characters
wc -l filename  # Lines only

# Sort file content
sort filename
sort -r filename  # Reverse
sort -n filename  # Numeric sort

# Remove duplicates
uniq filename
sort filename | uniq  # Sort first, then remove duplicates

# Replace text
sed 's/search/replace/g' filename
```

### Process Management
```bash
# List processes
ps aux
ps -ef

# Process tree
pstree

# Find process by name
pgrep process_name
ps aux | grep process_name

# Kill process
kill pid
kill -9 pid  # Force kill
pkill process_name  # Kill by name

# Background/foreground
command &  # Run in background
fg        # Bring to foreground
bg        # Send to background
jobs      # List jobs
```

### System Information
```bash
# System info
uname -a
cat /etc/os-release
lsb_release -a

# Memory usage
free -h

# Disk usage
df -h
du -sh directory

# CPU info
cat /proc/cpuinfo
lscpu

# Check open ports
netstat -tulpn
ss -tulpn
```

## AWS CLI

### Authentication
```bash
# Configure AWS CLI
aws configure

# List profiles
aws configure list-profiles

# Use specific profile
aws --profile profile_name command
```

### EC2
```bash
# List instances
aws ec2 describe-instances

# Start/stop instance
aws ec2 start-instances --instance-ids i-1234567890abcdef0
aws ec2 stop-instances --instance-ids i-1234567890abcdef0

# Create instance
aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro --key-name MyKeyPair

# List AMIs
aws ec2 describe-images --owners self
```

### S3
```bash
# List buckets
aws s3 ls

# List objects in bucket
aws s3 ls s3://bucket-name

# Copy files
aws s3 cp file.txt s3://bucket-name/
aws s3 cp s3://bucket-name/file.txt ./

# Sync directories
aws s3 sync local_dir s3://bucket-name/path
aws s3 sync s3://bucket-name/path local_dir

# Create/remove bucket
aws s3 mb s3://bucket-name
aws s3 rb s3://bucket-name --force
```

### CloudFormation
```bash
# Create stack
aws cloudformation create-stack --stack-name MyStack --template-body file://template.yaml

# Update stack
aws cloudformation update-stack --stack-name MyStack --template-body file://template.yaml

# List stacks
aws cloudformation list-stacks

# Delete stack
aws cloudformation delete-stack --stack-name MyStack
```

## Kubernetes

### Cluster Information
```bash
# Cluster info
kubectl cluster-info

# Get nodes
kubectl get nodes

# API resources
kubectl api-resources
```

### Pods
```bash
# List pods
kubectl get pods
kubectl get pods -n namespace
kubectl get pods --all-namespaces

# Pod details
kubectl describe pod pod_name

# Create pod from file
kubectl apply -f pod.yaml

# Delete pod
kubectl delete pod pod_name
kubectl delete -f pod.yaml

# Execute command in pod
kubectl exec -it pod_name -- /bin/bash

# View pod logs
kubectl logs pod_name
kubectl logs -f pod_name  # Follow logs
```

### Deployments
```bash
# List deployments
kubectl get deployments

# Create/update deployment
kubectl apply -f deployment.yaml

# Scale deployment
kubectl scale deployment deployment_name --replicas=3

# Rollout status
kubectl rollout status deployment/deployment_name

# Rollback
kubectl rollout undo deployment/deployment_name
```

### Services
```bash
# List services
kubectl get services
kubectl get svc

# Create service
kubectl apply -f service.yaml

# Expose deployment as service
kubectl expose deployment deployment_name --type=NodePort --port=8080
```

### Configuration
```bash
# ConfigMaps and Secrets
kubectl get configmaps
kubectl get secrets

# Create ConfigMap
kubectl create configmap config-name --from-file=config.properties

# Create Secret
kubectl create secret generic secret-name --from-literal=key=value
```

### Context and Namespaces
```bash
# List contexts
kubectl config get-contexts

# Switch context
kubectl config use-context context_name

# List namespaces
kubectl get namespaces

# Create namespace
kubectl create namespace namespace_name

# Set default namespace
kubectl config set-context --current --namespace=namespace_name
```

## Ansible

### Inventory
```bash
# Ping all hosts
ansible all -m ping

# List hosts
ansible all --list-hosts
ansible-inventory --list

# Facts about hosts
ansible hostname -m setup
```

### Ad-hoc Commands
```bash
# Run command on hosts
ansible all -a "uptime"
ansible webservers -a "service httpd status"

# Run module
ansible all -m apt -a "name=nginx state=present" -b  # With become (sudo)
```

### Playbooks
```bash
# Run playbook
ansible-playbook playbook.yml

# Check mode (dry run)
ansible-playbook playbook.yml --check

# Run with variables
ansible-playbook playbook.yml -e "variable=value"

# Limit to specific hosts
ansible-playbook playbook.yml --limit hostname
```

### Vault
```bash
# Create encrypted file
ansible-vault create secret.yml

# Edit encrypted file
ansible-vault edit secret.yml

# Encrypt existing file
ansible-vault encrypt file.yml

# Decrypt file
ansible-vault decrypt file.yml

# Run playbook with vault
ansible-playbook playbook.yml --ask-vault-pass
ansible-playbook playbook.yml --vault-password-file vault_pass.txt
```

## Terraform

### Initialization and Planning
```bash
# Initialize working directory
terraform init

# Update providers
terraform init -upgrade

# Format code
terraform fmt

# Validate configuration
terraform validate

# Show execution plan
terraform plan
terraform plan -out=tfplan  # Save plan to file
```

### Apply and Destroy
```bash
# Apply changes
terraform apply
terraform apply tfplan  # Apply saved plan

# Destroy resources
terraform destroy
terraform destroy -target=resource_type.resource_name  # Specific resource
```

### State Management
```bash
# List resources in state
terraform state list

# Show resource details
terraform state show resource_type.resource_name

# Move resource in state
terraform state mv source_resource target_resource

# Remove resource from state
terraform state rm resource_type.resource_name

# Pull current state
terraform state pull > terraform.tfstate

# Push state
terraform state push terraform.tfstate
```

### Workspaces
```bash
# List workspaces
terraform workspace list

# Create workspace
terraform workspace new workspace_name

# Select workspace
terraform workspace select workspace_name

# Delete workspace
terraform workspace delete workspace_name
```

### Modules and Providers
```bash
# Get modules
terraform get
terraform get -update

# Providers
terraform providers
terraform providers lock  # Create lock file
```

## Logging
### Export customersbackend log and compress it:
```bash
sudo journalctl -u customersbackend --since "1 day ago" | zstd -7 -o /tmp/customersbackend.log.zst
```
