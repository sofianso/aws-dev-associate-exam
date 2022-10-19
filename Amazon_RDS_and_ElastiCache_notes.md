# Amazon RDS and ElastiCache Notes

- Amazon RDS is a managed service that makes it easy to set up, operate, and scale a relational database in the cloud.
- It is mainly used for Online Transaction Processing (OLTP) such as storing orders details.
- You do not have access to the underlying EC2 instance (no root access).
- Supported database engines:
  - Amazon Aurora
  - MySQL
  - MariaDB
  - Oracle
  - SQL Server
  - PostgreSQL
- You can only scale RDS up (Compute and Storage). For example, `db.m4.large 8GB RAM` to `db.m4.2xl 32GB RAM`.
- MySQL is the only DB engine that can't be scaled in storage and storage type.
- Scaling compute will cause downtime.

## Multi-AZ Deployments VS Read Replicas

### Multi-AZ Deployments

- You use Multi-AZ RDS for Disaster Recovery.
- A standby copy of the DB in another AZ which is a synchronous replication (which is highly durable). Only the database engine on primary instance is active.
- Automated backups are taken from standby.
- Automatic failover to standby when a problem is detected. When the primary DB instance fails, the standby DB copy will be remapped (including DNS endpoint).

### Read Replicas

- Read replicas are asynchronous replications which are highly scalable since there would multiple replicas.
- Can be promoted to a standalone database engine.
- No backups configured by default.
- All read replicas are accessible and can be used for read scaling.

### Key Features of AWS Aurora

- High performance.
- DB compatibility with MySQL and PostgreSQL.
- Aurora replicas up to 15.
- MySQL Read Replicas.
- Global Database with low latency reads and fast replication.
- Serverless.
- Pay per second only when is active.

### Amazon ElastiCache

- Amazon ElastiCache is usually placed in front of RDS. Its main purpose is to improve latency for many read-heavy application workloads or compute-intensive workloads by using **in-memory caching**.
- It's best used for data that doesn't change often.
- Best for recommendation engines to store the results or storing sessions.
- You pay by node sie and hours of use.

### Memcached VS. Redis

#### Memcached

- Not data persistence.
- Doesn't have high availability (replication).
- No backup and restore.
- No snapshots.
- Multithreaded.
- No encryption.

#### Redis (cluster mode disabled)

- Data persistence.
- High availability (replication).
- Backup and restore.
- Snapshots.
- Encryption.
- No data partitioning.
- Single shard.

#### Redis (cluster mode enabled)

- Data persistence.
- High availability (replication).
- Backup and restore.
- Snapshots.
- Encryption.
- Data partitioning.
- Add shards.

### Lazy Loading

- Lazy loading caching is best paired with TTL. For example, every 1 hr it fetches new data for the recommendations. Or, sessions gets deleted after 30 minutes.
- Alterative caching strategy
  - Write Through
    - Write Through is when the cache gets updated whenever a new write or update is made to the underlying database.
    - Ideally it must have TTL or you can end up with a lot of cached data that is never read.
