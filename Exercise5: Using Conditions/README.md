## Exercise 5: Using Conditions

### Objective:
Create a CloudFormation template that uses conditions to control resource creation based on a parameter.

### Steps:

1. Create a new CloudFormation template:

```yaml
Parameters:
  EnvType:
    Description: Environment type
    Type: String
    Default: test
    AllowedValues:
      - prod
      - test

Conditions:
  CreateProdResources: !Equals [ !Ref EnvType, prod ]

Resources:
  MyS3Bucket:
    Type: "AWS::S3::Bucket"
    Condition: CreateProdResources
    Properties:
      BucketName: my-prod-bucket-12345

```
2. Deploy the stack, providing different values for the EnvType parameter.

3. Verify the bucket creation only when the EnvType parameter is set to prod.