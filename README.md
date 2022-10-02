# Elastic Devolepment ( installation - Configration files )

## Elastic Dependencies.  

- Install  java OpenJDK using Yum Repositories  
```
sudo yum install java 
```

## Install and Start Elasticsearch
### Download Elasticsearch manual 
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.4.2-x86_64.rpm 
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.4.2-x86_64.rpm.sha512 
shasum -a 512 -c elasticsearch-8.4.2-x86_64.rpm.sha512  
```
- Can Move this file from local host to VM using scp command  

### Install Elasticsearch 
```
sudo rpm --install elasticsearch-8.4.2-x86_64.rpm 
```
### Start and enable Elasticsearch using systemctl command 
```
sudo systemctl start elasticsearch.service 
sudo systemctl enable elasticsearch.service 
```
### Elasticsearch configurations in yaml file  
```
vim /etc/elasticsearch/elasticsearch.yml 
```
- Iam Disable all security features because Iam not have SSL certificate  
- Can check in local VM using Browser or curl command 
```
curl http://localhost:9200 
```
---
## Install and Start  Kibana 
### Download Kibana manual  
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-8.4.2-x86_64.rpm 
shasum -a 512 kibana-8.4.2-x86_64.rpm 
```
- Can Move this file from local host to VM using scp command 
### Install Kibana  
```
sudo rpm --install kibana-8.4.2-x86_64.rpm 
```
### Start and enable Kibana using systemctl command 
```
sudo systemctl start kibana.service 
sudo systemctl enable kibana.service
```
### Kibana onfigurations in yaml file 
- Enable this line in file configuration  
```
vim /etc/kibana/kibana.yml 
``` 
- Can check in local VM using Browser 
```
http://localhost:5601 
``` 
### when enabled elasticsearch SSL security features (xpack)
- configuration of kibana requires the following
```
/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-	token -s kibana 
```
- copy the enrollment token and paste in the textbox opened on kibana webui and click configure kibana 
- thre is a verification which you will generate a verification code using  
```
/usr/share/kibana/bin/kibana-verification-code 
```
---
## Install and Start Logstash 
### Download Logstash manual  
- Follow this path and can choice rpm package  
```
https://www.elastic.co/downloads/logstash 
```
- can Move the package using scp or rsync command to VM  
```
sudo rpm --install logstash-8.4.2-x86_64.rpm 
```
### Start and enable Logstash using systemctl command 
```
sudo systemctl start logstash.service 
sudo systemctl enable logstash.service 
```
- create and using file to configure input, output, filtration to start pipeline for example (beats.conf)
```
/etc/logstash/conf.d/beats.conf
/usr/share/logstash/beats.conf
```
### Start pipeline using file was created 
```
/usr/share/logstash/bin/logstash -f beats.conf
```
---
## Install and Start filebeat 
### Download filebeat manual 
```
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.4.2-x86_64.rpm 
sudo rpm -vi filebeat-8.4.2-x86_64.rpm 
```
### Start and enable Logstash using systemctl command 
```
sudo systemctl enable filebeat.service
sudo systemctl start filebeat.service
```
## Some Screanshots 
- In kibana can make sure from pipeline filtration
![alt text](https://raw.githubusercontent.com/melgawad/ELK-Task/main/Screenshot%20from%202022-10-02%2011-37-27.png)
---
- In elasticearch can make sure from configrytions
![alt text](https://raw.githubusercontent.com/melgawad/ELK-Task/main/Screenshot%20from%202022-10-02%2011-38-56.png)
---
- After Logstash config file to create pipeline can make sure from the service and pipeline is started
![alt text](https://raw.githubusercontent.com/melgawad/ELK-Task/main/Screenshot%20from%202022-10-02%2011-40-14.png)
---
## Finally, I wish you good luck
