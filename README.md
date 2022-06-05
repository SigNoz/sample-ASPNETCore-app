# sample-ASPNETCore-app

Sample ASPNetCore app with opentelemetry instrumentation

> Visit [Signoz install guide](https://signoz.io/docs/install/docker/)

### To build

```
dotnet build
```

### To run

```
dotnet run
```

> Ensure to change IP of SigNoz in appsettings.json

<hr/>

## Steps to use via `Docker`

### Build Image

```
docker build . -t example-signoz
```

### Create Network

```
docker network create signoz-network
```

### Add Signoz Collector to the network

```
docker network connect signoz-network clickhouse-setup_otel-collector_1
```

### Add Example App to the same network

```
docker run -d --name example-signoz \
    --network="signoz-network" \
    -p 5001:80 \
    -e Otlp__Endpoint="http://clickhouse-setup_otel-collector_1:4317" \
    example-signoz
```
