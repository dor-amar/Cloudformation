## Exercise 3: Create an EC2 Instance 

### Objective:
Create a CloudFormation template to launch an EC2 instance with specified parameters.

### Steps:

1. Create a new CloudFormation template:

```yaml
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
      ImageId: "ami-071878317c449ae48"  

```
3. Replace `ami-071878317c449ae48` with a valid AMI ID for your region. You can find this information in the AWS Management Console under EC2 > AMIs.
4. Deploy the stack, choosing an instance type.
5. Verify the instance creation in the EC2 console.