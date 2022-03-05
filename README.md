# Kafka with Docker

Project with a docker-compose file that contains images that allows us to:
- Serve Kafka with Zookeeper
- Serve Schema-Registry
- Serve KSQL and connect to it using CLI

## Usage

You don't need any extra configuration to run these Docker images, but if you're using a **macOS with M1 chip**, you will
need to configure some components. **On zookeeper service**, you will need to link some directories:
```
volumes:
      - ./volumes/zookeeper/log/version-2/:/var/lib/zookeeper/log/version-2
      - ./volumes/zookeeper/data/version-2/:/var/lib/zookeeper/data/version-2
```

## References

**Errors running `6.x.x` images on macOS with M1 chip**
- https://github.com/confluentinc/common-docker/issues/117

**Quick Start for Confluent Platform:**
- https://docs.confluent.io/platform/current/quickstart/ce-docker-quickstart.html
- https://github.com/confluentinc/cp-all-in-one/blob/6.2.0-post/cp-all-in-one/docker-compose.yml

**Running Kafka without Zookeeper 🚀🚀🚀**
- https://github.com/confluentinc/cp-all-in-one/blob/7.0.1-post/cp-all-in-one-kraft/docker-compose.yml

**Installing kSQL only:**
- https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/install-ksqldb-with-docker/
- https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/server-config/#setting-ksqldb-server-parameters
- https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/installing/

**Suggested docker-compose file:**
- https://github.com/confluentinc/ksql/blob/master/docker-compose.yml

**More info:**
- https://aweagel.github.io/ksql_workshop/
- https://towardsdatascience.com/enabling-a-powerful-search-capability-building-and-deploying-a-real-time-stream-processing-etl-a27ecb0ab0ae