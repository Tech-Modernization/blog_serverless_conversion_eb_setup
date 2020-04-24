# Summary
Cloudformation template that creates an pair of Elastic Beanstalk application and environment. The pair is to be used as the deployment target of a codepipeline.

# Features of the environment:
* An ELB fronts an autoscaling group.
* The ELB logs access to an S3 bucket.
* The TargetGroup response time triggers scaling action of the auto scaling group.
* Instance logs are streams to CloudWatch log.

# create the elastic beanstalk application and environment
```
    aws cloudformation deploy --stack-name <stack_name> --template-file elasticBeanStalk_setup.yml \
        --capabilities CAPABILITY_IAM \
        --parameter-overrides \
        SolutionStackName="64bit Amazon Linux 2018.03 v4.14.1 running Node.js" \
        NotificationEmail=<youremail@yourcom.com> \
        EC2KeyName=<ec2_sshkeypair_name>
```

# get the applications ID and the environment ID. They will be used as inputs for the creation of the codepipeline.
```
aws cloudformation describe-stacks --stack-name <stack_name> | jq ".Stacks[0].Outputs[]"
```
