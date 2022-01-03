# Mux Middleware Prometheus

This Library provides a middleware for the mux router

## Metrics

```

http_requests_total{path={path}}
http_response_status{path="{path}",status="{statusCode}"}
http_response_time_seconds_bucket{path="{path}",le="0.005"}

```

## Example

```go
package main

import (
    "net/http"

    "github.com/gorilla/mux"
    "github.com/hendrikhuels/mux_middleware_prometheus"
    "github.com/prometheus/client_golang/prometheus/promhttp"
)

func main {
    router := mux.NewRouter()
    router.Use(mux_middleware_prometheus.PrometheusMiddleware)
    router.Path("/metrics").Handler(promhttp.Handler())
    http.ListenAndServe("0.0.0.0:8080", router)
}
```
