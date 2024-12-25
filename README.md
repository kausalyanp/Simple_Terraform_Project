# Simple Terraform Project
 Terraform is an Infrastructure as Code (IaC) tool that allows you to define and provision infrastructure resources using configuration files. Here’s a step-by-step guide to learning Terraform for AWS using an Ubuntu server.

## Step 1: Install Terraform on Ubuntu
Update the system packages:
```
sudo apt update && sudo apt upgrade -y
```
Install required dependencies:
```
sudo apt install -y gnupg software-properties-common curl
```
Add the HashiCorp GPG key:
```
$ wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```
Verify the key's fingerprint:
```
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```
Add the official HashiCorp repository to your system:
```
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```
Download the package information from HashiCorp.
```
$ sudo apt update
```
Install Terraform from the new repository.
```
$ sudo apt-get install terraform
```

## Step 2: Set Up AWS Credentials
Download the AWS CLI installer:
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```
Install the unzip utility (if not already installed):
```
sudo apt install unzip -y
```
Unzip the downloaded file:
```
unzip awscliv2.zip
```
Run the installer:
```
sudo ./aws/install
```
Verify the installation:
```
aws --version
```

## Step 3: Create a Terraform Project
Create a project directory:
```
mkdir terraform-aws && cd terraform-aws
```
Create a main Terraform configuration file:
```
vi main.tf
```
Write a basic configuration to launch an EC2 instance:
```
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c2b8ca1dad447f8a" # Amazon Linux 2 AMI
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-Example"
  }
}
```

## Step 4: Initialize and Apply Terraform
Initialize Terraform:
```
terraform init
```
Validate the configuration:
```
terraform validate
```
Plan the infrastructure:
```
terraform plan
```
Apply the configuration:
```
terraform apply
```
Type yes to confirm. Verify the EC2 instance in the AWS Management Console.

Destroy resources:
```
terraform destroy
```
Type yes to confirm.
