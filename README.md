# RabbitMQ Test Cluster
My test setup for trying out various things using tools like [rabbitmq-perf-test](https://github.com/rabbitmq/rabbitmq-perf-test)

## Components
This setup consists out of the following components

* rabbitmq, version 3.13.6-management
* grafana, version 11.4.0
* prometheus, version v3.0.1
* haproxy, version 3.1.0

### RabbitMQ
**Web UI:** http://localhost:15672 \
**Metrics:** http://localhost:15692/metrics

**Username:** guest \
**Password:** guest

#### Network
It defines `rabbitmq-cluster` as an alias to the rabbitmq network, making e.g. `amqp://rabbitmq-cluster` available for a container on same network.

**Example using perf-test**
```
docker run -it --rm --network rabbitmq-test-cluster_rabbitmq pivotalrabbitmq/perf-test:latest -x 1 -y 2 -u "throughput-test-1" -a -q 100 --rate 500 --id "test 1" --uri amqp://rabbitmq-cluster
```

### Grafana
**Web UI:** http://localhost:3000

**Username:** admin \
**Password:** admin

### Prometheus
**Web UI:** http://localhost:9090

## Dashboards
The setup will bootstrap the following dashbords:

* [RabbitMQ - Overview](https://grafana.com/grafana/dashboards/10991-rabbitmq-overview/)
* [RabbitMQ - PerfTest](https://grafana.com/grafana/dashboards/6566-rabbitmq-perftest/)
* [RabbitMQ - Quorum Queues Raft](https://grafana.com/grafana/dashboards/11340-rabbitmq-quorum-queues-raft/)
* [RabbitMQ - Stream](https://grafana.com/grafana/dashboards/14798-rabbitmq-stream/)