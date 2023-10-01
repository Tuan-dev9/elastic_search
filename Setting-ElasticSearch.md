# Elasticsearch with Spring boot

## Setting up

### Spring boot Dependencies

- Spring boot web
- Spring data elasticsearch

### Maven project identifiers

https://www.baeldung.com/maven#:%7E:text=Maven%20uses%20a%20set%20of,a%20version%20of%20the%20project

1. groupId - a unique base name of the company or group that created the project
2. artifactId - a unique name of the project
3. version – a version of the project
4. packaging – a packaging method (e.g. WAR/JAR/ZIP)

### Docker Elasticsearch
**docker-compose.yml**

```
version: "3.0"
services:
  elasticsearch:
    container_name: es-container
    image: docker.elastic.co/elasticsearch/elasticsearch:7.11.0
    environment:
      - xpack.security.enabled=false
      - "discovery.type=single-node"
    networks:
      - es-net
    ports:
      - 9200:9200
  kibana:
    container_name: kb-container
    image: docker.elastic.co/kibana/kibana:7.11.0
    environment:
      - ELASTICSEARCH_HOSTS=http://es-container:9200
    networks:
      - es-net
    depends_on:
      - elasticsearch
    ports:
      - 5601:5601
networks:
  es-net:
    driver: bridge
```
**Note**
```
"discovery.type=single-node" // Run a single-node cluster
```

