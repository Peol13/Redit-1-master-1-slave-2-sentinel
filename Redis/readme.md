AUTH password: 5075ebcc35993270b30009791577bdcf58db5424

### Run 

cd .Redis\clustering\

docker compose up --build -d 

### info 


container name: 
redis-0
redis-1
sentinel-0
sentinel-1
network name:
clustering_redis

ports redis:
6379
ports sentinel:
5000


### Configuration

```
#persistence
dir /data
dbfilename dump.rdb
appendonly yes
appendfilename "appendonly.aof"

```
### redis-0 Configuration (master)

```
protected-mode no
port 6379

#authentication
masterauth 5075ebcc35993270b30009791577bdcf58db5424
requirepass 5075ebcc35993270b30009791577bdcf58db5424
```
### redis-1 Configuration (slave)

```
protected-mode no
port 6379
slaveof redis-0 6379

#authentication
masterauth 5075ebcc35993270b30009791577bdcf58db5424
requirepass 5075ebcc35993270b30009791577bdcf58db5424

```
###  SENTINEL CONFIG

```

port 5000
sentinel monitor mymaster redis-0 6379 2
sentinel down-after-milliseconds mymaster 5000
sentinel failover-timeout mymaster 60000
sentinel parallel-syncs mymaster 1
sentinel auth-pass mymaster 5075ebcc35993270b30009791577bdcf58db5424


