# Elastic Beanstalk Notes

## Web Server Environment

## Worker Environment

If your AWS Elastic Beanstalk application performs operations or workflows that take a long time to complete, you can offload those tasks to a dedicated worker environment.

## Deployment Policies

- All at once
  - Deploys the new version to all instances simultaneously.
    - Fastest deployment.
    - Out while the deployment is taking place.
    - Not ideal for production since if it fails it needs to re-deploy the original version of all your instances.
- Rolling
  - Update a batch of instances and move the next one once the first batch is healthy.
- Rolling with additional batch
  - Like Rolling but launces new instances in a new batch ensuring that there is a full availability.
- Immutable
  - Launches new instances in a new ASG and deploys the version update to these instances before swapping traffic to these instances before healthy.
- Blue/green:
  - Create a new "stage" environment and deploy updates there.

## .ebextensions

The .ebextensions file is used to add configuration files to the source code. Extensions are a zip file containing code that must be deployed to Elastic Beanstalk.
