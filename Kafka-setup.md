# Kafka Setup on Mac OS

To install and run Kafka we need following:
* Java
* Zookeeper
* Kafka

# Verify Java installation

Open your terminal and check Java version
```java --version ```
Then you should see similar to this
```
java version "1.8.0_202"
Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)
``` 
If you don't have the correct version of Java, continue with the next steps.

Java can be installed by using Homebrew or manual installation (by downloading JDK file from Oracle)


## With Homebrew
```brew cask install java```
for java8
```brew cask install java8```

# Kafka download
First download kafka tar file from https://kafka.apache.org/downloads

Once it downloaded move kafka from downloads to root directory and untar it
``` 
mv Downloads/kafka_2.12-2.2.0 tgz . 
tar -xvf kafka_2.12-2.2.0
```
It should create a directory kafka_2.12-2.2.0 and it consists of folders bin,config,libs,site-docs

Now verify Java is working by following command

```
cd kafka_2.12-2.2.0 
bin/kafka-topics.sh
```
It should show you something like this

```
Create, delete, describe, or change a topic.
Option                                   Description                            
------                                   -----------                            
--alter                                  Alter the number of partitions,        
                                           replica assignment, and/or           
                                           configuration for the topic.         
--bootstrap-server <String: server to    REQUIRED: The Kafka server to connect  
  connect to>                              to. In case of providing this, a     
                                           direct Zookeeper connection won't be 
                                           required.                            
--command-config <String: command        Property file containing configs to be 
  config property file>                    passed to Admin Client. This is used 
                                           only with --bootstrap-server option  
                                           for describing and altering broker   
                                           configs.                             
--config <String: name=value>            A topic configuration override for the 
                                           topic being created or altered.The   
                                           following is a list of valid         
                                           configurations:                      
                                         	cleanup.policy                        
                                         	compression.type                      
                                         	delete.retention.ms                   
                                         	file.delete.delay.ms                  
                                         	flush.messages                        
                                         	flush.ms                              
                                         	follower.replication.throttled.       
                                           replicas                             
                                         	index.interval.bytes                  
                                         	leader.replication.throttled.replicas 
                                         	max.message.bytes                     
                                         	message.downconversion.enable         
                                         	message.format.version                
                                         	message.timestamp.difference.max.ms   
                                         	message.timestamp.type                
                                         	min.cleanable.dirty.ratio             
                                         	min.compaction.lag.ms                 
                                         	min.insync.replicas                   
                                         	preallocate                           
                                         	retention.bytes                       
                                         	retention.ms                          
                                         	segment.bytes                         
                                         	segment.index.bytes                   
                                         	segment.jitter.ms                     
                                         	segment.ms                            
                                         	unclean.leader.election.enable        
                                         See the Kafka documentation for full   
                                           details on the topic configs.It is   
                                           supported only in combination with --
                                           create if --bootstrap-server option  
                                           is used.                             
--create                                 Create a new topic.                    
--delete                                 Delete a topic                         
--delete-config <String: name>           A topic configuration override to be   
                                           removed for an existing topic (see   
                                           the list of configurations under the 
                                           --config option). Not supported with 
                                           the --bootstrap-server option.       
--describe                               List details for the given topics.     
--disable-rack-aware                     Disable rack aware replica assignment  
--exclude-internal                       exclude internal topics when running   
                                           list or describe command. The        
                                           internal topics will be listed by    
                                           default                              
--force                                  Suppress console prompts               
--help                                   Print usage information.               
--if-exists                              if set when altering or deleting or    
                                           describing topics, the action will   
                                           only execute if the topic exists.    
                                           Not supported with the --bootstrap-  
                                           server option.                       
--if-not-exists                          if set when creating topics, the       
                                           action will only execute if the      
                                           topic does not already exist. Not    
                                           supported with the --bootstrap-      
                                           server option.                       
--list                                   List all available topics.             
--partitions <Integer: # of partitions>  The number of partitions for the topic 
                                           being created or altered (WARNING:   
                                           If partitions are increased for a    
                                           topic that has a key, the partition  
                                           logic or ordering of the messages    
                                           will be affected                     
--replica-assignment <String:            A list of manual partition-to-broker   
  broker_id_for_part1_replica1 :           assignments for the topic being      
  broker_id_for_part1_replica2 ,           created or altered.                  
  broker_id_for_part2_replica1 :                                                
  broker_id_for_part2_replica2 , ...>                                           
--replication-factor <Integer:           The replication factor for each        
  replication factor>                      partition in the topic being created.
--topic <String: topic>                  The topic to create, alter, describe   
                                           or delete. It also accepts a regular 
                                           expression, except for --create      
                                           option. Put topic name in double     
                                           quotes and use the '\' prefix to     
                                           escape regular expression symbols; e.
                                           g. "test\.topic".                    
--topics-with-overrides                  if set when describing topics, only    
                                           show topics that have overridden     
                                           configs                              
--unavailable-partitions                 if set when describing topics, only    
                                           show partitions whose leader is not  
                                           available                            
--under-replicated-partitions            if set when describing topics, only    
                                           show under replicated partitions     
--zookeeper <String: hosts>              DEPRECATED, The connection string for  
                                           the zookeeper connection in the form 
                                           host:port. Multiple hosts can be     
                                           given to allow fail-over.
```

