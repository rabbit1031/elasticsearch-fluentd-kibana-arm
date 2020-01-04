# elasticsearch-fluentd-kibana-arm
Elasticsearch-Fluentd-Kibana stack for ARM architecture

## make volumes

```
$ docker volume create elasticsearch-data
$ docker run -it --rm -v elasticsearch-data:/es-data alpine
# chown 1000:1000 /es-data

$ docker volume create elasticsearch-logs
$ docker run -it --rm -v elasticsearch-logs:/es-logs alpine
# chown 1000:1000 /es-logs
```