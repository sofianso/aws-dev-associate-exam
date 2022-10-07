# EC2 Notes

## Types of EC2 Instances

1. Reserved Instances are only available for only 1 year or 3 years commitment. Ideally for steady workloads.
2. Spot Request Instances allows you to purchase spare capacity at a discounted rate, however, AWS can shut it down at any time. **Suitable for large computing job**.
3. On-Demand Instances is ideal for short term needs or unpredictable workloads.
4. Dedicated Instances.
5. Scheduled Reserved Instances.
6. Capacity Reservation.
7. Dedicated hosts provide dedicated hardware and they give you full visibility of sockets and cores and targeted instance placement.

## EC2 Volumes

- EBS provides persistent storage.
- Instance store volumes are non-persistent. When shut down, data is deleted.

## Public Subnets

We attached IGW to public subnets. EC2 instances must have a public IP address to connect to the internet.

## Private Subnets

Private subnets are usually used for Database related instances. It requires a NAT instance or NAT Gateway to connect to the internet via the public subnet.

## NAT Instance

- Managed by you.
- Scale up manually.
- No high availability.
- Need to assign SG.
- Can use bastion host.
- Use an Elastic IP address or public address with a NAT instance.
- Can implement port forwarding.

## NAT Gateway (Preferred Option)

- Managed by AWS.
- Elastic scalability up to 45 Gbps.
- Provides automatic high availability with an AZ and can be placed in multiple AZs.
- No SG.
- Cannot access through SSH.
- Elastic IP address can only be associated with a NAT Gateway at creation.
- Does not support port forwarding.
- Once you created a NAT Gateway, it'll automatically create an Elastic IP Address. You need to delete it once you delete a NAT Gateway not to be charged by AWS.

## How To SSH Into EC2 Instance

1. Copy the newly-created EC2 instance public IP address.
2. Change directory to where the key pair was downloaded in your computer.
3. In your terminal, enter `chmod <key_pair_file.pem>`
4. And then run `ssh ec2-user@<public IP address> <key_pair_file.pem>`

## Security Groups

- If you have two instances that needs to communicate with each other, you can allow communications between the two instances by creating a SG(`SG_A`) in the first EC2 instance that allows `All ICMP - IPv4` for the inbound rules with source set as `SG_B` for the second EC2 instance and vice versa.

## Metadata

SSH into your instance and then run `http://169.254.169.254/latest/meta-data/` to get list of metadata from your EC2 instance. The metadata allows you to retrieve IPv4, IPv6, SG, and etc of your instance.

**Additional note**, to get `user-date` of your instance, run `curl http://169.254.169.254/latest/user-data/`. This will list the bash scripts when the instance is ran.

## Monitoring

Status checks are performed every minute. There are two types of system checks: `System Status Checks` and `Instance Status Checks`.

`System Status Checks` tells you something is wrong with AWS and requires AWS help. `Instance Status Checks` does not require AWS help to fix.

## Stress Test

1. SSH into your EC2 instance and install `sudo yum install stress -y`.
2. To get more help run, `stress help`.
3. To run stress test, run `stress -c 8` which spins up 8 worker nodes.

## Facts About IP Addresses

### Public IP Address

- **Lost when the instance is stopped.**
- Used in Public Subnets.
- No charge.
- Associated with a private IP on the instance.

### Private IP Address

- Retained when the instance is stopped.
- Used in Public and Private Subnets.

### Elastic IP Address

- **Static Public IP address**
- **You are charged if NOT used.**
- Associated with a private IP address on the instance.
- Can be moved between instances and Elastic Network Adapters.
