Terraform Module to provision an EC2 Instance that is running Apache.

Not for production use. Just showcasing how to create a custom module on Terraform Registry.

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.22.0"
    }
  }
}

provider "aws" {
  region = "eu-north-1"
}


module "apache" {
  source = ".//terraform-aws-apache-example"
  vpc_id = "vpc-0000000000"
  my_ip_with_cidr = "MY_OWN_IP_ADDRESS/32"
  public_key = "ssh-rsa AAAAB ..."
  instance_type = "t3.micro"
  server_name = "Apache Example Server"
}

output "public_ip" {
  value = module.apache.public_ip
}

```