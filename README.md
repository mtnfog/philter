# Philter

Philter finds, identifies, and removes sensitive information from text. The docker compose file in this repository will launch the Philter containers. For more information on these containers and how to use them visit https://www.mtnfog.com/products/philter/docker/.

## Docker Compose

To launch the Philter containers:

```
curl -O https://raw.githubusercontent.com/mtnfog/philter/master/docker-compose.yml
docker-compose up
```

Once the containers have started you can send a sample filter request:

```
curl http://localhost:8080/api/filter --data "George Washington was president and his ssn was 123-45-6789." -H "Content-type: text/plain"
```

Other example requests are available in the [Philter User’s Guide Quick Start](https://philter.mtnfog.com/introduction/quick-start).

### Configuring Philter

Philter can be configured by setting environment variables. Refer to the [Philter User's Guide](https://philter.mtnfog.com/configuration/settings) for the available settings. Below is an example of configuring Philter to use a Redis cache:

```
version: '3'
services:
  philter:
    depends_on:
      - "redis"
      - "philter-ner"
    environment:
      - PHILTER_CACHE_REDIS_ENABLED=true
      - PHILTER_CACHE_REDIS_HOST=redis
      - PHILTER_CACHE_REDIS_PORT=6379
      - PHILTER_CACHE_REDIS_AUTH_TOKEN=randompassword
      - PHILTER_LICENSE_KEY=
      - PHILTER_NER_ENDPOINT=http://philter-ner:18080/
...
```

## Cloud Images

For turnkey cloud images of Philter on AWS, Azure, or GCP visit https://www.mtnfog.com/products/philter/availability/.

## Getting Help

For assistance please contact support@mtnfog.com.
