## Exercise 5: Using Conditions

### Objective:
Create a CloudFormation template that uses mappings to define region-specific AMI IDs for an EC2 instance.

### Steps:

1. Create a new CloudFormation template:

```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: "ami-0ff8a91507f77f867"
    us-west-1:
      AMI: "ami-0bdb828fd58c52235"

Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
    AllowedValues:
      - t2.micro
      - t2.small
      - t2.medium
    Description: "The EC2 instance type"

Resources:
  MyEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      InstanceType: !Ref InstanceType
      ImageId: !FindInMap [ RegionMap, !Ref "AWS::Region", AMI ]
```
2. Deploy the stack in different regions to verify the correct AMI ID is used based on the region.

3. Verify the instance creation in the EC2 console.