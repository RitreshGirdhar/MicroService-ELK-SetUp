FROM docker.elastic.co/logstash/logstash:7.4.2

RUN rm -f /usr/share/logstash/pipeline/logstash.conf
RUN rm -f /usr/share/logstash/config/logstash.yml

COPY pipeline /usr/share/logstash/pipeline/
COPY config /usr/share/logstash/config/
