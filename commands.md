# Create Stacks 

## US-EAST-1
1. aws cloudformation deploy --template-file DR-East/1-sg-east.yaml --stack-name pl-sg-east --region us-east-1
2. aws cloudformation deploy --template-file DR-East/2-eip-east.yaml --stack-name pl-eip-east --parameter-overrides WebSubnet=subnet-3b5e1d63 WebServerSecurityGroup=sg-0f3f48c22f6179ac0 --region us-east-1
3. aws cloudformation deploy --template-file DR-East/3-ec2-east.yaml --stack-name pl-ec2-east --parameter-overrides NetworkInterface=eni-0ed08d51c8c491530 --region us-east-1
4. aws cloudformation deploy --template-file DR-East/4-s3-east.yaml --stack-name pl-s3-east --region us-east-1
5. aws cloudformation deploy --template-file DR-East/5-lambda-east.yaml --stack-name pl-lambda-east --parameter-overrides Email=greengocloud@gmail.com S3Bucket=pl-s3-east-s3bucket-5db79x4f1dml ZipFile=start-instance.py.zip --capabilities CAPABILITY_IAM --region us-east-1



## US-WEST-2 
1. aws cloudformation deploy --template-file DR-West/1-sg-west.yaml --stack-name pl-sg-west
2. aws cloudformation deploy --template-file DR-West/2-eip-west.yaml --stack-name pl-eip-west --parameter-overrides WebSubnet=subnet-1e9d6f68 WebServerSecurityGroup=sg-0744882d9bc31836e
3. aws cloudformation deploy --template-file DR-West/3-ec2-west.yaml --stack-name pl-ec2-west --parameter-overrides NetworkInterface=eni-0c4ed5ac7f7f0eb8f
4. aws cloudformation deploy --template-file DR-West/4-route53.yaml --stack-name pl-r53-west --parameter-overrides PrimaryRecord=35.163.21.122 SecondaryRecord=52.4.211.157 DomainName=aws.greengotech.net HostedZoneId=ZDJFTU500WUQU AlarmSNSTopicArn=arn:aws:sns:us-east-1:987092829714:dr-topic

# Failover
1. aws ec2 describe-instances
2. aws ec2 stop-instances --instance-ids i-0ac00cafc492b1730


# Delete Stacks

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