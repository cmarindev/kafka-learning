# Learning Kafka 
A repository used to learn Apache Kafka.


# How to use
Run `docker-compose up -d` to create the Kafka cluster and setup a broker

Create a topic:
```bash
docker exec broker \
kafka-topics --bootstrap-server broker:9092 \
             --create \
             --topic my-first-topic
```

Produce messages to the topic:
  - Run the next command and type some text. Each line is a new message.
  - Press Ctrl+D to exit
  
```bash
docker exec --interactive --tty broker \ 
kafka-console-producer --bootstrap-server broker:9092 \
                       --topic my-first-topic

```

Consume messages from topic
  - Wait to see the messages
  - Press Ctrl+C to exit
  
```bash
docker exec --interactive --tty broker \
kafka-console-consumer --bootstrap-server broker:9092 \
                       --topic my-first-topic \
                       --from-beginning
```

  Stop the Kafka broker with `docker-compose down`


\* Producer and consumer do not need to be running at the same time if the `--from-beggining` flag is included. (This option forces the consumer to retrieve every produced message on the topic, no matter how old. **Should not be use in production**)

# Resources
- [Confluent Kafka 101](https://developer.confluent.io/learn-kafka/apache-kafka/events/?utm_medium=sem&utm_source=google&utm_campaign=ch.sem_br.nonbrand_tp.prs_tgt.kafka_mt.xct_rgn.emea_lng.eng_dv.all_con.kafka-general&utm_term=apache+kafka&placement=&device=c&creative=&gclid=CjwKCAjwoMSWBhAdEiwAVJ2ndvuiHzU6biN_sZ4hb1ixOW2wUg2Ew6GgbXQME4C3e6SelDi86HSmChoCzTQQAvD_BwE)
- [Confluent Quick Start](https://developer.confluent.io/quickstart/kafka-docker/)

docker exec --interactive --tty broker \
kafka-console-producer --bootstrap-server broker:9092 \
                       --topic poems
                       --property parse.key=true \
                       --property key.separator=":"

docker exec --interactive --tty broker \
kafka-console-consumer \
  --topic orders \
  --bootstrap-server broker:9092 \
  --from-beginning \
  --property print.key=true \
  --property key.separator="-"