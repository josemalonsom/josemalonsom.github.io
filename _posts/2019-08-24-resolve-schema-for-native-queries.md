---
title: "How to resolve the schema name when using Spring Data JPA native queries"
date: 2019-08-24
categories:
  - spring
  - jpa
tags:
  - spring
  - jpa
---

When using native queries with Hibernate and need to reference a database table which is in a different schema as the default one, you can use the `{h-schema}` Hibernate's placeholder.

For example if we have a table "users" which is in the "management" schema we can reference it using `{h-schema}users`, Hibernate will replace it by the schema specified in the configuration property `hibernate.default_schema`.

```java
public interface UserRepository extends JpaRepository<User, Long> {

  @Query(value = "SELECT * FROM {h-schema}users WHERE email_address = ?1", nativeQuery = true)
  User findByEmailAddress(String emailAddress);
}
```

In the example above the value `{h-schema}users` will be replaced by `management.users` when the query is executed. Notice that Hibernate adds the dot automatically.

For more information about the available placeholders which can be used in native queries see [Resolving global catalog and schema in native SQL queries][hibernate-doc].

[hibernate-doc]: https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#sql-global-catalog-schema
