FROM fluentd:latest

USER root

RUN fluent-gem install fluent-plugin-elasticsearch

USER fluent

COPY fluent.conf /fluentd/etc/fluent.conf