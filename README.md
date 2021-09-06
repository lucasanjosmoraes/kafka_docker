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

## Errors

It's not possible to use Schema-Registry versions lower than `6.x.x` on **macOS with M1 chip**, due to error:
```
qemu: core dumped
```

These devices can't use `6.x.x` versions either, due to the error below:
```
Exception in thread "main" java.lang.ExceptionInInitializerError
at org.eclipse.jetty.http.MimeTypes.<clinit>(MimeTypes.java:175)
at org.eclipse.jetty.server.handler.gzip.GzipHandler.<init>(GzipHandler.java:190)
at io.confluent.rest.ApplicationServer.wrapWithGzipHandler(ApplicationServer.java:468)
at io.confluent.rest.ApplicationServer.wrapWithGzipHandler(ApplicationServer.java:477)
at io.confluent.rest.ApplicationServer.finalizeHandlerCollection(ApplicationServer.java:213)
at io.confluent.rest.ApplicationServer.doStart(ApplicationServer.java:230)
at org.eclipse.jetty.util.component.AbstractLifeCycle.start(AbstractLifeCycle.java:73)
at io.confluent.kafka.schemaregistry.rest.SchemaRegistryMain.main(SchemaRegistryMain.java:43)

Caused by: java.nio.charset.IllegalCharsetNameException: l;charset=iso-8859-1
at java.base/java.nio.charset.Charset.checkName(Charset.java:308)
at java.base/java.nio.charset.Charset.lookup2(Charset.java:482)
at java.base/java.nio.charset.Charset.lookup(Charset.java:462)
at java.base/java.nio.charset.Charset.forName(Charset.java:526)
at org.eclipse.jetty.http.MimeTypes$Type.<init>(MimeTypes.java:107)
at org.eclipse.jetty.http.MimeTypes$Type.<clinit>(MimeTypes.java:67)
```

Therefore, if you're not running these images on these devices, you can uncomment the line below and also serve the Schema-Registry:
```
KSQL_BOOTSTRAP_SERVERS: 'broker:29092'
# KSQL_KSQL_SCHEMA_REGISTRY_URL: http://schema-registry:8081
KSQL_KSQL_LOGGING_PROCESSING_STREAM_AUTO_CREATE: 'true'
```

## References

**Quick Start for Confluent Platform:**
- https://docs.confluent.io/platform/current/quickstart/ce-docker-quickstart.html
- https://github.com/confluentinc/cp-all-in-one/blob/6.2.0-post/cp-all-in-one/docker-compose.yml

**Installing kSQL only:**
- https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/install-ksqldb-with-docker/
- https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/server-config/#setting-ksqldb-server-parameters
- https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/installing/

**Suggested docker-compose file:**
- https://github.com/confluentinc/ksql/blob/master/docker-compose.yml

**More info:**
- https://aweagel.github.io/ksql_workshop/
- https://towardsdatascience.com/enabling-a-powerful-search-capability-building-and-deploying-a-real-time-stream-processing-etl-a27ecb0ab0ae