# Useful Hands-On.Cloud CloudFormation Templates - AWS Budget -> SQS -> Lambda integration

<img alt="AWS Budget and Lambda Integration" src="./img/AWS Budget and Lambda Integration.png" width="50%"/>

This stack configures AWS Budget threshold trigger of AWS Lambda through SQS queue.

## Deployment

```sh
export STACK_NAME="AWS-Budget-SQS-Lambda-Demo"

aws cloudformation create-stack \
	--stack-name $STACK_NAME \
	--template-body file://budget-alert-stack.yaml \
	--capabilities CAPABILITY_NAMED_IAM
	
aws cloudformation wait stack-create-complete --stack-name $STACK_NAME
```

## Outputs

### S3 Bucket

```sh
aws cloudformation describe-stacks \
	--stack-name $STACK_NAME \
	--query 'Stacks[0].Outputs[?OutputKey==`TerraformStateBucket`].OutputValue' \
	--output text
```

### DynamoDB Table

```sh
aws cloudformation describe-stacks \
	--stack-name $STACK_NAME \
	--query 'Stacks[0].Outputs[?OutputKey==`TerraformStateDynamoDBTable`].OutputValue' \
	--output text
```

## Decommission

```sh
aws cloudformation delete-stack --stack-name $STACK_NAME

aws cloudformation wait stack-delete-complete --stack-name $STACK_NAME
```


Maintained by [https://hands-on.cloud](https://hands-on.cloud)
