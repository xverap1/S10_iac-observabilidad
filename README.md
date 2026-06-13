# S10_iac-observabilidad
Laboratorio de monitoreo con Grafana, Prometheus y Loki.

## Levantar el stack

```bash
docker compose up -d --build
```

## Notas de compatibilidad con Codespaces

`node-exporter` requiere `pid: host`, incompatible con Codespaces. Se comentó del stack. Los paneles de CPU del host muestran "No data" por esta limitación.

## Reset

```bash
docker compose down -v
```