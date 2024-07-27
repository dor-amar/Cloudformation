## Exercise 2: Add Parameters and Outputs  

### Objective:
Enhance the previous template with parameters for bucket name and output the bucket's ARN.

### Steps:

1. Modify the template to include parameters:

```yaml
Parameters:
  BucketNameParameter:
    Type: String
    Description: "The name of the S3 bucket"

Resources:
  MyS3Bucket:
    Type: "AWS::S3::Bucket"
    Properties:
      BucketName: !Ref BucketNameParameter

Outputs:
  BucketARN:
    Description: "The ARN of the S3 bucket"
    Value: !GetAtt MyS3Bucket.Arn

```
3. Create a new stack with the updated template, providing a unique bucket name as a parameter.
4. Verify the bucket creation and check the output in the CloudFormation console.