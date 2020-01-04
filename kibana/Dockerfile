# Set the Node.js version required by Kibana:
# See: https://github.com/elastic/kibana/blob/7.6/package.json
ARG NODE_VERSION="10.19.0"

FROM node:${NODE_VERSION}-alpine

EXPOSE 5601

# Choose the distribution licensed under the Elastic license or the Apache 2.0 license:
#
# Elastic License: https://github.com/elastic/kibana/blob/7.6/licenses/ELASTIC-LICENSE.txt
# Apache 2.0 License: http://www.apache.org/licenses/LICENSE-2.0.txt
ARG KIBANA_DIST="kibana"
# ARG KIBANA_DIST="kibana-oss"

ARG KIBANA_VERSION="7.6.2"

WORKDIR /usr/src

RUN set -x && \
  wget -q https://artifacts.elastic.co/downloads/kibana/${KIBANA_DIST}-${KIBANA_VERSION}-linux-x86_64.tar.gz && \
  wget -q https://artifacts.elastic.co/downloads/kibana/${KIBANA_DIST}-${KIBANA_VERSION}-linux-x86_64.tar.gz.sha512 && \
  sha512sum -c ${KIBANA_DIST}-${KIBANA_VERSION}-linux-x86_64.tar.gz.sha512 && \
  tar xzf ${KIBANA_DIST}-${KIBANA_VERSION}-linux-x86_64.tar.gz && \
  rm -rf ${KIBANA_DIST}-${KIBANA_VERSION}-linux-x86_64.tar.gz* && \
  mv kibana-${KIBANA_VERSION}-linux-x86_64 kibana && \
  rm -f kibana/node/bin/node && \
  ln -sf /usr/local/bin/node kibana/node/bin/node

COPY kibana.yml /usr/src/kibana/config/kibana.yml

RUN set -x && \
  addgroup --system kibana && \
  adduser --system kibana -g kibana && \
  chown -R kibana:kibana /usr/src/kibana

USER kibana

ENTRYPOINT ["./kibana/bin/kibana"]
