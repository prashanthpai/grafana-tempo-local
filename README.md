## Grafana Tempo Local

Run [Grafana Tempo](https://grafana.com/oss/tempo/) locally for testing
integration with your app.

For more extensive examples, see: https://github.com/grafana/tempo/tree/main/example

### Start Grafana and Tempo

```console
docker-compose up -d
```

```console
docker-compose ps
```
```
NAME      IMAGE                    COMMAND                                 SERVICE   CREATED         STATUS         PORTS
grafana   grafana/grafana:10.1.1   "/run.sh"                               grafana   8 seconds ago   Up 7 seconds   0.0.0.0:3000->3000/tcp
tempo     grafana/tempo:latest     "/tempo -config.file=/etc/tempo.yaml"   tempo     8 seconds ago   Up 7 seconds   0.0.0.0:3200->3200/tcp, 0.0.0.0:4317->4317/tcp
```

All data is stored locally in the `tempo-data` directory.

### Integrate with your app

1. Add code instrumentation.
1. Export traces to `localhost:4317` via OTEL grpc exporter.
   Ref: https://pkg.go.dev/go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracegrpc
1. Perform operations that exercise required the code path.

### View Traces

Navigate to [Grafana](http://localhost:3000/explore), select the Tempo data
source and use the "Search" tab to find traces.

### Stop

```console
docker-compose down -v
```
