# quarkus-micrometer-bug Project

# Issue
Disabling micrometer metrics causes NullPointerException when RestClient is created 
(either via @RestClient or RestClientBuilder)


## Generated with
Simple Quarkus project generated with Quarkus 2.8.1.Final and extensions:

* quarkus-resteasy (classic)
* quarkus-resteasy-jsonb
* quarkus-rest-client-jsonb
* quarkus-micrometer-registry-prometheus

## Changes made to sample code

1. application.properties - disabled micrometer
2. Added Rest client interface with empty get method
3. In Server rest resource, inject rest client

## Observed behaviour
```
Caused by: java.lang.NullPointerException
    at io.quarkus.micrometer.runtime.binder.RestClientMetricsListener.prepClientMetrics(RestClientMetricsListener.java:50)
    at io.quarkus.micrometer.runtime.binder.RestClientMetricsListener.onNewClient(RestClientMetricsListener.java:38)
    at io.quarkus.restclient.runtime.QuarkusRestClientBuilder.lambda$build$0(QuarkusRestClientBuilder.java:236)
    at java.base/java.util.ArrayList.forEach(ArrayList.java:1541)
    at io.quarkus.restclient.runtime.QuarkusRestClientBuilder.build(QuarkusRestClientBuilder.java:236)
    at io.quarkus.restclient.runtime.RestClientBase.create(RestClientBase.java:72)
```
