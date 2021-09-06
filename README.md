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

## Errors

Isn't possible to use schema-registry versions lower than `6.x.x` on **macOS with M1 chip**, due to error:
```
qemu: core dumped
```

But if we use `6.x.x` versions, we will get the error below:
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
