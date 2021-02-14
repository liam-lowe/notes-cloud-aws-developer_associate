# ElastiCache

## Summary

Amazon Elasticache is an AWS managed caching database service. Provides a similar offering to AWS RDS, but for in-memory databases instead of relational databases.

Provides the following in memory database offerings:

- Redis
- Memcached

In-memory databases are caches with really high performance and lower latency compared to traditional relational databases. They are used to take load off of databases for read-intensive workloads. They can help to make your application stateless.

AWS Elasticache is an AWS managed implementation of these databases which handles:

- OS Maintenance
- Patching
- Optimizations
- Setup
- Configuration
- Monitoring
- Failure recovery
- Backups

## Features

### Feature - Database Offerings

On top of standard differences between the two services, Elasticache provides the following differences.

#### Feature - Database Offerings - Redis

Elasticache Redis also provides:

- Multi AZ with auto-failover
- Read replicas to scale reads and have high availability
- Data durability using AOF persistence
- Backup and restore features

#### Feature - Database Offerings - Memcached

Elasticache Memcached also provides:

- Multi-node for partitioning of data (sharding)
- Non-persistent
- No backup and restore
- Multi-threaded architecture

## Security

## Use Case

### Use Case - DB Cache

AWS Elasticache can be used as a DB Cache:

1. Application queries Elasticache for some data
2. If data is present in Elasticache it is returned
3. If data is not present, the service application requires the DB

This helps to relieve load off of RDS.
The cache must have an invalidation strategy to ensure only the most current data is used there.

### Use Case - User Session Store

Elasticache is used to maintain a user session.

1. User logs into any application
2. The application writes session data to Elasticache
3. The user hits another instance of the application
4. The application hits Elasticache, retrieves the session data and the user remains logged in

### Use Case - Caching Implementation

#### Use Case - Caching Implementation - Lazy Loading

Also called Lazy Loading / Cache-Aside / Lazy Population.

In lazy loading:

- Requested data is cached after initial request. Only requested data is cached, the cache isn't filled with unused data
- Node failures are not fatal, just increased latancy to warm the cache
- Cache misses result in 3 round trips, noticeable delay for that request
- There can be stale data in the cache. Data could be updated in DB, but not in cache

#### Use Case - Caching Implementation - Write Through

In write through caching:

- The cache is written when the database is updated.
- Data in the cache is never stale
- Reads are quick - just read the cache
- Writes are slower - write to DB and to cache
- Missing data until it is all added / updated in DB (update lazy loading as well)
- Alot of the data will never be read

#### Use Case - Cache Evictions / Time To Live (TTL)

Cache eviction can occur in 3 ways:

- You delete the item explicitly in the cache
- Item is evicted because the memory is full and it's not recently used (LRU)
- You set an item time-to-live (TTL)

TTL are helpful for many types of data:

- Leaderboards
- Comments
- Activity Streams

TTL duration can range from a few seconds to hours or days
If too many evictions happen due to memory, you should scale!

## Cost
