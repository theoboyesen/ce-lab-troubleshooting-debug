## Scenario 2 – How I would diagnose and fix it

# Check the Security Group first
Since SSH (port 22) works but HTTP (port 80) does not, this suggests a port-specific filtering issue. Security groups are instance-level, easy to verify, and commonly misconfigured.

# Verify the Security Group inbound rule
Ensure there is an inbound rule allowing TCP traffic on port 80 from the internet (e.g. 0.0.0.0/0 or a restricted IP range).

# Check the Network ACL if the issue persists
Because Network ACLs are stateless, they must explicitly allow traffic in both directions.

# Verify Network ACL rules
Ensure the Network ACL allows inbound TCP traffic on port 80 and outbound TCP traffic on port 80.

# Justification
Because SSH access works but public HTTP access does not, this indicates a filtering issue rather than a routing issue.