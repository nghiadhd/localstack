# Launch AWS SQS

1. Build docker image

```bash
commitId=`git rev-parse HEAD | cut -c 1-10`

docker build -t localstack:$commitId -t localstack:sqs --label "commit.id=$commitId" --label "built.at=$(date -u)" .
```

2. Start SQS

```bash
docker-compose -f aws-sqs-docker-compose.yml up -d
docker-compose -f aws-sqs-docker-compose.yml down
```

3. Control with AWS CLI

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
