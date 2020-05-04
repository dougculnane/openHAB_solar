# Grafana Server

## Build

```bash
docker build -t ash-grafana .
```

## Install Panels.

```bash
docker exec ash-grafana grafana-cli plugins install grafana-piechart-panel
```


## Run

```bash
docker run -d --name ash-grafana \
  --restart always \
  --network="ash-net" \
  ash-grafana
```
