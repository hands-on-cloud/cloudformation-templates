# Useful Hands-On.Cloud CloudFormation Templates - Cloud9 IDE Setup

## Deployment

```sh
aws cloudformation create-stack \
	--stack-name MyCloud9Stack \
	--template-body file://cloud9-environment.yaml \
	--parameters \
		ParameterKey=InstanceType,ParameterValue=t2.micro \
		ParameterKey=SubnetId,ParameterValue=subnet-xxxxxx \
	--capabilities CAPABILITY_NAMED_IAM
	
aws cloudformation wait stack-create-complete --stack-name MyCloud9Stack
```

## Cloud9 IDE URL

```sh
aws cloudformation describe-stacks \
	--stack-name MyCloud9Stack \
	--query 'Stacks[0].Outputs[?OutputKey==`Cloud9URL`].OutputValue' \
	--output text
```

## Decommission

```sh
aws cloudformation delete-stack --stack-name MyCloud9Stack

aws cloudformation wait stack-delete-complete --stack-name MyCloud9Stack
```


Maintained by [https://hands-on.cloud](https://hands-on.cloud)
