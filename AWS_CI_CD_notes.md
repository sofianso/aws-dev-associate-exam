# AWS CI/CD Notes

## CodeCommit

Similar to GitHub.

### Three Types of Credentials

- Git credentials
- SSH Keys
- AWS Access Keys

## CodeBuild (Build & Test)

- Similar to Jenkins.
- It is a fully managed continuous integration (CI) - service that compiles source code, run tests, and produces software packages that are ready to deploy.
  AWS will scale, provision and manage the build servers.
- Multiple builds run concurrently, thus, builds are not left waiting in a queue.
- You pay based on the time it takes to complete the builds.
- CodeBuild takes source code from GitHub, CodeCommit, CodePipeline, S3, etc.
- Build instructions can be defined in the `buildpsec.yml` file.
  -Output logs can be configured to be sent to S3 and CloudWatch Logs.

## CodeDeploy (Deploy)

- Similar to Ansible.
- CodeDeploy contains information about what to deploy and how to deploy it.
- Need to choose compute platform in either:
  - EC2 or On-premises
    - With EC2, the file used by AWS CodeDeploy to define the deployment actions to execute for an Amazon EC2 deployment is named `appspec.yml`.
  - AWS Lambda (Can only be deployed with Blue/Green)
- Blue/Green traffic shifting
  - **Canary** is when traffic is shifted in two increments. Basically, you can specify percentage of traffic to your updated Amazon ECS task set / Lambda function before the remaining traffic is shifted in the second increment.
  - **Linear** is when traffic is shifted in equal increments with an equal number of minutes between each increment.
  - **All-at-once** is when all traffic is shifted to your updated Amazon ECS task set / Lambda function all at once.

## AWS CodePipeline

AWS CodePipeline automates the build, test, and deploy phases of the release process

### What Are Artifacts?

- Files or changes that will be worked on by the actions and stages in the pipeline.
- Each pipeline stage can create "artifacts".
- Artifacts are passed, stored in Amazon S3 and then passed on to the next stage.

## AWS CodeStar

Enable develops to quickly develop, build and deploy applications.
