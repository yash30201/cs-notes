# Database Replication

- Usually done with a Master Slave configuration
- One master, many slaves
- Writes in master
- Replication to slaves
- Reads from slaves.
- Favours most of the systems as they have high read write ratio
- Allows failover
- Increases redundancy of the system, eliminating SPOF

## Pros

- **Better Performance**: Segregation of read and writes
- **Parallelism**: Allows parallel reads
- **Reliability**: No need to word about data loss as it replicated
- **High Availability**: Traffic diversion to functioning servers

## Cons / Challenges

- If master goes offline, a slave db is promotes to master
  - This is challenging task
  - Takes time for slave to get updated from the data recovery scripts.

## Replication Methods

Master slave is just one of the replication methods. There are others like multi-masters, circulat replication, etc.
