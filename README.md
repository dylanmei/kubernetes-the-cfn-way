kubernetes-the-cfn-way
----------------------

An AWS CloudFormation template based on a walkthrough of Kelsey Hightower's [kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way).

*Using this is cheating!* But it does get you through some of the boring bits.

## common commands

Validate template

```
% aws cloudformation validate-template --template-body file://$PWD/template.yaml

```

Create stack

```
% aws cloudformation create-stack --stack-name "kubernetes" \
  --template-body file://$PWD/template.yaml \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=KeyName,ParameterValue=my-key-pair

% aws cloudformation wait stack-create-complete --stack-name "kubernetes"

```

Update stack

```
% aws cloudformation update-stack --stack-name "kubernetes" \
  --template-body file://$PWD/template.yaml \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=KeyName,ParameterValue=my-key-pair

% aws cloudformation wait stack-update-complete --stack-name "kubernetes"

```

Print outputs

```
% aws cloudformation describe-stacks --stack-name "kubernetes" --query 'Stacks[].Outputs[].[OutputKey, OutputValue]' --output table

```

A long-winded way of printing EC2 details, such as the public ip addresses:

```
% aws ec2 describe-instances --filters Name=tag-value,Values=$(aws cloudformation describe-stacks --stack-name "kubernetes" --query 'Stacks[0].StackId' --output text) --query 'Reservations[].Instances[].[Tags[?Key==`Name`] | [0].Value, InstanceId, PublicIpAddress]' --output table

```
