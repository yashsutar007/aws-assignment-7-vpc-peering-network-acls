# Assignment 7 - VPC Peering and Network ACLs

## Overview

This project demonstrates how to establish private communication between two Amazon Virtual Private Clouds (VPCs) using **AWS VPC Peering**. Two VPCs with different CIDR blocks were created, connected through a VPC Peering Connection, and configured with custom route tables and Network ACLs. Connectivity between the VPCs was successfully verified using Amazon EC2 instances.

---

## Objective

- Create two VPCs with different CIDR blocks.
- Establish a VPC Peering Connection.
- Configure route tables for inter-VPC communication.
- Verify Network ACL configuration.
- Launch EC2 instances in both VPCs.
- Test connectivity using private IP addresses.

---

## AWS Services Used

- Amazon VPC
- Amazon EC2
- VPC Peering Connection
- Internet Gateway
- Route Tables
- Public Subnets
- Security Groups
- Network ACLs

---

## Network Design

### VPC-A

| Property | Value |
|----------|-------|
| CIDR Block | 10.10.0.0/16 |
| Public Subnet | 10.10.1.0/24 |
| EC2 Private IP | 10.10.1.26 |

### VPC-B

| Property | Value |
|----------|-------|
| CIDR Block | 10.20.0.0/16 |
| Public Subnet | 10.20.1.0/24 |
| EC2 Private IP | 10.20.1.89 |

---

## Project Architecture

```text
                         Internet
                             |
                 +-----------+-----------+
                 |                       |
             Internet Gateway      Internet Gateway
                 |                       |
          +------+-------+       +-------+------+
          |    VPC-A     |       |    VPC-B     |
          |10.10.0.0/16  |       |10.20.0.0/16  |
          |              |       |              |
          | PublicSubnet |       | PublicSubnet |
          |10.10.1.0/24  |       |10.20.1.0/24  |
          |              |       |              |
          | EC2-VPC-A    |       | EC2-VPC-B    |
          |10.10.1.26    |       |10.20.1.89    |
          +------+-------+       +-------+------+
                 \                     /
                  \                   /
                   \                 /
                  VPC Peering Connection
```

---

## Implementation Steps

1. Created **VPC-A** (10.10.0.0/16).
2. Created **VPC-B** (10.20.0.0/16).
3. Created one public subnet in each VPC.
4. Attached an Internet Gateway to both VPCs.
5. Created custom Route Tables.
6. Associated Route Tables with public subnets.
7. Launched Ubuntu EC2 instances.
8. Created and accepted a VPC Peering Connection.
9. Updated Route Tables with peering routes.
10. Verified Network ACL configuration.
11. Connected to EC2 using SSH.
12. Successfully tested connectivity using the `ping` command.

---

## Connectivity Test

The connectivity between EC2 instances was verified using private IP addresses.

Command used:

```bash
ping 10.20.1.89
```

Result:

- 11 packets transmitted
- 11 packets received
- 0% packet loss

This confirms that the VPC Peering Connection and routing configuration were successfully implemented.

---

## Project Structure

```
Assignment-7-VPC-Peering-Network-ACLs/
│
├── README.md
├── Report/
│   └── Assignment_7_Report.pdf
│
├── Screenshots/
│   ├── 01-created-vpc-a.png
│   ├── 02-created-vpc-b.png
│   ├── 03-subnet-vpc-a.png
│   ├── 04-subnet-vpc-b.png
│   ├── 05-igw-vpc-a.png
│   ├── 06-igw-vpc-b.png
│   ├── 07-route-table-vpc-a.png
│   ├── 08-route-table-vpc-b.png
│   ├── 09-ec2-vpc-a.png
│   ├── 10-ec2-vpc-b.png
│   ├── 11-vpc-peering.png
│   ├── 12-updated-route-table-vpc-a.png
│   ├── 13-updated-route-table-vpc-b.png
│   ├── 14-network-acl-vpc-a.png
│   ├── 15-network-acl-vpc-b.png
│   ├── 16-ssh-login.png
│   └── 17-connectivity-test.png
```

---

## Learning Outcomes

After completing this assignment, I learned how to:

- Design multiple VPCs with different CIDR blocks.
- Configure Internet Gateways and Route Tables.
- Launch EC2 instances inside custom VPCs.
- Establish secure communication using VPC Peering.
- Configure and verify Network ACLs.
- Test private communication between EC2 instances.
- Troubleshoot AWS networking issues related to routing and security.

---

## Challenges Faced

- SSH connectivity initially failed because the public IP address changed, requiring an update to the Security Group rule.
- Route tables had to be configured correctly in both VPCs to enable communication.
- Connectivity was verified only after confirming Security Groups, Route Tables, Internet Gateways, and VPC Peering configuration.

---

## Conclusion

This project successfully demonstrated the implementation of **AWS VPC Peering** for secure communication between two isolated VPCs. Custom networking components, including subnets, Internet Gateways, Route Tables, Security Groups, and Network ACLs, were configured correctly. Connectivity between EC2 instances was successfully verified using private IP addresses, demonstrating a working inter-VPC networking solution.

