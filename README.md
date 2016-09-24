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
