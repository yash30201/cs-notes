# Scalability For Dummies

<cite>Article [Link](https://web.archive.org/web/20221030091841/http://www.lecloud.net/tagged/scalability/chrono)</cite>

---

# First Golden Rule of Scalability

All the servers should have the same codebase and should never store any user specific data (like sessions, etc).

Sessions should be stored in a centralised external store accesible to all the webservers, like external database or a external persistent cache like Redis.

# Server Codebase Updation

**Problem statement**: How do we make sure that a code change in the codebase gets reflected to all the servers?

**Solution**: This problem is solved through automation servers like Capistrano, Jenkins, Ansible (this is a complete orchestration engine and has much more functionalities), etc

# Images

After codebase updation and cache outsourcing, we can create an image of a web server (like docker image) and just use this for spawning extra web servers whenever needed!

<cite>Part 1 ends</cite>

Now, we've scaled servers horizontally and are serving thousands of concurrent request! But somewhere down the road application gets slower and slower and slower until it breaks down!

Reason !? Our database, MySql isn't it?

# Database

There are two ways going ahead to mitigate this issue:

## Path 1

*Keep the Beast (*MySql*) running!!!*

Hire a DBA (Database Adminstrator) to:
- Implement master slave replication (reads from slave, writes to master)
- Upgrade master's RAM by adding more and more and more

In some time, the DBA will come up with works like Sharding, Normalization and SQL Tuning and will look worries about overtime over the next few weeks.

At that point, every new action to keep the database running would be more expensive and more time consuming than the previous action, **hence better of going with Path 2 from the starting!**

## Path 2

Denormalize the database right from the starting (wait... what is [normalization](DatabaseNormalization.md)?):
- Avoiding computational heave JOIN operation!
- In the case where joins are necessary, they would be done in the Application code.

We can stay with MySql and treat it as NoSql db or move to a NoSql db like MongoDB or CouchDB.

The sooner we do this normalization and join in application layer step, the better it is. But still!!, even after getting the most latest and greatest NoSql DB, soon your database requests will becomes slower and slower. We introduce a cache for this!

# Cache

We've now build a scalable database and now have no fear of terabytes, world is looking great! But users still suffer when system is loaded! We can improve this by caching!

There would be two ways to cache results:

## Cached Database Queries

- Let a user do a query `q`.
- Serialize `q` into some hash `h`
- Look for `h` in cache.
    - If cache hit
        - Return `value[h]`
    - Else
        - Fetch the value `v` from database
        - Return the `value[h] = v`

### Problem !?

**Expiration!!** What if some cell's value changes in the table, which cache data to update? (finding this since queries are stores in hashes?...wow)

## Cached Objects

We create class respresenting the query's output format and then search an object of this class in the cache. For example:

Products:
  id | name          | price
-------|---------------|-------
  1  | T-Shirt       | $20
  2  | Running Shoes | $80

Reviews:
  id | product_id | rating | content
-------|-------------|--------|---------
  1  | 1           | 5      | Great quality!
  2  | 2           | 4      | Comfortable fit.

- User wants all reviews for `T-Shirt`
- Let us denote this info by a class called `Reviews` which takes `name` as constructor argument
- See if an object `Reviews('T-Shirt')` is present in cache
- If yes then get the value from cache, deserilize it and return.
- If not the fetch the data, populate the object, serialize it, cache it and then return the object.

### Pros

- **Easy updates on table value change**: Easy to figure out which cache elements are invalidated.
- **Asynchrounous Creation of cache!!**: Assume an army of workers assembling object for you. This allows to update the affected cache when some write operation occurs in the db.

## Some ideas of objects to cache:

- User sessions! (never store in database)
- Fully rendered web page like some article / blog
- Activity streams (read heavy and less write operation, that too not mandatory to be super accurate instantly)


Example of caches: Memcached, Redis, GCP Memorystore, Amazon Memcached.

# Async Behaviour

*. . . . Please wait a while*

😤 Frustrating right?

To avoid this situation, asynchronous processing needs to be done. There would be two scenarios for async processing:

## Async 1

Regularly pre process dynamic pages to create static html pages and store it in some CDN. These regular processing could be done by setting up cron jobs. This would allows the user to get general and simple type of dynamic data in an instant! The server would be less bogged down by these tasks and would only spend time in doing complex task!

## Async 2

Whenever user asks something, just say it will be done, please continue to do something else in the website.

- Meanwhile, the client would constantly check for responses
- Backend would send response once processing is done.
- Client would get to know, 'Oh! the job is done, let's inform the user'

~~~
|--------------------|                         |--------------------|
|                    |------------------------>|  Request Server    |
|                    |<------------------------|                    |
|                    |                         |--------------------|
|                    |
|                    |                         |--------------------|
|                    |------------------------>|                    |
|                    |<------------------------|                    |
|                    |                         |                    |
|      Client        |------------------------>|    Status Server   |
|                    |<------------------------|                    |
|                    |                         |                    |
|                    |------------------------>|                    |
|                    |<------------------------|                    |
|                    |                         |--------------------|
|                    |
|                    |                         |--------------------|
|                    |------------------------>|   Resource Server  |
|                    |<------------------------|                    |
|--------------------|                         |--------------------|
~~~

