
@snap[midpoint]
## Monitoring Rest Template
#### Using Spring 'properly'
@snapend

  
  @snap[south-east]
  Harry Martland  
  Senior Software Engineer  
  **@color[darkblue](Booking)@color[deepskyblue](Go)**
  @snapend

---

@snap[west]
![Kubernetes Logo](images/spring-boot-logo.png)
@snapend
@snap[east]
![Docker Logo](images/prometheus-logo.png)
@snapend

Note:
- writing as little as possible so it is easy for teams
- use Prometheus as it is our default monitoring provider
- convention over configuration (often forgotten)

---
#### How Not to Use RestTemplate

@snap[midpoint]
```java
return new RestTemplate().getForObject(
        baseUrl + "/postcodes/" + postcode, 
        PostCodeResponse.class);
```
@snapend

Note:
- creating a new one
- not setting base URL
- concatenating query parameters

---
#### Autowiring RestTemplateBuilder

@snap[midpoint]
```java
return restTemplateBuilder
    .rootUri(p.getUrl())
    .setConnectTimeout(p.getConnectTimeout())
    .setReadTimeout(p.getReadTimeout())
    .build();
    
return restTemplate.getForObject(
    "/postcodes/{postcode}", 
    PostCodeResponse.class, 
    postcode);
```
@snapend

Note:
- not full code. Create a bean and return a request examples
- each method returns a new builder so no cross contamination
- use path variables
- Set timeouts
- Use a connection pool (just include Apache http)
- use a separate RestTemplate for each API
- spring can add listeners for instrumentation

---

## Testing

@snap[midpoint]
```java
@Test
public void shouldMakeRequest() {
    when(restTemplate.getForObject("/postcodes/{postcode}", PostCodeResponse.class, "AT3ST"))
        .thenReturn(mockResponse);
    
    PostCodeResponse result = postCodeController.getPostCode("AT3ST");
    verify(restTemplate).getForObject("/postcodes/{postcode}", PostCodeResponse.class, "AT3ST");
    assertEquals(mockResponse, result);
}
```
@snapend

Note:
- don't need to test base URL in repository
- Use Wire mock!

---

## Prometheus Metrics

Note:
- as long as you use the advice above everything should work smoothly
- if you don't you won't get metrics or there will be a metric for each query argument

---

## Open Tracing

Note:
- include dependence
- as long as you use the advice above everything should work smoothly

---

## Monitoring Connection Pools