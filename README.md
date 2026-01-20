# Lab M2.09 - Troubleshooting and Debugging

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-troubleshooting-debug](https://github.com/cloud-engineering-bootcamp/ce-lab-troubleshooting-debug)

**Activity Type:** Individual  
**Estimated Time:** 45-60 minutes

## Learning Objectives

- [ ] Practice systematic troubleshooting
- [ ] Debug common deployment issues
- [ ] Use CloudWatch Logs for debugging
- [ ] Create troubleshooting documentation
- [ ] Implement fixes for broken deployments

## Your Task

You're given scenarios with intentionally broken configurations. Find and fix each issue:

### Scenario 1: Can't SSH to Instance
- Instance is running
- Security group looks correct
- Connection times out

**Your job:** Diagnose and fix

### Scenario 2: Website Not Loading
- Can SSH to instance
- Application is running
- curl localhost:80 works
- Public access fails

**Your job:** Diagnose and fix

### Scenario 3: Application Crashes
- Starts successfully
- Crashes after 30 seconds
- Error: "Cannot connect to database"

**Your job:** Diagnose and fix

## Troubleshooting Commands

```bash
# Instance diagnostics
aws ec2 describe-instances --instance-ids i-xxxxx
aws ec2 describe-instance-status --instance-ids i-xxxxx

# Security group check
aws ec2 describe-security-groups --group-ids sg-xxxxx

# Network testing
nc -zv instance-ip port
telnet instance-ip port
curl -v http://instance-ip

# On instance
ps aux | grep APPLICATION
systemctl status SERVICE
journalctl -u SERVICE -n 50
tail -f /var/log/messages
ss -tuln | grep PORT
```

## 📤 What to Submit

**Submission Type:** GitHub Repository

Create a **public** GitHub repository named `ce-lab-troubleshooting` containing:
- `TROUBLESHOOTING-GUIDE.md` - Your methodology
- `scenario-1-solution.md` - How you fixed scenario 1
- `scenario-2-solution.md` - How you fixed scenario 2
- `scenario-3-solution.md` - How you fixed scenario 3
- `debugging-commands.sh` - Useful commands
- Screenshots of before/after

## Grading: 100 points
- Scenario solutions: 60pts (20 each)
- Troubleshooting methodology: 20pts
- Documentation: 20pts
