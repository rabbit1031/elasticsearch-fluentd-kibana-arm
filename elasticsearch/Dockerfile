# If you need to build the image for 32-bit arm processors,
# using the arm32v7 base-image instead of the arm64v8 one.
FROM arm64v8/openjdk:11-slim
# FROM arm32v7/openjdk:11-slim

# Choose the distribution licensed under the Elastic license or the Apache 2.0 license:
#
# Elastic License: https://github.com/elastic/elasticsearch/blob/7.5/licenses/ELASTIC-LICENSE.txt
# Apache 2.0 License: http://www.apache.org/licenses/LICENSE-2.0.txt
ARG ES_DIST="elasticsearch"
# ARG ES_DIST="elasticsearch-oss"

ARG ES_VERSION="7.6.2"

EXPOSE 9200

WORKDIR /usr/src

RUN set -x && \
  apt-get update && \
  apt-get install -y --no-install-recommends wget && \
  wget -q https://artifacts.elastic.co/downloads/elasticsearch/${ES_DIST}-${ES_VERSION}-no-jdk-linux-x86_64.tar.gz && \
  wget -q https://artifacts.elastic.co/downloads/elasticsearch/${ES_DIST}-${ES_VERSION}-no-jdk-linux-x86_64.tar.gz.sha512 && \
  sha512sum -c ${ES_DIST}-${ES_VERSION}-no-jdk-linux-x86_64.tar.gz.sha512 && \
  tar xzf ${ES_DIST}-${ES_VERSION}-no-jdk-linux-x86_64.tar.gz && \
  rm -rf elasticsearch-*.tar.gz* && \
  rm -rf /var/lib/apt/lists/* && \
  mv elasticsearch-${ES_VERSION} elasticsearch

COPY elasticsearch.yml elasticsearch/config/elasticsearch.yml
COPY jvm.options elasticsearch/config/jvm.options

RUN set -x && \
  groupadd --system elasticsearch && \
  useradd --system elasticsearch -g elasticsearch && \
  chown -R elasticsearch:elasticsearch /usr/src/elasticsearch

USER elasticsearch

ENTRYPOINT ["./elasticsearch/bin/elasticsearch"]
