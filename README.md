# Create kafka cloud
Creates a kafka cloud on different servers. (here: virtual servers)



## on Server 1
ip:192.168.94.131

```
cat /etc/hosts

192.168.94.131  broker-1
192.168.94.132  broker-2
192.168.94.133  broker-3
```

$ git clone https://github.com/acimail01/multiarea-kafka-cluster.git

$ cd multiarea-kafka-cluster/node1

adjust .env-File

$ docker-compose up -d




## on Server 2
ip:192.168.94.132

```
cat /etc/hosts

192.168.94.131  broker-1
192.168.94.132  broker-2
192.168.94.133  broker-3
```

$ git clone https://github.com/acimail01/multiarea-kafka-cluster.git

$ cd multiarea-kafka-cluster/node2

adjust .env-File

$ docker-compose up -d





## on Server 3
ip:192.168.94.133

```
cat /etc/hosts

192.168.94.131  broker-1
192.168.94.132  broker-2
192.168.94.133  broker-3
```

$ git clone https://github.com/acimail01/multiarea-kafka-cluster.git

$ cd multiarea-kafka-cluster/node3

adjust .env-File

$ docker-compose up -d



## test from Server 1
```
docker exec -it kafka kafka-topics --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --create --topic topic01
docker exec -it kafka kafka-topics --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --create --topic topic02
docker exec -it kafka kafka-topics --bootstrap-server broker-1:9092  --replication-factor 3 --partitions 5 --create --topic topic03
docker exec -it kafka kafka-topics --bootstrap-server broker-2:9092  --replication-factor 3 --partitions 5 --create --topic topic04
docker exec -it kafka kafka-topics --bootstrap-server broker-3:9092  --replication-factor 3 --partitions 5 --create --topic topic05
```

## test from Server 2
```
docker exec -it kafka kafka-topics --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --create --topic topic07
docker exec -it kafka kafka-topics --bootstrap-server broker-1:9092  --replication-factor 3 --partitions 5 --create --topic topic08
docker exec -it kafka kafka-topics --bootstrap-server broker-2:9092  --replication-factor 3 --partitions 5 --create --topic topic09
docker exec -it kafka kafka-topics --bootstrap-server broker-3:9092  --replication-factor 3 --partitions 5 --create --topic topic10
```

## test from Server 3
```
docker exec -it kafka kafka-topics --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --create --topic topic11
docker exec -it kafka kafka-topics --bootstrap-server broker-1:9092  --replication-factor 3 --partitions 5 --create --topic topic12
docker exec -it kafka kafka-topics --bootstrap-server broker-2:9092  --replication-factor 3 --partitions 5 --create --topic topic13
docker exec -it kafka kafka-topics --bootstrap-server broker-3:9092  --replication-factor 3 --partitions 5 --create --topic topic14
```

```
docker exec -it kafka kafka-topics --bootstrap-server broker-3:9092  --replication-factor 5 --partitions 5 --create --topic shouldnotgo
```
