# monitoring

Стек мониторинга на базе Prometheus и Grafana для сбора метрик хоста ALT Linux.

## Стек

- **Prometheus** — сбор и хранение метрик
- **Node Exporter** — метрики ОС (CPU, память, диск, сеть)
- **Grafana** — визуализация

## Архитектура

Node Exporter (localhost:9100)
↓ scrape
Prometheus (localhost:9090)
↓ datasource
Grafana (localhost:3000)

## Дашборды

Создан дашборд Node Metrics с панелями:

    CPU Usage: 100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

    Memory Usage: 100 * (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes))

    Disk Usage (root): 100 - ((node_filesystem_avail_bytes{mountpoint="/"} * 100) / node_filesystem_size_bytes{mountpoint="/"})

    Load Average: node_load1

## Особенности

    На ALT Linux проброс портов через -p не работает — используется network_mode: host.

    Конфигурация Prometheus хранится в prometheus.yml.

## Автор

Егор Кузнецов
