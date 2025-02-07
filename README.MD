# TMS REDIS

This repository contains a Dockerfile for building a Redis image with a custom configuration file. The image is based on the official Redis `8.0-M03` image and includes a pre-configured `redis.conf` file.

## Dockerfile Overview

```dockerfile
FROM redis:8.0-M03

COPY redis.conf /usr/local/etc/redis/redis.conf

EXPOSE 6379

CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]
```

### Features
- Based on Redis `8.0-M03`.
- Custom configuration file (`redis.conf`) included.
- Exposes the default Redis port `6379`.
- Starts the Redis server with the custom configuration file.

## How to Use

1. **Clone this repository:**
   ```bash
   git clone <repository_url>
   cd <repository_name>
   ```

2. **Customize the configuration file:**
   Edit the `redis.conf` file to your preferences.

3. **Build the Docker image:**
   ```bash
   docker build -t custom-redis .
   ```

4. **Run the Docker container:**
   ```bash
   docker run -d -p 6379:6379 --name redis-server custom-redis
   ```

5. **Access Redis CLI:**
   ```bash
   docker exec -it redis-server redis-cli
   ```

## Configuration Details

### Networking
The following settings are used to secure and configure network access:

```conf
bind 127.0.0.1 192.168.1.10
protected-mode yes
port 6379
```

- `bind`: Defines the IP addresses Redis will listen on.
- `protected-mode`: Ensures Redis is secure by default.
- `port`: Redis port (default is 6379).

### Performance
Optimized for better performance:

```conf
maxmemory 2gb
appendfsync everysec
save 900 1
save 300 10
save 60 10000
```

- `maxmemory`: Limits the maximum memory usage to 2GB.
- `maxmemory-policy`: Evicts keys based on the LRU policy.
- `appendonly` and `appendfsync`: Enables AOF persistence and synchronizes every second.
- `save`: Sets snapshot intervals for RDB persistence.

### Resource Management

```conf
maxclients 10000
timeout 300
tcp-keepalive 60
```

- `maxclients`: Limits the number of concurrent clients to 10,000.
- `timeout`: Disconnects idle clients after 300 seconds.
- `tcp-keepalive`: Ensures active connections remain alive.

### Logging and Monitoring

```conf
loglevel notice
slowlog-log-slower-than 10000
slowlog-max-len 128
```

- `loglevel`: Sets the logging level to `notice`.
- `slowlog-log-slower-than` and `slowlog-max-len`: Configures slow query logging.

### High Availability

```conf
replica-read-only yes
```

- `replica-read-only`: Ensures replicas are read-only.


### Security

```conf
rename-command FLUSHALL "disabled-xyz"
rename-command SHUTDOWN "disabled-def"
```

- `rename-command`: Renames sensitive commands to enhance security.

### Thread Management

```conf
io-threads-do-reads yes
io-threads 4
```

- `io-threads-do-reads`: Enables multi-threaded reads.
- `io-threads`: Configures the number of I/O threads.

### Miscellaneous

```conf
hz 50
activerehashing yes
```

- `hz`: Adjusts the frequency of Redis housekeeping.
- `activerehashing`: Improves hash table performance.

## License
This work is licensed under a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](./LICENSE).
