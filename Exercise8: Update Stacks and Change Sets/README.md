## Exercise 8: Update and Change Sets

### Objective:
Update an existing stack using change sets.

### Steps:

1. Modify the EC2 instance (Exercise 3) template to add a security group:

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
  MySecurityGroup:
    Type: "AWS::EC2::SecurityGroup"
    Properties:
      GroupDescription: "Allow SSH access"
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0

  MyEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      InstanceType: !Ref InstanceType
      ImageId: "ami-0ff8a91507f77f867"
      SecurityGroups:
        - !Ref MySecurityGroup

```
2. Create a change set for the stack.

3. Review and execute the change set.

4. Verify the updates in the EC2 and Security Groups console.