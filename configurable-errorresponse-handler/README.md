[Back to restclient-ext](https://github.com/microprofile-extensions/restclient-ext/blob/master/README.md)

# Configurable Error Response Handler

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.microprofile-ext.jaxrs-ext/configurable-exception-handler/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.microprofile-ext.jaxrs-ext/configurable-exception-handler)
[![Javadocs](https://www.javadoc.io/badge/org.microprofile-ext.jaxrs-ext/configurable-exception-handler.svg)](https://www.javadoc.io/doc/org.microprofile-ext.jaxrs-ext/configurable-exception-handler)

This Handler can be configured to handle certain HTTP response codes and map them to a Java Exception. It will get the exception message from the reason header.

## Adding Configurable Error Response Handler

In ```pom.xml```:
    
```xml

    <dependency>
        <groupId>org.microprofile-ext.restclient-ext</groupId>
        <artifactId>configurable-errorresponse-handler</artifactId>
        <version>XXXXX</version>
    </dependency>

```

In your Microprofile ```rest client```

```java

    @RegisterProvider(RuntimeResponseExceptionMapper.class)

```

Example:

```java

    @RequestScoped
    @RegisterRestClient
    @Consumes(MediaType.APPLICATION_JSON) @Produces(MediaType.APPLICATION_JSON)
    @RegisterProvider(RuntimeResponseExceptionMapper.class)
    @Path("/api")
    public interface MembershipProxy {

        @GET @Path("/{id}") @Operation(hidden = true)
        public Membership getMembership(@NotNull @PathParam(value = "id") int id);
     }

```

## Default mappings

Here some default mappings. You can add more mappings in your own config, or override these with your own config.(See https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

- **401 Unauthorized (RFC 7235)** 
  - ```401/mp-restclient-ext/exception=javax.ws.rs.NotAuthorizedException```

## Adding your own mappings

In your config (MicroProfile Config API) add your own mapping (examples above)


*HTTP_Status_code*/mp-restclient-ext/exception = *Java_Exception_Name*
