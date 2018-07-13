## Deploy Pilot Light scenario on AWS
When an instance in one region goes down, this deployment will automatically start an instance in another region using Route 53 health checks, SNS and Lambda.

![greenshot 2018-07-06 15 10 54](https://user-images.githubusercontent.com/23042063/42403841-0408b49a-8139-11e8-8434-c13dac0b633f.png)

### Steps:
1. Deploy CF templates in pilot-light-east in US-EAST-1 (N. Virginia) region in order. Pass parameters into each stack creation.
2. Deploy CF templates in pilot-light-west in US-WEST-2 (Oregon) region in order. Pass parameters into each stack creation.
4. Deploy CF template for Route 53 failover configuration. 
    a. Update health check alarm with SNS topic created from pilot-light-east CF template.

### Roadmap:
- Include notification in Route 53 health check

