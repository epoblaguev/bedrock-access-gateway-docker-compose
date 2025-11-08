# bedrock-access-gateway-docker-compose
A sample docker-compose file for self-hosting [bedrock-access-gateway](https://github.com/aws-samples/bedrock-access-gateway).

It appears that each service can only target one region, so if you want multiple regions to be available, you must deploy them as separate services.

```yaml
services:

  # Gateway for us-east-1
  east-1: 
    build:
      context: https://github.com/aws-samples/bedrock-access-gateway.git#main:src
      dockerfile: Dockerfile_ecs
    environment:
      - API_KEY=${API_KEY}
      - AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
      - AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
      - AWS_REGION=us-east-1
    ports:
      - "8085:8080"
  
  # Gateway for us-east-2
  east-2: 
    build:
      context: https://github.com/aws-samples/bedrock-access-gateway.git#main:src
      dockerfile: Dockerfile_ecs
    environment:
      - API_KEY=${API_KEY}
      - AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
      - AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
      - AWS_REGION=us-east-2
    ports:
      - "8086:8080"
```
