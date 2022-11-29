# envoy-otel-example

This repository will be used to transfer Envoy's Trace information to New Relic.

The code base is based on envoy's [example](https://github.com/envoyproxy/envoy/tree/main/examples/opentelemetry).

## Setup

Get New Relic [LicenseKey](https://one.newrelic.com/launcher/api-keys-ui.launcher)

### Replace api-key header value

```yaml
# otel-collector-config.yaml

exporters:
  otlp:
    endpoint: "https://otlp.nr-data.net:4317" #US endpoint
    headers:
      api-key: "<set your license key>"　→ your key

```

### Run
```shell
 docker compose up --build
```

## Make Request 

### request to service 1

This will be routed via 2 of the Envoy proxies:

- front-proxy

- envoy-1

```shell
curl localhost:10000/trace/1
```

### request to service 2

This will be routed via all 3 of the Envoy proxies:

- front-proxy

- envoy-1

- envoy-2

```shell
curl localhost:10000/trace/2
```

## Check New Relic UI

<img width="1305" alt="Screen Shot 2022-11-28 at 14 42 35" src="https://user-images.githubusercontent.com/39491874/204202667-d7f4bb4c-c64f-4922-881a-d005c05a9d36.png">
