# Route 53 Notes

## Domain Registration

It allows you to register .com, .net. etc.

## Hosted Zone

A collection of DNS records.

### CNAME

- Route 53 charges for CNAME queries.
- CNAME can to point to any DNS record that is hosted anywhere.

### Alias

- Route 53 does not charge for Alias queries.
- An alias record can only point to Cloudfront distribution, Elastic Beanstalk env, ELB, S3 bucket as a static website, or to another record in the same hosted zone that you're creating the record in.

## Health Checks

If the health checks pass, you can send the instance to one of the domains registered in `Hosted Zone`.

## Traffic Flow

## Routing Policies

### Simple Policy

Simple DNS response providing the IP address associated with a name.

### Weighted Policy

With this policy, you can create a record set that allows traffic to go to different instances in either the same region or different region.

For example, 50% of traffic can go to an instance in region A and 2x 25% of the traffic can go two instances in region B. The use case for using this is if you want to route an experimental feature to 10% of the traffic coming in to your website, while the other 90% still go to your normal instance.

### Latency Routing Policy

This policy directs users to the lowest latency route possible.

## Failover Routing Policy

This policy does a health check of the primary instance and if the health check fails it will reroute to a secondary instance. You can test this by removing `Port 80` in SG.

### Geolocation Routing Policy

Think of Netflix and how it distributes certain contents to certain regions. This policy is different to `Latency Routing Policy` since you can **lock** certain contents to a certain region.

## Geoproximity Policy

Routes to the closest region within a geographic area.

### Failover Routing Policy

This policy allows you to route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy.
