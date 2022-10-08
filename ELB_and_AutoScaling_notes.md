# Elastic Load Balancers & Auto Scaling Notes

## Network Load Balancer

1. Low latency and high performance.
2. Connect using TCP/UDP.
3. Requires Target Group for Routing.

## Application Load Balancer

### Path-Based Routing

1. Connect using HTTP/HTTPS.
2. Edit the `Rules` of the ALB to hit a different Target Groups. For example, `/home` will hit `TG1` and `/orders` will hit `TG2`.

### Host-Based Routing

1. Connect using HTTP/HTTPS.
2. To set this up, you must use `Hosted Zones` to create a Record Set that will use an `Alias` to point at the load balancers.
3. Edit the `Rules` of the ALB to hit a different Target Groups. For example, `www.store.home.com` will hit `TG1` and `www.blogs.home.com` will hit `TG2`.

## Auto Scaling Group

### Launch Configuration

1. Launch Configuration cannot be edited. It can only be deleted or copied.

### Launch Template (Newer)

Launch Template is basically a Launch Configuration with additional custom settings such as using Spot or On-Demand instances.

### Auto Scaling Health Checks

By default, ASG uses EC2 Status Checks. However, AWS recommends that Auto Scaling relies on ELB Health Checks to check if an instance is healthy or not. You need to **manually modify** this on the ASG settings to enable `Health Checks` to `ÈLB`.

### EC2 Monitoring

By default, EC2 sends basic monitoring every 5 minutes. Detailed monitoring sends metrics every 1 minute (chargeable).

### Auto Scaling Termination Policies

By default, it will delete the extra instance in the multiple AZs. However, you can set how the instance gets terminated in ASG settings.

### Cross-Zone Load Balancing

**Cross-Zone Load Balancing** allows all traffic to be distributed evenly on all instances. For example, AZ1 has 3 instances while AZ2 has 2 instances. If we don't enable **Cross-Zone Load Balancing**, AZ1 will get 50% of the traffic instead of 60% of of the traffic. By default, **Cross-Zone Load Balancing** is disabled when using NLB. With ALB, **Cross-Zone Load Balancing** is enabled and cannot be disabled.

### ELB Sticky Sessions

ELB Sticky Sessions is useful for ecommerce websites. For example, it allows the website to keep track of the user's activities to keep their cookie until it expires.

### Scaling Types

#### Target Tracking Policy

This policy adds/removes instances as required to keep the metric to the specific target value.

#### Simple Scaling Policy

Waits until health check and cool down period expires before re-evaluating. AWS recommends this for most cases.

#### Step Scaling Policy

Increase or decrease the current capacity of your ASG based on a set of scaling adjustments.
