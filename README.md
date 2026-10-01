## AWS VPC Peering — Hands-on Practice

This repository documents my hands-on practice with AWS VPC Peering, including VPC peering concepts, AWS CLI commands, route table configuration, IAM permissions, and route verification.

---

## What I Learned

- What is VPC Peering and how it works
- Requester VPC and Accepter VPC
- Same Region and Cross-Region VPC Peering
- Same Account and Different Account VPC Peering
- VPC CIDR blocks and overlapping CIDR issue
- VPC Peering is non-transitive
- VPC Peering Connection ID (PCX)
- Route Tables and routing
- Main and Explicit Route Table Association
- `local` route
- Internet Gateway route
- NAT Gateway route
- `blackhole` route status
- IAM permissions required for VPC Peering operations
- AWS CLI commands for VPC Peering
- Using JMESPath `--query` with AWS CLI

---

## VPCs Used

| VPC | CIDR |
|---|---|
| Custom VPC | `10.0.0.0/16` |
| Default VPC | `172.31.0.0/16` |

The CIDR blocks must not overlap because overlapping IP ranges cannot be routed correctly between peered VPCs.

---

## VPC Peering Process

1. Create VPC Peering request
2. Accept the peering request
3. Verify peering status
4. Add routes in both VPC route tables
5. Verify both routes
6. Test connectivity when resources are available

---

## Hands-on Environment

### Custom VPC

- VPC ID: `<CUSTOM_VPC_ID>`
- CIDR: `10.0.0.0/16`
- Route Table ID: `<CUSTOM_ROUTE_TABLE_ID>`

### Default VPC

- VPC ID: `<DEFAULT_VPC_ID>`
- CIDR: `172.31.0.0/16`
- Route Table ID: `<DEFAULT_ROUTE_TABLE_ID>`

### VPC Peering Connection

- Peering ID: `<PEERING_CONNECTION_ID>`
- Region: `ap-south-1`
- Final Status: `active`

---

# AWS CLI Commands Practiced

## 1. Check VPCs

```bash
aws ec2 describe-vpcs \
  --region ap-south-1 \
  --query 'Vpcs[*].[VpcId,CidrBlock,IsDefault,State]' \
  --output table \
  --no-cli-pager
