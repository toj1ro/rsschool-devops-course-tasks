## Infrastructure setup

1. Download and install AWS CLI package from AWS: https://awscli.amazonaws.com/AWSCLIV2.pkg
2. Download and install Terraform https://developer.hashicorp.com/terraform/install?product_intent=terraform
3. Check that everything is okay: `aws --version` and `terraform version`
4. Create IAM user with the following permission policies: 
- AmazonEC2FullAccess
- AmazonRoute53FullAccess
- AmazonS3FullAccess
- IAMFullAccess
- AmazonVPCFullAccess
- AmazonSQSFullAccess
- AmazonEventBridgeFullAccess
- AmazonDynamoDBFullAccess  
4.1 Create access keys for user
5. Configure AWS CLI credentials by providing access keys by `aws configure` command. Also specify region `eu-east-1`
6. Create github repository for Terraform code
7. Define and apply s3 bucket resource creating for storing terraform state.
8. Define and apply dynamo db table creating for implementation of locking mechanism.  
**NOTE**: Do not forget migrate your local state to the remote backend. 
9. Setup OIDC for github actions and AWS:
- Define and apply `aws_iam_openid_connect_provider` resource with all required parameters.
- Define and apply IAM role with required federated provider.
- Define and apply IAM permission policies for this role, also add `AmazonDynamoDBFullAccess` IAM permission to have
access for operations under dynamoDB lock table.  
10. Create github workflow:
- Define init, check, plan and apply jobs. Also cache all needed resources.
