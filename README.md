# redis-cluster
The redis-cluster repository is a collection of scripts that can be used to create a Redis cluster locally or in a distributed fashion. This repository exists to capture lessons learned during the process of setting up a Redis cluster across multiple machines, as setup information can be sparse or aimed primarily at creating a cluster on one machine. Completing the [Redis Cluster tutorial](https://redis.io/topics/cluster-tutorial) as well as reading the [Redis Cluster specification](https://redis.io/topics/cluster-spec) will aid in understanding the scripts contained in the repository.

## Preparing the Cluster
Before a cluster can be created, a number of Redis instances need to be running. Redis documentation recommends a minimum of three master nodes and three slave nodes. The ``bash_scripts`` folder contains several helpful scripts for accomplishing the required setup.



The ``start_instances.sh`` script starts a number of instances depending on the range of ports passed to the script as arguments. The first argument will be used as the starting port while the second argument will specify an end port. The following command creates Redis instances on ports 7000, 7001, 7002, 7003, 7004, and 7005. 
```
./start_instances.sh 7000 7005
```
A peek into ``start_instances.sh`` shows the contents of the config file created for each instance. Each port has a directory containing the config file. This config is an extension of another config file found in an article written by [Monsurul Haque Shimul](https://cleanprogrammer.net/setting-up-a-high-available-multi-node-redis-cluster/). Setting ``protected-mode no`` is not recommended in production.

```bash
port ${port}
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
protected-mode no

dir ./
loglevel notice
logfile ${port}.log

save 900 1
save 300 10
save 60 10000
```

## Starting the Cluster
The documentation for this repository is ongoing and will be completed soon. 