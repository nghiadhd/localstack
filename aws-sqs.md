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
