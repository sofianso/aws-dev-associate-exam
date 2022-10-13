# AWS Cloudformation

## What does CloudFormation Contain?

1. Resources (EC2 instance, S3)
2. Parameters (optional)
3. Mappings (optional) - With mappings you can, for example, set values based on a region. You can create a mapping that uses the region name as a key and contains the values you want to specify for each specific region.
4. Outputs (optional)
5. Conditions (optional)
6. Transform (optional)

## Change Sets

Change sets provide a summary of proposed changes to your stack that allows you to see how those changes might impact existing resources before implementing them.

## Intrinsic Functions

There are a few built-in intrinsic functions in Cloudformation:

1. `!Ref` refers to the value of the specified value or resource.
2. `Fn::GetAtt` returns the value of an attribute from a resource in the template.
3. `Fn::FindInMap` returns the value corresponding to keys in a two-level map that is declared in the Mappings section.
