[![Build Status](https://travis-ci.org/Blackdread/sql-to-jdl.svg?branch=master)](https://travis-ci.org/Blackdread/sql-to-jdl)
[![StackShare](https://img.shields.io/badge/tech-stack-0690fa.svg?style=flat)](https://stackshare.io/Blackdread/sql-to-jdl)

# sql-to-jdl
Tool to translate SQL databases to JDL format of jHipster (Created due to existing databases to be generated with jHipster and build angular-java web)

# Why not use tools like UML provided on jHipster?
- JDL from web is ok for a few entities but not for more than 100 entities and relations
- UML software and xml exporters could have worked (other tools on jHipster) but:
  - already many databases in production to be exported in JDL (faster to generate the JDL from it)
  - already working UML design with MySQL Workbench

# An alternative for REST filter and sort
Different criterias, support for JPA and jOOQ dynamic filtering and sorting

https://github.com/Blackdread/rest-filter

# How to use
Run "mvn compile" at least once to let jOOQ generate some required tables (see [Issue solved](https://github.com/Blackdread/sql-to-jdl/issues/2)).

Set properties file:
- Schema name to export
- Tables names to be ignored
- Path of export file

Particularly:

- In `application.yml` set the following:
```yml
spring:
    datasource:
            type: com.zaxxer.hikari.HikariDataSource
            url: jdbc:mysql://localhost:3306/[PUT DATABASE NAME HERE]?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=UTC
            username: root
            password: [PUT DATABASE PASSWORD HERE]

application:
    database-to-export: <PUT DATABASE NAME HERE>
```

In pom.xml
```xml
<project>
    <properties>
        <database.url>jdbc:mysql://localhost:3306/[PUT DATABASE NAME HERE]?serverTimezone=UTC</database.url>
        <database.user>root</database.user>
        <database.password>[PUT DATABASE PASSWORD HERE]</database.password>
```

# After JDL file is generated
Still have some manual steps to do:
- review relations:
  - ManyToMany
  - Owner side display field
  - Inverse side field name and display field
  - Bidirectional or not
- add values to enums
- review validations of entities

# Use of
- jOOQ
- Spring boot

# Default specific rules
Table is treated as enum if only 2 columns and both are: "id" AND ("code" OR "name")

Table is treated as ManyToMany if only 2 columns and both are foreign keys

# Links
[jHipster JDL](http://www.jhipster.tech/jdl/)
