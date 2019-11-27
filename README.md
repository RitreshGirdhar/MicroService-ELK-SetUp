# MicroService-ELK-SetUp

Idea of this POC is to help you in setting your ELK docker set up and run custom Filebeat docker image which will read your Microservices Logs and push to ELK stack.


Let's start elastic search
```
docker run -d --name "elasticsearch" -p 9200:9200 -p 9300:9300 --volume="/app/elasticsearch/data/:/usr/share/elasticsearch/data/" --volume="/var/run/docker.sock:/var/run/docker.sock:ro" -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.4.2
```

Now start kibana and link with elastic search docker
```
docker run --name "kibana" --link "elasticsearch:elasticsearch" -p 5601:5601  --volume="/var/run/docker.sock:/var/run/docker.sock:ro" docker.elastic.co/kibana/kibana:7.4.2
```

Finally start logstash.
```
docker run --name "logstash" -p 5044:5044 --link "elasticsearch:elasticsearch" --volume="/var/run/docker.sock:/var/run/docker.sock:ro" -v "/app/elasticsearch/logstash-logs/:/datalog/" logstash
```

Here we are mounting "/app/elasticsearch/logstash-logs/" volume. Here we could see the logs captured by logstash.

