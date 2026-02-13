## How I would resolve the SSH timeout issue

# Verify the EC2 instance has a public IP address
Without a public IP (or Elastic IP), the instance cannot be reached from the internet, which would result in an SSH timeout.

# Check the subnet route table
Ensure the subnet has a route with destination 0.0.0.0/0 targeting an Internet Gateway, allowing internet-bound traffic to reach the instance.

# Review Network ACL rules
Confirm that the Network ACL allows both inbound and outbound traffic on port 22 (SSH), as NACLs are stateless and require rules in both directions.

# Confirm Security Group rules
Ensure the security group allows SSH (port 22) from the appropriate source (e.g. 0.0.0.0/0 or a specific IP range).