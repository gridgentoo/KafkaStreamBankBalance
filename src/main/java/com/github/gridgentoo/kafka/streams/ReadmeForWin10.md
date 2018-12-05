# Создаем input topic with one partition to get full ordering
kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic bank-transactions

# смотрим список Топиков
kafka-topics --zookeeper 127.0.0.1:2181 --list 

# Создаем output log compacted topic
kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic bank-balance-exactly-once --config cleanup.policy=compact

# смотрим список Топиков
kafka-topics --zookeeper 127.0.0.1:2181 --list

# Запускаем Kafka consumer
kafka-console-consumer --bootstrap-server localhost:9092 ^
    --topic bank-balance-exactly-once ^
    --from-beginning ^
    --formatter kafka.tools.DefaultMessageFormatter ^
    --property print.key=true ^
    --property print.value=true ^
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer ^
    --property value.deserializer=org.apache.kafka.common.serialization.StringDeserializer
    
# Запускаем в IDEA streams application


########################################################################################
# package your application as a fat jar
mvn clean package

# run your fat jar
java -jar <your jar here>.jar

# list all topics that we have in Kafka (so we can observe the internal topics)
kafka-topics --list --zookeeper localhost:2181
