This plugin allows having multiple Gerrit masters to be deployed across
various sites without having to share any storage. The alignment between
the masters happens using the replication plugin and Kafka as an external
message broker.

This plugin allows Gerrit to publish and to consume events over a Kafka
message broker for aligning with the other masters over different sites.

## Setup

Prerequisites:

* Kafka message broker deployed in a multi-master setup across all the sites

For the masters:

* Install and configure @PLUGIN@ plugin

Here is an example of minimal @PLUGIN@.config:

For all the masters on all the sites:

```
[kafka]
  bootstrapServers = kafka-1:9092,kafka-2:9092,kafka-3:9092
  eventTopic = gerrit_index

[kafka "publisher"]
  enable = true
  indexEventTopic = gerrit_index
  streamEventTopic = gerrit_stream
  cacheEvictionEventTopic = gerrit_cache_eviction

[kafka "subscriber"]
  enable = true
  pollingIntervalMs = 1000
  autoCommitIntervalMs = 1000
```


For further information and supported options, refer to [config](config.md)
documentation.
