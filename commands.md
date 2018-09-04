
## US-EAST-1
1. aws cloudformation deploy --template-file DR-East/1-sg-east.yaml --stack-name pl-sg-east --region us-east-1
2. aws cloudformation deploy --template-file DR-East/2-eip-east.yaml --stack-name pl-eip-east --parameter-overrides WebSubnet=<ENTER SUBNET ID> WebServerSecurityGroup=<ENTER SECURITYGROUP ID> --region us-east-1
3. aws cloudformation deploy --template-file DR-East/3-ec2-east.yaml --stack-name pl-ec2-east --parameter-overrides NetworkInterface=<ENTER ENI ID>
4. aws cloudformation deploy --template-file DR-East/4-s3-east.yaml --stack-name pl-s3-east --region us-east-1


## US-WEST-2 
1. aws cloudformation deploy --template-file DR-West/1-sg-west.yaml --stack-name pl-sg-west
2. aws cloudformation deploy --template-file DR-West/2-eip-west.yaml --stack-name pl-eip-west --parameter-overrides WebSubnet=<ENTER SUBNET ID> WebServerSecurityGroup=<ENTER SECURITYGROUP ID>
3. aws cloudformation deploy --template-file DR-West/3-ec2-west.yaml --stack-name pl-ec2-west --parameter-overrides NetworkInterface=<ENTER ENI ID>


# Deleting Stacks

- Note: Remove zip file from S3 bucket before deleting stack.
    - Example: *aws s3 rm s3://pl-s3-s3bucket-1oazy52gscksv/start-instance.py.zip*

## US-EAST-1
1. 
2. aws cloudformation delete-stack --stack-name pl-ec2-west
3. aws cloudformation delete-stack --stack-name pl-eip-west
4. aws cloudformation delete-stack --stack-name pl-sg-west
   
## US-WEST-2 
1. aws cloudformation delete-stack --stack-name pl-ec2-west
2. aws cloudformation delete-stack --stack-name pl-eip-west
3. aws cloudformation delete-stack --stack-name pl-sg-west