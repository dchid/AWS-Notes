# Elasticache

- Create caching for RDS using Elasticache
- Require invalidation strategy
- Can store user session to make application stateless

## Engines
- Supports Redis and Memchached

|                    | Redis                                 | Memcached                              |
|--------------------|---------------------------------------|----------------------------------------|
| Nodes              | Multi AZ                              | Multi Node for partitioning (sharding) |
| Availability       | Read Replicas                         | No Replication                         |
| Persistence        | Data Durability using AOF Persistence | None                                   |
| Backup and Restore | Yes                                   | No                                     |
| Notes              | Supports Sets and Sorted Sets         | Supports Multithreading                |

## Redis Cluster Modes
- Cluster Mode Disabled
    - One primary node and 5 replicas
    - Asynchronous replication
    - Primary node for read/write while others are read only
    - Multi AZ enabled by default
    - Horizontal scaling up to 5 replicas
    - Vertical scaling will have automatic replications and DNS updates
- Cluster Mode Enabled
    - Data partitioned across multiple shards to scale writes
    - Multi AZ compatible
    - Up to 500 nodes per cluster
    - Supports online horizontal scaling to minimize downtime and offline horizontal scaling for stability
    - Vertical scaling is online only
- Redis supports autoscaling
- To connect to clusters use connection endpoints
- Cluster mode enabled used three endpoints
    - `Primary Endpoint` for writes
    - `Reader Endpoint` for evenly split read opperations
    - `Node Endpoint` for Reads 
- Cluster mode enabled used two endpoints
    - `Configuration Endpoint` for all reads and writes
    - `Node Endpoint` for reads

## Memcashed Scaling
- Can have 1-40 Nodes
- Vertical scaling must be handled manually by
    - Creating a new cluster
    - Changing and endpoint to point to the new cluster
    - Deleting the old cluster
- Memcached has *Auto Discovery* to ease horizontal scaling

## Monitoring
- There are several metrics for both Redis and Memcached
    - `Evictions`: number of non expired items that the cache evicted to allow space for new writes
    - `CPUUtilization`: used for scaling
    - `SwapUsage`: should not exceed 50 MB
    - `CurrConnections`
- There are several metrics for Redis and only
    - `DatabaseMemoryUsagePercentage`
    - `NetorkBytesIn/Out` and `NetworkPacketsIn/Our`
    - `ReplicationBytes`
    - `ReplicationLag`
There is one metric unique to Memcached called `FreeableMemory` which is the amount of free memory on the host
