## How I Would Diagnose and Fix the Issue

# Check the database security group

First, I would verify the security group attached to the database. This is the most common cause and the quickest to validate.

I would ensure the database security group allows:
- Inbound TCP traffic on port 3306
- Source: the application instance’s security group
- This ensures the application is permitted to connect to the database using least-privilege access.

# Verify Network ACL rules

If the security group configuration is correct, I would then check the Network ACL associated with the database subnet.

Because Network ACLs are stateless, I would confirm that:
- Inbound TCP traffic on port 3306 is allowed
- Outbound TCP traffic on port 3306 is also allowed
- Blocking either direction would cause connection timeouts and application crashes.

# Confirm database availability

Next, I would verify that the database service itself is:
- Running
- Listening on the expected port
- Reachable from within the VPC

If the database were stopped or unhealthy, the application would fail after connection retries.

# Validate application database configuration

Finally, I would review the application’s database configuration to ensure:
- The database endpoint/hostname is correct
- The port matches the database listener
- Credentials and environment variables are correctly set
- An incorrect endpoint or misconfigured connection string would also result in connection timeouts.

## Justification

Because the application starts successfully but crashes after a delay with a database connection error, this indicates a dependency connectivity issue rather than an application startup failure. The most likely causes are network filtering or database availability issues.