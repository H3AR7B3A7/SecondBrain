# Spring Data Mongo
[[Spring]] Data also offers support for Mongo.

## Dependencies
Starter Data Mongo:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```
Embedded database:
```xml
<dependency>
    <groupId>de.flapdoodle.embed</groupId>
    <artifactId>de.flapdoodle.embed.mongo</artifactId>
</dependency>
```

## MongoDB Concepts
*Mongo BSON (= Binary JSON):*

- Database
- Collections (<> Tables)
- Documents (<> Rows)
- Fields (<> Columns)
- Id (<> Primary Key)

## Annotations
- @Document
- @Id
- @Field
- @Transient - Not persisted
- @Indexed - To speed up lookups
- @TextIndexed
- @CompoundIndex
- @DbRef - To join tables

## Properties

- Mongo server IP
- Mongo server port
- Database name
- Credentials

## Query Execution

- Without indexes
  - Collection scan, each document is evaluated
  - Slow searches
  - Fast inserts & updates
- With indexes
  - Does not scan every document in collection
  - Fast searches
  - Slow inserts & updates

## Filter Operators

- is / ne (is, not equals)
- lt / lte (less than, less tha, equals)
- gt / gte (greater than, greater than equals)
- in (value in list)
- exists (has value)
- regex (fits pattern)

## Insert Process

Persisting a Document
- Create collection if it doesn't exist
- Generate ID if not present
- Save single document atomically

**Single Document transactions**:

*An operation on a single document is atomic. Because relationships are embedded in a single document,
this mostly eliminates the need for multi-document transactions.*

**Multi-Document transactions**:

*For situations that require atomicity to multiple documents (in single or multiple collections),
Mongo 4+ supports multi document transactions. However, we should avoid this where possible.*

- Insert has batch operation support. (e.g.: insertAll(List<>))

## Save / Update

*Save can also insert, but we should use it only to update.*

Save:
- Save completely overwrites the original document if the id already exists, never just one field.
- Save does **not** have batch operation support.

Update:
- Update only affects the fields defined in the update definition, not the whole document.
- Update has batch operation support.

## Delete

Deleting documents:
- Single
- Multi
- All

## Mongo Converter

*Is a feature used for mapping all Java types to/from DBObjects when storing or retrieving these objects.*

Custom converter:
- Create write converter
- Create read converter
- Register converters as a Spring bean

## String
Mongo prefers strings as data ype, so we change our id from Long to String.

## LocalDateTime
Mongodb removed the nanosecond information from Date type and has a precision of milliseconds.

We can truncate LocalDateTime in Java:

```java
Clock millisecondClock = Clock.tick(Clock.systemDefaultZone(), Duration.ofNanos(1000000)); 
LocalDateTime d = LocalDateTime.now(millisecondClock);
```

## MongoRepository Interface
- Interface: Repository
- Interface: CrudRepository
- Interface: PagingAndSortingRepository
- Interface: MongoRepository
- Interface: MyCustomRepository (Our own abstraction using IoC)

## @Query
Example:
```java
@Query("{'aircraft.nbSeats' : {$gte: ?0}}")
List<FlightInformation> findByMinAircraftNbSeats(int i);
```

## Mongo Document References
In mongo, denormalized data in a single document is optimal.
We should always try to minimize relationships between documents.

Relating documents:
- Manual: Saving the '_id' of a document in another document
- DBRefs: Link documents together by using the '_id' field, collection name and database name
  - Can link documents across collections or different databases
  - To resolve DBRefs, the application must perform additional queries
  - Cascading is not supported

DBRef formats:
- $ref
- $id
- $db

Example:
```json
{
  "_id": ObjectId("37291b08-9591-4db7-912a-c7ed37cc7ed3"),
  "name": "SomeName",
  "cap": 666,
  "engine": {
    "$ref": "engines",
    "$id": ObjectId("73535742-5097-4a14-ac93-c4a623c5d395"),
    "$db": "atm"   // Optional
  }
}
```
*The order of the formats matters!!! DBRefs are not 'smart'.*

Implementation:
```java
@Document
public class Aircraft {
    @Id
    private String id;
    private String name;
    private Integer cap;
    @DBRef
    private Engine engine;
}
```

## Mongo Lifecycle Events
- onBeforeConvert
- onBeforeSave
- onBeforeDelete
- onAfterConvert
- onAfterSave
- onAfterLoad
- onAfterDelete

Behavior:
- Lifecycle events are emitted only for root level types.
  Sub-documents are not subject to event publication unless they are annotated with @DBRef
- It is all happening in an async fashion. We have no guarantees to when an event is processed

Use-cases:
- Implementing cascade on save
- Trigger some job/action in different systems
- Security audits

Implementation:

- *Create a bean that **Extends** AbstractMongoEventListener and **Overrides** the methods.*
- *Create an event listener per feature. (Cascading/Auditing/...)*

## Hierarchy of Preference for References
1. No relationships - NoSQL philosophy
2. Use @DBRef, but only if we implement cascade on save, and we don't have bidirectional references
    - Population of related documents done by the framework
    - Cascading
3. Manual references

## Migrations
*Data changes over time.*

Mongo Documents vs Java Objects:
- A change in a Mongo Document will impact serialization / deserialization process
- A change in Mongo Document will impact the queries
- Changes to collections will also impact queries

Implementation options:
- Manual migrations using scripts (to be avoided at all cost)
- Create migration component ourselves
    - Needs
      - Version detection (& automatic upgrade)
      - Simple configuration
      - Logging
    - Pro
      - Complete control
      - Can meet every aspect of our needs
    - Con
      - Requires more time to develop
      - Is not trivial to create
- Use an existing migration framework
    - Pro
        - Saves time
        - Increased focus on the application domain
    - Con
        - The data migration process is not fully under our control
        - Some applications need more features than frameworks offer


### Mongobee
Dependency:
```xml
<dependency>
  <groupId>com.github.mongobee</groupId>
  <artifactId>mongobee</artifactId>
</dependency>
```
Configure bean:
```java
@Bean
public Mongobee mongobee() {
    Mongobee runner = new Mongobee(mongoUri);
    runner.setEnabled(true);
    runner.setChangeLogsScanPackage("yourdomain.*");
    runner.setMongoTemplate(this.mongoTemplate);
    return runner;
}
```
Changelog:
```java
@ChangeLog(order = "001")
public class DBChangeLog001 {
    @ChangeSet(order = "001", id = "seedCrew", author = "Steven")
    public void seedCrewMembers(MongoTemplate mongoTemplate) {
        // ...
    }
}
```

We can go [here](https://github.com/mongobee/mongobee) for more information and examples.

### Other Options
- Liquibase MongoDB Extension
    - [Example project](https://github.com/alexandru-slobodcicov/liquibase-nosql-quickstart)
- Mongock
    - [Example project](https://github.com/cloudyrock/mongock-integration-tests/tree/master/mongock-spring-v5/mongock-spring5-springdata3-it)


---
#Spring