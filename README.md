# Stock-Market-Real-Time-Data-Streaming
Stock Market Real-Time Data Streaming Using Kafka

Credit : Darshil Parmar Youtube Channel

![image](https://github.com/chenphopp/Stock-Market-Real-Time-Data-Analysis/assets/82653803/55e77597-da59-4a0a-9aef-cb1974e47a6d)

## Install Kafka
```
wget https://archive.apache.org/dist/kafka/3.3.1/kafka_2.12-3.3.1.tgz
tar -xvf kafka_2.12-3.3.1.tgz
```
```
java -version
sudo yum install java-1.8.0-amazon-corretto-devel
java -version
cd kafka_2.12-3.3.1
```
## Start Zookeeper
```
bin/zookeeper-server-start.sh config/zookeeper.properties
```
## Start Kafka
-----------
Duplicate the session & enter in a new console --
```
export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"
cd kafka_2.12-3.3.1
bin/kafka-server-start.sh config/server.properties
```
It is pointing to private server , change server.properties so that it can run in public IP 

To do this , you can follow any of the 2 approaches shared belwo --
Do a "sudo nano config/server.properties" - change ADVERTISED_LISTENERS to public ip of the EC2 instance

## Create the topic
```
cd kafka_2.12-3.3.1
bin/kafka-topics.sh --create --topic demo-testing --bootstrap-server {Put the Public IP of your EC2 Instance:9092} --replication-factor 1 --partitions 1
```

<img width="1201" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Analysis/assets/82653803/aa45f444-c8e5-4c4f-938a-eea89a5b6e47">

## Start Producer
```
bin/kafka-console-producer.sh --topic demo-testing --bootstrap-server {Put the Public IP of your EC2 Instance:9092} 
```

<img width="932" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Analysis/assets/82653803/cca84436-8648-4bff-b27b-bb2670533677">


## Start Consumer

Duplicate the session & enter in a new console --
```
cd kafka_2.12-3.3.1
bin/kafka-console-consumer.sh --topic demo-testing --bootstrap-server {Put the Public IP of your EC2 Instance:9092}
```

<img width="939" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Analysis/assets/82653803/5fde9abc-97a1-4208-bfdf-35d19e605645">

## Install Jupiter Notebook on MAC M1
```
brew install pyenv
```
```
pyenv install --list
pyenv install 3.10.12
pyenv global 3.10.12
```
```
pyenv init
```

![image](https://github.com/chenphopp/Stock-Market-Real-Time-Data-Analysis/assets/82653803/87d21dcf-79f8-4ba9-a1e0-cd52df70b4ac)

```
python --version
```

Install Jupiter Notebook
```
jupyter notebook
```

![image](https://github.com/chenphopp/Stock-Market-Real-Time-Data-Analysis/assets/82653803/ab34a330-dd7e-4c89-8906-71ff7bfb0c6e)

# Create KafkaProducer and KakfaConsumer
- KafkaProducer.ipynb for producer application
- KafkaConsumer.ipynb for consumer application

## Create S3 for store data

<img width="1090" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Streaming/assets/82653803/f00eabc1-09e7-4d69-b82f-66bd652d060b">

## Create user for access S3 from your machine

<img width="1090" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Streaming/assets/82653803/0a31dcdc-d9e3-407f-83e7-4dc3dff06a24">


Give S3 full access permission then copy Access key ID and Secret access key for below 

```
## Do it on your host machine ***
chenphop@Chenphops-MacBook-Pro Downloads % aws configure
AWS Access Key ID [****************C25A]: ..
AWS Secret Access Key [****************ekD0]: ..
```

*You need to install aws cli first*

## Create AWS Glue for sourcing and loading table

<img width="1148" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Streaming/assets/82653803/fc008e5c-5ca5-4bbe-b999-1782a593f231">

create role for Glue and give full access permission

<img width="1087" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Streaming/assets/82653803/eba25e70-f00c-453e-803e-89f85c758404">

## Now you can queury the data with queury service (Aws Athena)


<img width="631" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Streaming/assets/82653803/69291564-6955-47be-8713-fd8c4c7682ca">

This is the result!!

<img width="1031" alt="image" src="https://github.com/chenphopp/Stock-Market-Real-Time-Data-Streaming/assets/82653803/cf62c3b3-67e4-4b5f-a7da-b9b318111ce5">



