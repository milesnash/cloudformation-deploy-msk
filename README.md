## Deploying an MSK (Amazon Managed Streaming for Apache Kafka) cluster to AWS using SAM (AWS Serverless Application Model)

The CloudFormation (CF) template was based on a combination of:
* the CF ["Get Started With Amazon MSK"](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-msk-cluster.html#aws-resource-msk-cluster--examples) template
* the MSK ["Getting Started"](https://docs.aws.amazon.com/msk/latest/developerguide/getting-started.html) instructions
* a CloudFormer-generated template built using the resources created during completion of the "Getting Started" instructions

The main changes from the "Get Started With Amazon MSK" template are:
* Add serverless transform for SAM
* the instance provisioning has been paired back to the bare minimum to keep costs down
* the AMI can be passed in and defaults to one in eu-west-2 (London ting)
* Tags and names are prepended with the stack name
* The bash script for the client instance has been simplified (no python shenanigans)

## Prerequisites

* [SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)

## Getting Started

1. Deploy the stack (you will need to provide the name of an existing EC2 key pair here)
```bash
  sam deploy --capabilities CAPABILITY_NAMED_IAM CAPABILITY_IAM --guided
```

2. ssh into the client instance once it is ready
```bash
  ssh -i <EC2_KEY> <CLIENT_HOSTNAME>
```

3. Configure the aws cli (See [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html#cli-quick-configuration) for more about this)
```bash
  aws configure
```

From here, you should be able to follow the instructions from point 8 of the Getting Started [Create a topic](https://docs.aws.amazon.com/msk/latest/developerguide/create-topic.html) step onwards to start producing and consuming messages! Note that kafka will reside in `~/kafka/kafka_2.12-2.2.1/`.
