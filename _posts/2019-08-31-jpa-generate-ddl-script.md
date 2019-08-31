---
title: "Instruct the persistence provider to generate the DDL scripts using JPA 2.2 properties"
date: 2019-08-31
categories:
  - java
  - jpa
  - sprint
tags:
  - java
  - jpa
  - spring
---

When using JPA 2.2 it is possible to instruct the persistence provider to generate the DDL scripts for drop/create the database schema using the next properties:

- **javax.persistence.schema-generation.create-source**: allows to specify the source for the schema generation, it can be the ORM mapping metadata, a DDL script or a combination of both. Possible values are: *metadata, script, metadata-then-script, script-then-metadata*.
- **javax.persistence.schema-generation.scripts.action**: specifies which scripts must be generated. Possible values are: *none, create, drop-and-create, drop*.
- **javax.persistence.schema-generation.scripts.drop-target**: name of the file for the drop script.
- **javax.persistence.schema-generation.scripts.create-target**: name of the file for the create script.

If we are using *Spring Boot* we can prefix this properties with *"spring.jpa.properties"*, for example *"spring.jpa.properties.javax.persistence.schema-generation.create-source"*, as the
prefix is going to be stripped out and the properties are going to be passed as normal JPA properties (see [Configure JPA properties][spring-boot-jpa-properties])

This is an example of how to configure our *Spring Boot* application to generate the DDL scripts for drop and create the schema using an *application.yml* file:

```yml
spring:
  jpa:
    properties:
      javax:
        persistence:
          schema-generation:
            create-source: metadata
            scripts:
              action: drop-and-create
              drop-target: drop.sql
              create-target: create.sql
```

in this example the drop script will be generated in the file *drop.sql* and the create script in *create.sql*.

There is a working example [here][github-example].

For more information about these properties you can check the [JSR 338: JavaTM Persistence 2.2][jpa2-specification] specification.

[spring-boot-jpa-properties]: https://docs.spring.io/spring-boot/docs/2.1.7.RELEASE/reference/html/howto-data-access.html#howto-configure-jpa-properties
[github-example]: https://github.com/josemalonsom/blog-examples/tree/master/java/jpa/jpa-generate-ddl-script
[jpa2-specification]: https://jcp.org/en/jsr/detail?id=338
