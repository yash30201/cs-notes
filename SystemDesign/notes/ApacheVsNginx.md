# Apache vs NginX

## Apache

It's a http server created in 1995 and was the most popular server on the internet from at least 1996 through 2016. Because of this popularity, Apache benefits from:

- Great documentation
- Flexibility
- Power
- Near-universal support
- It is extensible through a dynamically loadable module system and can directly serve many scripting languages, such as PHP, without requiring additional software.

## NginX

In 2002, Igor Sysoev began work (released in 2004) on Nginx as an answer to the C10K problem, which was an outstanding challenge for web servers to be able to handle ten thousand concurrent connections. NginX solves this by:

- Relying on asynchrounous event driven architecture
- Nginx surpassed Apache in popularity due to its:
    - Lightweight footprint
        - *Thus resource efficient*
    - Ability to scale easily on minimal hardware.
        - *Responsive under load*
    - Straightforward configuration syntax
    - Excels at serving static content quickly
    - Own robust module system
    - Can proxy dynamic requests off to other software as needed


## Connection Handling Architecture

One difference between Apache and Nginx is the specific way that they handle connections and network traffic.

### Apache

Provides variety of multi-processing modules (Apache calls these MPMs) that dictate how client requests are handled:

- **mpm_prefork**: Spawns processes with a single thread each to handle requests:
    - Each child can handle a single connection at a time.
    - MPM is difficult to scale effectively as RAM is limited => limited max number of processes.
- **mpm_worker**: Spawns processes that can each manage multiple threads:
    - Each of these threads can handle a single connection.
    - Threads are much more efficient than processes => MPM scales better than the prefork MPM
- **mpm_event**: Similar to the worker module in most situations, but is optimized to handle keep-alive connections:
    - In `mpm_worker`, a connection will hold a thread regardless of whether a request is actively being made for as long as the connection is kept alive:
    - `mpm_event` handles keep alive connections by setting aside dedicated threads for handling keep alive connections
    - Passes active requests off to other threads
    - This keeps the module from getting bogged down by keep-alive requests, allowing for faster execution.

### NginX

**Designed for Concurrency**: Addressing limitations: Nginx was created specifically with these evolving web demands in mind. Its core focus is on handling many connections simultaneously (concurrency) with minimal resource overhead.

- **Asynchronous**: Doesn't wait for one task to fully complete before starting the next.
- **Non-blocking**: Requests don't lock up resources. While waiting for external factors (reading a file, database response), Nginx can work on other things.
- **Event Loop**: A central mechanism that constantly monitors incoming events (like new connections, data arriving, data ready, etc). As events trigger, Nginx responds quickly.
- It has lightweight worker processes, each capable of juggling thousands of connections.

**The magic of the Event Loop**:

- Connections sit in the loop.
- Nginx only actively works on them when events occur (data ready, connection closed).
- Processing happens in a non-blocking way, allowing the worker to switch between many connections super efficiently.
- **The Result**: Efficiency and Scale
- **Less overhead**: Because Nginx isn't constantly creating/destroying processes or threads, its memory usage is low and predictable.
- **Handling spikes**: Can serve many more users with the same hardware compared to a traditional server like Apache. ◊This is why it often powers very high-traffic websites.


## Static and Dynamic Content Handling

### Static Content

**Apache**: Handles static content (files like HTML, CSS, images) directly. Performance depends largely on its internal work allocation methods (MPMs).
**Nginx**: Designed to excel at serving static content. Its event-driven architecture makes it super efficient in this area.

### Dynamic Content

#### Apache

Can process dynamic content (PHP, Python, etc.) internally using embedded modules.

**Advantage**: Tight integration, contributed heavily to the popularity of "LAMP" stacks.

**Downside**: Module overhead exists even when serving static files.

#### Nginx

Requires external processors (like PHP-FPM) to handle dynamic content. Communication done through protocols like http, FastCGI, SCGI, uWSGI, memcache, etc.

**Advantage**: Separates static and dynamic processing. Static content remains super lightweight; dynamic interpreters are loaded only when needed.

### Key Takeaways

- Nginx is often favored for its efficiency in handling large volumes of connections, especially if serving a mix of static and dynamic content.
- Apache can be a good choice for simpler setups or where tight integration with dynamic languages is important.

## Distributed vs Centralized Configuration

### Apache

Apache includes an option of reading hidden `.htaccess` files within subdirectories. This:
- Changes are implemented directly without the need for server reload.
- Allows non-priviledged users to control certain aspects of their own web content without giving them control over the entire configuration file.
- Subdirectories override the parent dir overlapping configurations.

### NginX

*Apache was originally developed at a time when it was advantageous to run many heterogeneous web deployments side-by-side on a single server, and delegating permissions made sense.*

Nginx was developed at a time when individual deployments were more likely to be containerized and to ship with their own network configurations, minimizing this need. This may be less flexible in some circumstances than the Apache model, but it does have its own advantages:
- Increased performance
- Security due to centralized configuration.
    - Distributing directory-level configuration access also distributes the responsibility of security to individual users, who may not be trusted to handle this task well.

## Request Interpretation

### Apache

Apache provides the ability to interpret a request as a physical resource on the filesystem or as a URI location:
- `<Directory>` or `<Files>` blocks for File System request
- `<Location>` blocks for more abstract URI request

Default behaviour is to interpret requests as filesystem resources. Apache provides a number of alternatives for when the request does not match the underlying filesystem:
- Alias directive can be used to map to an alternative location.
- Using `<Location>` blocks is a method of working with the URI itself instead of the filesystem.
- Regular expression variants which can be used to apply configuration more flexibly throughout the filesystem.

While Apache has the ability to operate on both the underlying filesystem and other web URIs, it leans heavily towards filesystem methods. **This can be seen in some of the design decisions**, including the use of .htaccess files for per-directory configuration.

> The Apache docs themselves warn against using URI-based blocks to restrict access when the request mirrors the underlying filesystem.

### NginX

Nginx was created to be both a web server and a proxy server. Due to the architecture required for these two roles, it works primarily with URIs, translating to the filesystem when necessary.

Primary configuration blocks for Nginx are server and location blocks:
- **Server block** interprets the host being requested
- **Location block** maches portions of the URI that comes after the host and port.
    - At this point, the request is being interpreted as a URI, not as a location on the filesystem.
- For static files, all requests are mapped to a location on the filesystem.
    - First, Nginx selects the server and location blocks that will handle the request and then combines the document root with the URI, adapting anything necessary according to the configuration specified.

> Nginx does not check the filesystem until it is ready to serve the request, which explains why it does not implement a form of .htaccess files.

## Using both of them together

In certain scenarios, its beneficial to use the combination of Apache and Nginx, where Nginx sits in front (as [Reverse Proxy](ReverseProxy.md)) of Apache. It:
- Recieves all the client traffic
- Serves static content as this is nginx speciality (it fast!)
- Send requets which require non native language processing to respective Apache server.
- Increase performance by allowing horizontal scaling

> This method still would incurr SPF (Single point of Failure)!
