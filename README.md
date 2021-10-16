**Ansible Scripts to Deploy Zookeeper, Kafka and YARN on an Linux-based env**

*Command execution order:*

1. ansible-playbook -i openstack_inventory ansible_kafka.yml
2. ansible-playbook -i openstack_inventory ansible_prepare_yarn.yml
3. ansible-playbook -i openstack_inventory ansible_yarn.yml

_Artefact versions:_
* kafka_version: kafka_2.12-3.0.0
* zookeeper_version: zookeeper-3.5.5
* hadoop_version: hadoop-3.3.1
* Java JDK 8

**Known issues during the process**

- Kafka has some permission issues starting. I have fixed them in the install.yml.
- Major issue is the version of hadoop. According to this: https://www.morling.dev/blog/bytebuffer-and-the-dreaded-nosuchmethoderror/ i have fixed it manually. The 
```hadoop-yarn-common-3.3.1.jar``` needs a rebuild with some changes.
- Also the yarn.properties file is needed to run the samza job.
- Lessons learned: Package your app and run everything from the yarn resource manager VM.

```
yarn.package.path="<your packaged app>-dist.tar.gz"

# Job
job.factory.class=org.apache.samza.job.yarn.YarnJobFactory
job.container.count=2

# default system
job.coordinator.system=kafka
job.default.system=kafka
systems.kafka.samza.factory=org.apache.samza.system.kafka.KafkaSystemFactory
systems.kafka.consumer.zookeeper.connect=127.0.0.1:2181
systems.kafka.producer.bootstrap.servers=127.0.0.1:9092
systems.kafka.default.stream.replication.factor=1
```
