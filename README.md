# Welcome to Vostok

_A complete microservice toolkit for .NET developers._

Vostok has everything .NET developers need to create distributed systems. It enables intra-cluster interaction between microservices and collects their logs, metrics, and distributes traces out of the box. Vostok-enabled microservices are compatible with .NET Standard 2.0.

### How it works {#how-it-works}

Vostok provides instrumentation for microservices and a number of Vostok infrastructure components. Instrumentation is required to collect data which is necessary for any production-ready distributed system:

* logs for application lifecycle
* metrics for resource usage
* traces for intra-cluster interaction

Every Vostok-instrumented microservice collects described data out of the box. No additional confuguration or code is required.

Applications would use provided interfaces to write custom logs and metrics. Any outgoing requests via provided [Cluster Client](https://github.com/vostok/core/tree/master/Vostok.ClusterClient) would be included to collected distributed traces. These include requests to Vostok-instrumented applications \(e.g., other microservices\) and non-instrumented applications \(e.g., databases or external APIs\).

![](http://vostok.tools/blueprint.png)

Microservices send all logs, metrics, and traces via their [Airlock Clients](https://github.com/vostok/core/tree/master/Vostok.Airlock.Client) to the [Airlock Gate](https://github.com/vostok/airlock.gate). This [ridiculuosly performant](https://github.com/vostok/core/issues/3) service puts received events to Apache Kafka. A swarm of [Airlock Consumers](https://github.com/vostok/airlock.consumer) read and process events from Kafka.

Events are either transformed and put back to Kafka, or transferred to backends:

* _Logs_ consumer transfers logs to Elasticsearch
* _Metrics Aggregator_ calculates aggregated metrics and puts them to Kafka
* _Metrics_ consumer transfers metrics to Graphite
* _Traces_ consumer transfers traces to Cassandra

Backends store the data and feed it to end-user applications. Developers use them to monitor the distributed system as a whole:

* view and search logs in Kibana
* view and plot metrics in Grafana
* view and explore traces in [Contrails](https://github.com/vostok/contrails.web)

### Features {#features}

**Feature complete.** Vostok has everything to create, monitor and troubleshoot microservices. No other tools or libraries are required.

**Sanely pre-configured.** Vostok has a ready to use template for an ASP.NET Core 2.0 application as well as Docker files for Vostok infrastructure components. Zero configuration is required to get started.

**Fast by design.** Vostok is benchmarked and optimized for performance and throughput. No expensive hardware is required. Commodity servers are just fine for Vostok.

### Getting started with Vostok {#getting-started-with-vostok}

You can easily create and run your first Vostok-enabled application:

* Install and run [Spaceport](https://github.com/vostok/spaceport#spaceport), a single-host bundle with all Vostok components.
* Install and use [Launchpad](https://github.com/vostok/launchpad#launchpad) to create a Vostok-instrumented application from a template.
* Make some HTTP requests to that application and explore results in Grafana, Kibana and Contrails.

