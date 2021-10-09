**Ansible Scripts to Deploy Zookeeper, Kafka and YARN on a Linux Cluster (Vagrant or AWS)**

*Command execution order:*

1. ansible-playbook -i openstack_inventory ansible_kafka.yml
2. ansible-playbook -i openstack_inventory ansible_prepare_yarn.yml
3. ansible-playbook -i openstack_inventory ansible_yarn.yml

_Artefact versions:_
* kafka_version: kafka_2.12-3.0.0
* zookeeper_version: zookeeper-3.5.5
* hadoop_version: hadoop-3.3.1
* Java JDK 8
