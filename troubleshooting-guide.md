# Troubleshooting Guide

## Overview

This guide documents a **structured troubleshooting methodology** for diagnosing and resolving common infrastructure and application issues in an AWS environment. The approach focuses on identifying symptoms, mapping them to the correct layer, and applying targeted fixes rather than guessing or changing configurations at random.

The same methodology is applied consistently across all scenarios in this lab.

---

## Troubleshooting Methodology

### 1. Identify the Symptom Clearly
The first step is to understand **what is failing** and **how it is failing**.

Examples:
- Connection **timeout** vs **permission denied**
- Application **fails immediately** vs **crashes after a delay**
- Local access works but **public access fails**

The exact symptom provides strong clues about which layer is responsible.

---

### 2. Map the Failure to the Correct Layer

Each issue is mapped to a specific layer before attempting a fix:

| Symptom | Likely Layer |
|------|-------------|
| SSH timeout | Network / routing |
| One port works, another fails | Traffic filtering |
| App crashes after delay | External dependency |
| Local access works, public fails | Security controls |

This prevents unnecessary changes and speeds up diagnosis.

---

### 3. Follow the Traffic or Dependency Path

Troubleshooting always follows the **path of the request**:

- **User → AWS → Instance**
- **Application → External Service (e.g. database)**

By following the path step-by-step, it becomes easier to identify where the failure occurs.

---

### 4. Troubleshoot from Most Likely to Least Likely

Issues are checked in the following order:

1. **Closest to the resource**
   - Security Groups
   - Application configuration
2. **Subnet-level controls**
   - Network ACLs
3. **Routing components**
   - Route tables
   - Internet Gateways
4. **Service health**
   - Application processes
   - Database availability

This mirrors real-world cloud troubleshooting and avoids unnecessary changes.

---

### 5. Use Commands as Evidence, Not Guesswork

Commands are used to **validate assumptions**, not replace reasoning.

Examples:
- `curl` or `nc` to test port reachability
- AWS CLI commands to inspect configuration
- Service logs to confirm application behaviour

Each command is tied to a specific hypothesis.

---

## Common Diagnostic Patterns

### Timeout Errors
- Indicates traffic is not reaching its destination
- Common causes:
  - Missing routes
  - Blocked ports
  - Network ACL rules

---

### Port-Specific Failures
- One service works while another fails
- Strongly indicates **filtering issues**
- Check:
  - Security Groups
  - Network ACLs

---

### Delayed Application Crashes
- Often caused by failed connections to external services
- Common causes:
  - Database not reachable
  - Blocked database port
  - Incorrect service endpoint

---

## Key AWS Components and Their Roles

### Security Groups
- Instance-level firewall
- Stateful
- Controls inbound and outbound traffic per port

### Network ACLs
- Subnet-level firewall
- Stateless
- Requires explicit inbound and outbound rules

### Route Tables
- Control traffic routing
- Do not filter by port

### Internet Gateway
- Enables internet access for a VPC
- Required for public connectivity

---

## Guiding Principles

- **Never assume** — always validate
- **Fix the cause, not the symptom**
- **Change one thing at a time**
- **Use the simplest explanation that fits the evidence**

---

## Conclusion

This troubleshooting approach emphasizes structured reasoning, clear symptom analysis, and targeted validation. By consistently applying this methodology, issues can be resolved efficiently while minimizing risk and unnecessary configuration changes.
