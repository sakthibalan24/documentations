# Redis Annotations and Commands in Spring Boot

## 1. Redis Annotation Types

### Spring Cache annotations

These annotations control when application data is cached, retrieved
from the cache, updated, or removed.

### Spring Data Redis mapping annotations

These annotations describe how a Java object is represented and stored
in Redis when using Redis repositories.

## 2. Application Startup

### `@EnableCaching`

Enables annotation-driven caching. Add it to your Spring Boot
configuration class.

## 3. Service-Level Cache Annotations

### `@Cacheable` --- Read or populate the cache

-   **First call:** Cache miss → execute the method → save the result in
    Redis.
-   **Next call:** Cache hit → return the cached result without
    executing the method.

### `@CachePut` --- Update the cache

Always execute the method. When it succeeds, put its returned value into
the cache under the specified key.

### `@CacheEvict` --- Remove cached data

Remove one cache entry or clear all entries in the named cache. It does
not delete data from MySQL by itself.

### `@Caching` --- Group multiple cache operations

Groups multiple cache operations on one method. Example: evict two
caches when an employee is updated.

### `@CacheConfig` --- Share cache configuration

Defines common cache configuration for a class. Example: specify a
default cache name for service methods.

## 4. Example Request Flow

  ---------------------------------------------------------------------------
  Request                     MySQL                   Redis cache
  --------------------------- ----------------------- -----------------------
  `POST /employees`           Inserts employee        Not populated by this
                                                      example

  `GET /employees/101` ---    Reads employee          Stores result
  cache miss                                          

  `GET /employees/101` ---    No query from this      Returns cached result
  cache hit                   method                  

  `PUT /employees/101`        Updates employee        Replaces entry with
                                                      returned object

  `DELETE /employees/101`     Deletes employee        Removes entry

  `DELETE /employees/cache`   No database change      Clears the named cache
  ---------------------------------------------------------------------------

## 5. Spring Data Redis Mapping and Repository Annotations

  -----------------------------------------------------------------------
  Annotation                          Purpose
  ----------------------------------- -----------------------------------
  `@RedisHash`                        Marks a class for Redis repository
                                      persistence and specifies its
                                      keyspace.

  `@Id`                               Identifies the object's ID, used in
                                      the Redis key.

  `@Indexed`                          Creates a secondary index for
                                      querying a field through supported
                                      Redis repository operations.

  `@TimeToLive`                       Configures expiration for an object
                                      in Redis.

  `@GeoIndexed`                       Supports geospatial indexing of a
                                      property, such as for
                                      nearby-location searches.

  `@EnableRedisRepositories`          Enables Redis repository
                                      infrastructure for `CrudRepository`
                                      interfaces configured for Redis.
  -----------------------------------------------------------------------

### Other shared Spring Data mapping annotations

  -----------------------------------------------------------------------
  Annotation                          Purpose
  ----------------------------------- -----------------------------------
  `@Transient`                        Excludes a property from
                                      persistence mapping.

  `@TypeAlias`                        Defines a custom type alias for
                                      stored type information.
  -----------------------------------------------------------------------

### Note about `@Reference`

`@Reference` is not a standard Spring Data Redis mapping annotation.
Redis object references are generally handled differently, for example
by storing IDs.

## 6. Quick Annotation Reference

### Spring Cache annotations

-   `@EnableCaching`
-   `@Cacheable`
-   `@CachePut`
-   `@CacheEvict`
-   `@Caching`
-   `@CacheConfig`

### Spring Data Redis mapping and repository annotations

-   `@RedisHash`
-   `@Id`
-   `@Indexed`
-   `@TimeToLive`
-   `@GeoIndexed`
-   `@EnableRedisRepositories`

### Other shared Spring Data mapping annotations

-   `@Transient`
-   `@TypeAlias`

## 7. `allEntries = true`

`allEntries = true` is an annotation attribute (not a Redis command).
For example, `@CacheEvict(cacheNames = "employees", allEntries = true)`
evicts all entries in the named cache.

## 8. Redis CLI Commands

  Command     Purpose
  ----------- ------------------------------------------------------
  `SCAN`      Iterates through keys matching a pattern.
  `TYPE`      Checks a key's data type.
  `GET`       Reads a string value.
  `HGETALL`   Reads all fields and values in a hash.
  `TTL`       Checks the remaining time to live (expiry) of a key.
