# VPC Notes

## Route Tables

NAT Gateway must be in a public subnet.

You use `AAAA` for IPv6 address for in `Hosted Zones`.

### NACL

- NACL is a firewall at a subnet level.
- It either only ALLOW or DENY.
- Stateless (SG is Stateful)
- Process rules in order.
- NACL is useful to blocking a certain IP address from trying to reach your instance.
