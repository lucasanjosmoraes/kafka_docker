# Kafka with Docker

Project that contains docker-compose files which create containers that:
- Serve Kafka with Zookeeper
- Contain command-line tools to interact with the broker
- Serve KSQL

It's based on [Billy Dharmawan's](https://billydharmawan.medium.com) Medium article which can be found [here](https://betterprogramming.pub/your-local-event-driven-environment-using-dockerised-kafka-cluster-6e84af09cd95).

## Usage

You don't need any extra configuration to run these Docker images, but if you're using a **macOS with M1 chip**, you will need to configure some components:

- On zookeeper service, you will need to link some directories.
```
volumes:
      - ./volumes/zookeeper/log/version-2/:/var/lib/zookeeper/log/version-2
      - ./volumes/zookeeper/data/version-2/:/var/lib/zookeeper/data/version-2
```
