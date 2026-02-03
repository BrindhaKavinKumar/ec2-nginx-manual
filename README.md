1. Title & Goal

# EC2 + Nginx (Manual Setup, Zero Magic)

This project demonstrates a manual setup of an EC2 instance running Nginx,
with a strong focus on understanding traffic flow, Linux services,
networking, and debugging.


2. Architecture Overview

## Architecture

User Browser
→ Internet
→ AWS Internet Gateway
→ Security Group
→ EC2 Instance
→ Nginx
→ HTML File


3. Step-by-Step Setup (high level, not tutorial spam)

## Setup Summary

1. Launch Ubuntu EC2 in public subnet
2. Allow SSH (22) and HTTP (80) in Security Group
3. SSH into instance
4. Install nginx using apt
5. Verify service with systemctl and curl


4. How Traffic Reaches the Server (MOST IMPORTANT SECTION)

## How Traffic Works

- Browser sends HTTP request to public IP
- Security Group allows TCP 80
- Linux kernel receives packet
- Nginx listens on port 80
- Nginx maps URL to /var/www/html
- HTML file is returned

5. Debugging Checklist (this differentiates you)

## Debugging Checklist

- Is the EC2 instance running?
- Can I SSH into it?
- Is nginx running?
- Does curl localhost work?
- Is port 80 listening?
- Is HTTP allowed in Security Group?
- Are nginx configs correct?
- Check logs (journalctl, nginx error.log)

6. Common Failures & Fixes

## Common Issues

| Issue | Root Cause | Fix |
|-----|-----------|-----|
| Website not loading | HTTP blocked in SG | Open port 80 |
| curl localhost fails | nginx stopped | systemctl start nginx |
| 404 error | File missing | Check /var/www/html |


7. Cost Awareness (huge bonus)

## Cost Notes

- Used t2.micro / t3.micro (free-tier eligible)
- Instance stopped when not in use