## Kafka setup

Lets update bash profile 
```cat ~/.bash_profile```
It will show you current bash profile. To update it we need file path
``` 
cd bin
pwd
```
copy the path of the bin and to update bash profile i am using nano editor

``` nano ~/.bash_profile```

Add export PATH="$PATH:/Users/rohithuppala/kafka_2.12-2.2.0/bin"

Now if open another window in terminal and type 'kafka-' and then TAB you can see suggestions

```
kafka-acls.sh                        kafka-preferred-replica-election.sh
kafka-broker-api-versions.sh         kafka-producer-perf-test.sh
kafka-configs.sh                     kafka-reassign-partitions.sh
kafka-console-consumer.sh            kafka-replica-verification.sh
kafka-console-producer.sh            kafka-run-class.sh
kafka-consumer-groups.sh             kafka-server-start.sh
kafka-consumer-perf-test.sh          kafka-server-stop.sh
kafka-delegation-tokens.sh           kafka-streams-application-reset.sh
kafka-delete-records.sh              kafka-topics.sh
kafka-dump-log.sh                    kafka-verifiable-consumer.sh
kafka-log-dirs.sh                    kafka-verifiable-producer.sh
kafka-mirror-maker.sh                
```

## Start Zookeper
To use Kafka we need zookeeper up and running

To start zookeeper
``` bin/zookeeper-server-start.sh config/zookeeper.properties```
If everything went well you will this message at the end
```2019-04-20 20:32:44,655] INFO binding to port 0.0.0.0/0.0.0.0:2181 (org.apache.zookeeper.server.NIOServerCnxnFactory)```

If you have 2181 port already binded you then you will get error. Make port 2181 free or you can change the port number from config file.
by ``` cat config/zookeeper.properties ```
Zookeeper has to uup and running all the time. 

## Start Kafka
Open another window 

```bin/kafka-start-server.sh config/server.properties```
If everything went well should see a message saying KafkaServer id=0 started


# Kafka Topics basics

## Create Topic
For each topic creation we need following information :
* Zookeeper running address (127.0.0.1:2181)
* topic name
* partitions number
* Replication factor (RF)

RF should always be less than or equal to number of brokers.
```kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 1```

## List all topics

To list all the existing topics
```kafka-topics.sh --zookeeper 127.0.0.1:@181 --list```
It will show all the created topics.

## Desscriber topic

To know the topic information
```kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --describe```
 This will show all the information abour the topic like leader broker, number of replications, configs.


 ## Delete topics 
````kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --delete```
delete.topic.enable is set to true by default.

# Producer
Now we creted topics, we need to send data to topic. To send data to topic we need producers.
















