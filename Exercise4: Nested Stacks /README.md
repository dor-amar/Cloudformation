## Exercise 4: Nested Stacks 

### Objective:
Create a parent stack that includes nested stacks for better organization.

### Steps:

1. Create a nested stack template for an S3 bucket:

```yaml
Resources:
  NestedS3Bucket:
    Type: "AWS::S3::Bucket"
    Properties:
      BucketName: my-nested-bucket-12345
```
2. Upload the nested-s3-bucket.yaml file to an S3 bucket. Note the URL of the uploaded file.

3. Create a parent stack template that references the nested stack:
```yaml
Resources:
  MyNestedStack:
    Type: "AWS::CloudFormation::Stack"
    Properties:
      TemplateURL: "URL_TO_YOUR_s3-bucket.yaml"
```

4. Deploy the parent stack.
5. Verify the nested stack creation in the CloudFormation console.