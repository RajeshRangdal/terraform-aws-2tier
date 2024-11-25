Terraform-Managed AWS Infrastructure: Scalable 2-Tier Architecture

This project sets up a scalable two-tier architecture on AWS using Terraform. The architecture includes a public-facing web server (EC2) and a backend database (RDS).

---

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

---

**Steps to Deploy**

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/<your-username>/terraform-aws-2-tier-architecture.git
   cd terraform-aws-2-tier-architecture
