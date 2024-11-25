###Terraform-Managed AWS Infrastructure: Scalable 2-Tier Architecture

This repository contains Terraform configurations for deploying a scalable 2-tier architecture on AWS. The infrastructure includes internet-facing and internal load balancers, auto-scaling groups, and associated networking components.

---

## Repository Structure

terraform-aws-2-tier-architecture/

── main.tf               # Contains your Terraform configuration
── variables.tf          # (Optional) Define input variables for customization
── outputs.tf            # (Optional) Define output values
── terraform.tfstate     # (Auto-generated, DO NOT upload this file)
── terraform.tfstate.backup # (Auto-generated, DO NOT upload this file)
── README.md             # Project documentation
── .gitignore            # Specify files to ignore in version control



**Architecture Overview**
1. **VPC**:
   - CIDR Block: `10.0.0.0/16`
   - DNS Support and DNS Hostnames enabled.
2. **Subnets**:
   - 2 Public Subnets (across 2 Availability Zones).
   - 1 Private Subnet.
3. **Internet Gateway**:
   - Allows public traffic to access resources in public subnets.
4. **Route Tables**:
   - Public Route Table with a default route to the Internet Gateway.
5. **Security Groups**:
   - **Web Server SG**: Allows HTTP (80) and SSH (22) traffic.
   - **Database SG**: Allows MySQL (3306) traffic only from the private subnet.
6. **Compute Resources**:
   - EC2 instance running in the public subnet for web services.
7. **Database**:
   - RDS MySQL instance deployed in a private subnet.

---

**Getting Started**

**Prerequisites**
- [Terraform CLI](https://developer.hashicorp.com/terraform/downloads) installed.
- AWS account with appropriate permissions.
- AWS CLI configured with your credentials.
- S3 bucket for Terraform state (recommended)

---

## Steps to Deploy

1. Clone the repository:
```bash
git clone https://github.com/yourusername/terraform-aws-2tier.git
cd terraform-aws-2tier
```

2. Initialize Terraform:
```bash
terraform init
```

3. Create a `terraform.tfvars` file with your variables:
```hcl
aws_region = "us-west-2"
environment = "dev"
vpc_cidr = "10.0.0.0/16"
public_subnets = ["10.0.1.0/24", "10.0.2.0/24"]
private_subnets = ["10.0.3.0/24", "10.0.4.0/24"]
```

4. Review the execution plan:
```bash
terraform plan
```

5. Apply the configuration:
```bash
terraform apply
```

## Module Details

### Networking Module
- Creates VPC with public and private subnets
- Sets up Internet Gateway and NAT Gateways
- Configures route tables and network ACLs

### Security Module
- Defines security groups for ALBs, web tier, and app tier
- Implements network ACLs
- Sets up IAM roles and policies

### Load Balancers Module
- Configures internet-facing ALB for web tier
- Sets up internal ALB for app tier
- Defines listener rules and target groups

### Autoscaling Module
- Creates Launch Templates for web and app tiers
- Configures Auto Scaling Groups
- Implements scaling policies based on metrics

## Configuration Files

### main.tf
```
content...
```

### variables.tf
```
content...
```

## Security Considerations

- All resources are deployed with least-privilege permissions
- Private subnets are not accessible from the internet
- Security groups follow the principle of minimal access
- Sensitive data should be stored in AWS Secrets Manager
- Enable VPC Flow Logs for network monitoring

## Monitoring and Maintenance

The infrastructure includes:
- CloudWatch metrics for Auto Scaling Groups
- ALB access logs stored in S3
- VPC Flow Logs for network monitoring
- Custom metrics for application monitoring

## Cost Optimization

- Use Spot Instances in Auto Scaling Groups where appropriate
- Implement automatic scaling based on demand
- Configure lifecycle hooks to gracefully handle instance termination
- Use AWS Cost Explorer to monitor spending

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License - See LICENSE file for details
