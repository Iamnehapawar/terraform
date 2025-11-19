# Terraform Project – Deploying an EC2 Instance on AWS

This project demonstrates how to provision an AWS EC2 Instance along with a Security Group using Terraform.

## Project Overview
Creating a custom Security Group

Launching an EC2 instance

Running Terraform lifecycle commands

Destroying the infrastructure after use

## Terraform Configuration
### main.tf

```hcl
resource "aws_instance" "myweb" {
  ami           = "ami-0cae6d6fe6048ca2c"
  instance_type = "t2.micro"
  key_name      = "terraform"

  vpc_security_group_ids = [
    aws_security_group.my-sg.id
  ]

  tags = {
    Name = "webapp"
  }
}

resource "aws_security_group" "my-sg" {
  name = "tf-sg"

  ingress {
    description = "allow ssh"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "allow http"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "allow https"
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    description = "allow all traffic"
    from_port   = 0
    to_port     = 0
    protocol    = -1
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```


    
  


    
    

## Terraform Script in VS Code
![](./img/vs%20code%20terraform.png)

## EC2 Instance on AWS Console
![](./img/launch%20ec2.png)

## How to Run the Project
### Initialize
terraform init

### Plan
terraform plan

### Apply
terraform apply -auto-approve

### Destroy
terraform destroy -auto-approve

### Outcome
EC2 instance created

Security group attached

Infrastructure fully managed using Terraform

### Conclusion
This project demonstrates real-world Terraform and AWS provisioning with clear IaC concepts.
