## Exercise 1: Create an S3 Bucket 

### Objective:
Create a simple CloudFormation template to create an S3 bucket.

### Steps:

1. Open the CloudFormation console.
2. Create a new stack and use the following template:

```yaml
Resources:
  MyS3Bucket:
    Type: "AWS::S3::Bucket"
    Properties:
      BucketName: my-unique-bucket-name-12345
```
3. Deploy the stack.
4. Verify the bucket creation in the S3 console.