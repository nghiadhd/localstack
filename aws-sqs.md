# Launch AWS SQS

1. Start SQS

```bash
docker-compose -f aws-sqs-docker-compose.yml up -d
docker-compose -f aws-sqs-docker-compose.yml down
```

2. Control with AWS CLI

- See cli help

```bash
docker run --rm mesosphere/aws-cli help
```

- Create new queue

```bash
docker run --rm \
  -e "AWS_DEFAULT_REGION=us-east-1" \
  -e "AWS_ACCESS_KEY_ID=ignored" \
  -e "AWS_SECRET_ACCESS_KEY=ignored" \
  -e "AWS_DEFAULT_OUTPUT=json" \
  --network="bridge" --add-host="localstack:172.17.0.1" \
  mesosphere/aws-cli --endpoint-url=http://localstack:4576/ sqs create-queue --queue-name duy-test
```

- List queues

```bash
docker run --rm \
  -e "AWS_DEFAULT_REGION=us-east-1" \
  -e "AWS_ACCESS_KEY_ID=ignored" \
  -e "AWS_SECRET_ACCESS_KEY=ignored" \
  -e "AWS_DEFAULT_OUTPUT=json" \
  --network="bridge" --add-host="localstack:172.17.0.1" \
  mesosphere/aws-cli --endpoint-url=http://localstack:4576/ sqs list-queues
```
