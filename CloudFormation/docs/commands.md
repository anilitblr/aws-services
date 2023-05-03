### Install and configure aws cli

ref: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

### Test aws cli
```
aws iam get-user
```

### Create a stack using CloudFormation template
```
aws cloudformation create-stack --stack-name chatgpt-demo-stack --template-body file://CloudFormation/template.yaml
```

### Delete stack
```
aws cloudformation delete-stack --stack-name chatgpt-demo-stack
```
### Use the describe-key-pairs command as follows to get the ID of the key pair.
```

aws ec2 describe-key-pairs --filters Name=key-name,Values=chatgpt-demo --query KeyPairs[*].KeyPairId --output text
```
- Output example: `key-05abb699beEXAMPLE`

### Use the get-parameter command as follows to get the parameter for your key and save the key material in a .pem file.
```
aws ssm get-parameter --name /ec2/keypair/key-06af74568eb7b6517 --with-decryption --query Parameter.Value --output text > ~/.ssh/chatgpt-demo.pem
```

### Change permission for .pem file
```
chmod 600 ~/.ssh/chatgpt-demo.pem
```

### SSH into EC2 Instance
```
ssh -i ~/.ssh/chatgpt-demo.pem ubuntu@<IP-Address>
```
