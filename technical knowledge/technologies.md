- [ ] mongodb
	-   Used as our general purpose storage for most of our data
	-   Access via either PyMongo or Mongoengine (ORM)
	-   Example Data: Configuration, Security Events, Incidents, System Components registry, Orchestration Assets (and physical assets)
- [ ] elasticsearch
	-   Used mainly for data that requires lots of aggregations and searches
	-   Some data is duplicated in both MongoDB and Elasticsearch (mainly Incident data) - this mostly used to support UI filter options for Incidents
	-   We use it for some free text search (minor use case for us)
	-   Example Data: Network Events, Reveal Data (Graph), Incidents
- [ ] [redis](https://redis.io/)
	- Used for 2 main use-cases - caching and buffering messages
	- As mentioned above, our Redis servers are cluster-managed and can thus run on slaves and are being monitored automatically
	- Example Data: Alive Agents events buffer, Reveal Matcher cache and much more
	- Redis is used as a local cache in a number of layers among GuardiCore applications. It is frequently used as an expirable cache that allows key-value questions.
- [ ] influxdb
	-   A database mostly used for our statistics and metrics operations
	-   The Grafana server is the consumer for this data - it polls it and visualizes using the Grafana UI
	-   Example Data: statsd metrics
- [ ] [rabbitmq](http://www.rabbitmq.com/getstarted.html)
	- Rabbitmq is used as messaging layer between Guardicore management application and the different Guardicore components (used for both RPC and as work queue)
- [ ] [zookeeper](http://zookeeper.apache.org/doc/current/zookeeperOver.html)
	- Zookeeper is used as synchronization framework between distributed Guardicore components - to perform tasks such role elections (some functions should be executed on single component - with the constraint that exactly one component should execute them at a time, and if the component runs them fails from any reason, other will take its place). Also it is prerequisite for running kafka
- [ ] [kafka](http://cloudurable.com/blog/what-is-kafka/index.html)
	- Kafka is used to synchronize distributed log. Different Guardicore components write events to it kafka topic, which later consumed by others to create distributed state machine which allow different distributed components to decide the same decisions based on the recent content of the events stream.
- [ ] [haproxy](http://cbonte.github.io/haproxy-dconv/1.7/intro.html#3)
	- Haproxy is used in multiple ways in Guardicore application. Among those usages, load balancer, ssl termination server, SNI proxy server, and SSL proxy.
- [ ] [management](https://guardicore.atlassian.net/wiki/spaces/MGMT/pages/129237000/The+Management)
- [ ] [containers](https://docs.docker.com/get-started/#recap-and-cheat-sheet)
- [ ] certificates
- [ ] pki