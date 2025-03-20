
# Kafka Useful Commands

This document contains a collection of useful Kafka commands for managing and interacting with Kafka clusters.

## **1. Start Kafka Broker**

path = /usr/bin

To start a Kafka broker, use the following command:
```bash
kafka-server-start.sh /path/to/kafka/config/server.properties
```

## **2. Start Zookeeper (if using standalone Zookeeper)**

If using standalone Zookeeper, use this command to start it:
```bash
zookeeper-server-start.sh /path/to/kafka/config/zookeeper.properties
```

## **3. Kafka Topics**

### **3.1. List All Topics**
To list all topics in the Kafka cluster:
```bash
kafka-topics.sh --bootstrap-server <broker-address> --list
```

### **3.2. Create a New Topic**
To create a new topic:
```bash
kafka-topics.sh --bootstrap-server <broker-address> --create --topic <topic-name> --partitions <num-partitions> --replication-factor <num-replication>
```

Example:
```bash
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic my-topic --partitions 3 --replication-factor 1
```

### **3.3. Describe a Topic**
To describe a topic (view its configuration and partition information):
```bash
kafka-topics.sh --bootstrap-server <broker-address> --describe --topic <topic-name>
```

### **3.4. Delete a Topic**
To delete a topic:
```bash
kafka-topics.sh --bootstrap-server <broker-address> --delete --topic <topic-name>
```

## **4. Produce Messages to a Kafka Topic**

### **4.1. Using Kafka Console Producer**
To produce messages to a Kafka topic using the command line:
```bash
kafka-console-producer.sh --bootstrap-server <broker-address> --topic <topic-name>
```

- Type your message and press Enter to send.
- To send a message from a file:
```bash
kafka-console-producer.sh --bootstrap-server <broker-address> --topic <topic-name> < message-file.txt
```

## **5. Consume Messages from a Kafka Topic**

### **5.1. Using Kafka Console Consumer**
To consume messages from a Kafka topic:
```bash
kafka-console-consumer.sh --bootstrap-server <broker-address> --topic <topic-name> --from-beginning
```

- To consume messages from the end of the topic:
```bash
kafka-console-consumer.sh --bootstrap-server <broker-address> --topic <topic-name>
```

### **5.2. Consume with Specific Offset**
To consume messages starting from a specific offset:
```bash
kafka-console-consumer.sh --bootstrap-server <broker-address> --topic <topic-name> --offset <offset>
```

## **6. Kafka Consumer Groups**

### **6.1. List Consumer Groups**
To list all consumer groups in the Kafka cluster:
```bash
kafka-consumer-groups.sh --bootstrap-server <broker-address> --list
```

### **6.2. Describe Consumer Group**
To describe a specific consumer group:
```bash
kafka-consumer-groups.sh --bootstrap-server <broker-address> --describe --group <consumer-group-name>
```

### **6.3. Reset Consumer Group Offsets**
To reset consumer group offsets:
```bash
kafka-consumer-groups.sh --bootstrap-server <broker-address> --group <consumer-group-name> --reset-offsets --to-earliest --execute --topic <topic-name>
```

## **7. Kafka Logs**

### **7.1. View Kafka Broker Logs**
Kafka broker logs are typically stored in `/logs` directory inside Kafka's installation directory. You can view logs like:
```bash
tail -f /path/to/kafka/logs/server.log
```

### **7.2. View Zookeeper Logs**
Zookeeper logs are stored in `/logs` directory of the Zookeeper installation:
```bash
tail -f /path/to/zookeeper/logs/zookeeper.log
```

## **8. Kafka Consumer Lag Monitoring**

### **8.1. Monitor Consumer Lag**
To monitor consumer lag for a topic, use:
```bash
kafka-consumer-groups.sh --bootstrap-server <broker-address> --describe --group <consumer-group-name>
```

This will show the lag between the consumer and the latest offset.

## **9. Produce JSON Message**

To send a JSON message using the Kafka producer, use `echo` or pipe the message:
```bash
echo '{"eventId": "12345", "eventType": "ORDER_PLACED", "timestamp": "2025-01-10T12:34:56Z"}' | kafka-console-producer.sh --bootstrap-server <broker-address> --topic <topic-name>
```

## **10. Kafka Configuration File**

### **10.1. Edit Kafka Broker Configurations**
The Kafka broker configuration file `server.properties` is where you configure Kafka settings like:
- `listeners`: Defines the broker's network address.
- `log.dirs`: Where log data is stored.
- `zookeeper.connect`: The address of Zookeeper.
- `log.retention.hours`: Sets the retention period for logs.

Example (edit `server.properties`):
```properties
listeners=PLAINTEXT://0.0.0.0:9092
log.dirs=/var/lib/kafka/data
zookeeper.connect=localhost:2181
```

## **11. Kafka Topic Partitions and Replication**

### **11.1. Change Number of Partitions**
To change the number of partitions for a topic:
```bash
kafka-topics.sh --bootstrap-server <broker-address> --alter --topic <topic-name> --partitions <new-num-partitions>
```

### **11.2. Alter Replication Factor**
Replication factor cannot be changed directly after a topic is created. You need to recreate the topic or use other methods like adding new brokers to the cluster and rebalancing.

## **12. Kafka Security**

### **12.1. Enable SSL**
To enable SSL for a Kafka producer or consumer, configure SSL settings in the `client.properties` file or Kafka server configuration:
```properties
security.protocol=SSL
ssl.keystore.location=/path/to/keystore.jks
ssl.keystore.password=<password>
ssl.key.password=<key-password>
ssl.truststore.location=/path/to/truststore.jks
ssl.truststore.password=<truststore-password>
```

### **12.2. SASL Authentication**
For SASL authentication, configure SASL properties in the configuration files:
```properties
security.protocol=SASL_PLAINTEXT
sasl.mechanism=PLAIN
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="user" password="password";
```

---

### **Conclusion**

These are some of the commonly used Kafka commands. For more advanced configurations and use cases, refer to the official [Kafka Documentation](https://kafka.apache.org/documentation/).

