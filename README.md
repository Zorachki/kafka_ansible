# Kafka Ansible

It's just an Ansible role to set up Kafka cluster on three nodes and nothing else. You can use it (I believe) on these

## Platforms

- Ubuntu 20.04, 18.04
- CentOS 7,8
- Debian 10.x
- RHEL 7,8

So all you need are

## Requirements

- Ansible >=2.9.6 on your deploy machine `sudo yum install ansible`(CentOS or RHEL) and `sudo apt install ansible`(Ubuntu or Debian)
- Internet connection, I guess

## Install

Put your IP addresses into 'hosts' file and run
```sh
ansible-playbook -i hosts start.yml
```
Also you can change Kafka or Scala version in `roles/kafka/default/main.yml`. There are another settings of Kafka server.
Default Kafka version is 3.1.0 and Scala version – 2.13.

## Testing

First of all change directory (/opt/kafka default)
`cd /opt/kafka`
then
Check the number of connected brokers (it must be three WATCHERS)

`bin/zookeeper-shell.sh 127.0.0.1:2181 ls /brokers/ids`

Create a test topic

`bin/kafka-topics.sh --create --partitions 1 --replication-factor 1 --topic test-events --bootstrap-server localhost:9092`

View the description of the topic

`bin/kafka-topics.sh --describe --topic test-events --bootstrap-server localhost:9092`

Send a message

`bin/kafka-console-producer.sh --topic test-events --bootstrap-server localhost:9092`
(Quit - Ctrl+C)

Read the message

`bin/kafka-console-consumer.sh --topic test-events --from-beginning --bootstrap-server localhost:9092`
(Quit - Ctrl+C)
