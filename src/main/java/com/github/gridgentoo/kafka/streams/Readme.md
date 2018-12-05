# Создаем input topic with one partition to get full ordering
kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic bank-transactions

# смотрим список Топиков
kafka-topics --zookeeper 127.0.0.1:2181 --list 

# Создаем output log compacted topic
kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic bank-balance-exactly-once --config cleanup.policy=compact

# смотрим список Топиков
kafka-topics --zookeeper 127.0.0.1:2181 --list