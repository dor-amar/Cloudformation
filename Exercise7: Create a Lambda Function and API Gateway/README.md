## Exercise 7: Create a Lambda Function and API Gateway

### Objective:
Create a CloudFormation template to create a Lambda function and expose it via API Gateway.


### Steps:

1. Create a new CloudFormation template:

```yaml
Resources:
  MyLambdaExecutionRole:
    Type: "AWS::IAM::Role"
    Properties:
      AssumeRolePolicyDocument:
        Version: "2012-10-17"
        Statement:
          - Effect: "Allow"
            Principal:
              Service:
                - "lambda.amazonaws.com"
            Action:
              - "sts:AssumeRole"
      Policies:
        - PolicyName: "MyLambdaPolicy"
          PolicyDocument:
            Version: "2012-10-17"
            Statement:
              - Effect: "Allow"
                Action:
                  - "logs:CreateLogGroup"
                  - "logs:CreateLogStream"
                  - "logs:PutLogEvents"
                Resource: "arn:aws:logs:*:*:*"

  MyLambdaFunction:
    Type: "AWS::Lambda::Function"
    Properties:
      Handler: "index.handler"
      Role: !GetAtt MyLambdaExecutionRole.Arn
      Runtime: "nodejs12.x"
      Code:
        ZipFile: |
          exports.handler = async (event) => {
              const response = {
                  statusCode: 200,
                  body: JSON.stringify('Hello from Lambda!'),
              };
              return response;
          };

  MyApiGateway:
    Type: "AWS::ApiGateway::RestApi"
    Properties:
      Name: "MyApiGateway"

  MyApiGatewayResource:
    Type: "AWS::ApiGateway::Resource"
    Properties:
      ParentId: !GetAtt MyApiGateway.RootResourceId
      PathPart: "mylambda"
      RestApiId: !Ref MyApiGateway

  MyApiGatewayMethod:
    Type: "AWS::ApiGateway::Method"
    Properties:
      AuthorizationType: "NONE"
      HttpMethod: "GET"
      ResourceId: !Ref MyApiGatewayResource
      RestApiId: !Ref MyApiGateway
      Integration:
        IntegrationHttpMethod: "POST"
        Type: "AWS_PROXY"
        Uri: !Sub
          - "arn:aws:apigateway:${AWS::Region}:lambda:path/2015-03-31/functions/${MyLambdaFunction.Arn}/invocations"
          - { AWS::Region: !Ref "AWS::Region" }

  MyApiGatewayDeployment:
    Type: "AWS::ApiGateway::Deployment"
    Properties:
      RestApiId: !Ref MyApiGateway
      StageName: "prod"
    DependsOn:
      - MyApiGatewayMethod

  MyLambdaPermission:
    Type: "AWS::Lambda::Permission"
    Properties:
      Action: "lambda:InvokeFunction"
      FunctionName: !Ref MyLambdaFunction
      Principal: "apigateway.amazonaws.com"

```
2. Deploy the stack.

3. Verify the creation of the Lambda function and API Gateway in their respective consoles.

4. Test the API Gateway endpoint to ensure it triggers the Lambda function.