
### **🛠 Project Overview**

Title: lab-streaming-pipelines-kafka

Description: 
This repository provides a hands-on introduction to the fundamentals of Apache Kafka using the KRaft (Kafka Raft) consensus protocol. This lab guides users through setting up a local Kafka environment, creating topics, and orchestrating a real-time data flow between a producer and a consumer without the need for Zookeeper.


<br>

### **🛠 Prerequisites**

#### Download and extract Kafka

Download Kafka by running the command below:
```Bash
wget https://archive.apache.org/dist/kafka/3.8.0/kafka_2.13-3.8.0.tgz
```

Extract Kafka from the zip file by running the command below.
```Bash
tar -xzf kafka_2.13-3.8.0.tgz
```

#### Configure KRaft and start server

Navigate to the kafka_2.13-3.8.0 directory.

```Bash
cd kafka_2.13-3.8.0
```

Generate a cluster UUID that will uniquely identify the Kafka cluster.

```Bash
KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"
```

KRaft requires the log directories to be configured. Run the following command to configure the log directories passing the cluster ID

```Bash
bin/kafka-storage.sh format -t $KAFKA_CLUSTER_ID -c config/kraft/server.properties
```

Now that KRaft is configured, you can start the Kafka server by running the following command.
<br>
You can be sure that the Kafka server has started when the output displays messages like "Kafka Server started".

```Bash
bin/kafka-server-start.sh config/kraft/server.properties
```

### 🛠 **How to Practice**

#### Create a topic and start producer

Start a new terminal and change to the kafka_2.13-3.8.0 directory.

```Bash
cd kafka_2.13-3.8.0
```

To create a topic named news, run the command below.
```Bash
bin/kafka-topics.sh --create --topic news --bootstrap-server localhost:9092
```

You need a producer to send messages to Kafka. Run the command below to start a producer.
```Bash
bin/kafka-console-producer.sh   --bootstrap-server localhost:9092   --topic news
```

After the producer starts, and you get the '>' prompt, type any text message and press enter. Or you can copy the text below and paste. The below text sends three messages to Kafka.
```Bash
Good morning
Good day
Enjoy the Kafka lab
```

#### Start Consumer

Start a new terminal and change to the kafka_2.13-3.8.0 directory.
```Bash
cd kafka_2.13-3.8.0
```

- Run the command below to listen to the messages in the topic news.
- You should see all the messages you sent from the producer appear here.
- You can go back to the producer terminal and type some more messages, one message per line, and you will see them appear here.
```Bash
bin/kafka-console-consumer.sh   --bootstrap-server localhost:9092   --topic news   --from-beginning
```

#### Explore Kafka directories

Kafka uses the /tmp//tmp/kraft-combined-logs directory to store the messages.
Start a new terminal and navigate to the kafka_2.13-3.8.0 directory.

```Bash
cd kafka_2.13-3.8.0
```

Explore the root directory of the server.

```Bash
ls
```

- Notice there is a tmp directory. The kraft-combine-logs inside the tmp directory contains all the logs. To check the logs generated for the topic news run the following command:
- Note: All messages are stored in the news-0 directory under the /tmp/kraft-combined-logs directory.

```Bash
ls /tmp/kraft-combined-logs/news-0
```

#### Clean up

To stop the producer
In the terminal where you are running producer, press 
```Bash
CTRL+C.
```

To stop the consumer
In the terminal where you are running consumer, 
```Bash
press CTRL+C.
```

To stop the Kafka server
In the terminal where you are running Kafka server, 
```Bash
press CTRL+C.
```


