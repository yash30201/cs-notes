# Harward Scalability Lecture

## Vertical Scaling

Vertical scaling has hardware limits (upper ceiling) eventually either due to the technology constrains or due to maintainance constraints.

## Horizontal Scaling

This is where horizontal scaling comes, knowing that we'll eventually hit the ceiling in vertical scaling, we just make peace with low spec machines and try to use multiple of them to get a increased capacity

## Caching

Since multiple machines are involved, thats why a requirement arises for a centralized caching system.

## Load Balancing

Since there are multiple machines, a need of a system which will route the incoming request to appropriate resource arises, this is called load balancer.

Load balancer can become a Single Point of Failure (SPF) and hence it makes sense to have two load balancers in Active - Active mode or Active - Passive mode. In both modes, the load balancers send and recieve heart beats of the other one so that they know the overall status of the system and step up / step down to a dominant position as per the need.

## Database Replication

In any database, it can become a SPF if just used in a single machine. That's why it makes sense to have atleast one replicas. As replicas are introduces, we need to introduce a load balancer again to route traffic to less busy database.

## Database Partitioning

In master slave configuration of databases, especially in read heavy systems, it's better to divert the read queries of a particular set of users to a partition and another set of users to other partition. All the reads go to the master and the reads through slaves.
