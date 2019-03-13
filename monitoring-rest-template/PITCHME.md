

## Monitoring Rest Template
#### Using Spring 'properly'

  
  @snap[south-east]
  Harry Martland  
  Senior Software Engineer  
  **@color[darkblue](Booking)@color[deepskyblue](Go)**
  @snapend

---?image=images/ot-sp-p-logos.png&size=contain

Note:
- writing as little as possible so it is easy for teams
- use Prometheus as it is our default monitoring provider
- convention over configuration (often forgotten)

---

#### How to?

```groovy
compile 'io.micrometer:micrometer-registry-prometheus'
compile 'org.springframework.cloud:spring-cloud-starter-zipkin'
```

Note:
- some config needed to get prometheus exposed 
- need to enable scraping of prometheus and tracing sidecar in bgcloud config

---
#### How Not to Use RestTemplate

```java
return new RestTemplate().getForObject(
        baseUrl + "/postcodes/" + postcode, 
        PostCodeResponse.class);
```


Note:
- creating a new one
- not setting base URL
- concatenating query parameters

---
#### Autowiring RestTemplateBuilder

```java
return restTemplateBuilder
    .rootUri(p.getUrl())
    .setConnectTimeout(p.getConnectTimeout())
    .setReadTimeout(p.getReadTimeout())
    .build();
    
```

```java
return restTemplate.getForObject(
    "/postcodes/{postcode}", 
    PostCodeResponse.class, 
    postcode);
```

Note:
- not full code. Create a bean and return a request examples
- each method returns a new builder so no cross contamination
- use path variables
- Set timeouts
- Use a connection pool (just include Apache http)
- use a separate RestTemplate for each API
- spring can add listeners for instrumentation

---?image=images/monitoring/test-rest-template.png&size=contain

## Testing

Note:
- don't need to test base URL in repository
- Use Wire mock!

---?image=images/monitoring/rest-template-prometheus.png&size=contain

## Prometheus Metrics


Note:
- as long as you use the advice above everything should work smoothly
- if you don't you won't get metrics or there will be a metric for each query argument
- request count, total time (can calculate average), max time, error statistics

---?image=images/jaeger-screenshot.png&size=contain

## Open Tracing


Note:
- include dependence
- as long as you use the advice above everything should work smoothly
- with spring defaults to 10% traffic
- can set header to force sampling

---?image=images/monitoring/connection-pool.png&size=contain

## Monitoring Connection Pools