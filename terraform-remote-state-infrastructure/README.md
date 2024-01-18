# Useful Hands-On.Cloud CloudFormation Templates - Terraform Remote State Infrastructure

## Deployment

```sh
aws cloudformation create-stack \
	--stack-name Terraform-Remote-State-Infrastructure \
	--template-body file://terraform-remote-state.yaml \
	--parameters \
		ParameterKey=ProjectName,ParameterValue=my-demo-project \
	--capabilities CAPABILITY_NAMED_IAM
	
aws cloudformation wait stack-create-complete --stack-name Terraform-Remote-State-Infrastructure
```

## Outputs

### S3 Bucket

```sh
aws cloudformation describe-stacks \
	--stack-name Terraform-Remote-State-Infrastructure \
	--query 'Stacks[0].Outputs[?OutputKey==`TerraformStateBucket`].OutputValue' \
	--output text
```

### DynamoDB Table

```sh
aws cloudformation describe-stacks \
	--stack-name Terraform-Remote-State-Infrastructure \
	--query 'Stacks[0].Outputs[?OutputKey==`TerraformStateDynamoDBTable`].OutputValue' \
	--output text
```

## Decommission

```sh
aws cloudformation delete-stack --stack-name Terraform-Remote-State-Infrastructure

aws cloudformation wait stack-delete-complete --stack-name Terraform-Remote-State-Infrastructure
```


Maintained by [https://hands-on.cloud](https://hands-on.cloud)
