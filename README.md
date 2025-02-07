# Prometheus.io Process Collector
[![Hex.pm](https://img.shields.io/hexpm/v/prometheus_process_collector.svg?maxAge=2592000?style=plastic)](https://hex.pm/packages/prometheus_process_collector)
[![Hex.pm](https://img.shields.io/hexpm/dt/prometheus_process_collector.svg?maxAge=2592000)](https://hex.pm/packages/prometheus_process_collector)
[![Hex
Docs](https://img.shields.io/badge/hex-docs-lightgreen.svg)](https://hexdocs.pm/prometheus_process_collector/)
[![GitHub Actions](https://github.com/prometheus-erl/prometheus_process_collector/actions/workflows/ci.yml/badge.svg)](https://github.com/prometheus-erl/prometheus_process_collector/actions/workflows/ci.yml)
[![Codecov](https://codecov.io/github/prometheus-erl/prometheus_process_collector/graph/badge.svg?token=G9HB5UKNIY)](https://codecov.io/github/prometheus-erl/prometheus_process_collector)


Collector which exports the current state of process metrics including cpu, memory, file descriptor usage and native threads count as well as the process start and up times.

- FreeBSD;
- Linux - uses /proc;
- MacOS X (expiremental).

## Installation

**Hex package note**: Because OTP strictly validates NIF version c_src was compiled with, I removed precompiled binaries from the Hex package. This means that OTP source code is needed to build this library.

Also collector needs to be registered (for example in default registry):

```erlang
prometheus_registry:register_collector(prometheus_process_collector)
```

```elixir
require Prometheus.Registry
Prometheus.Registry.register_collector(:prometheus_process_collector)
```

## Example scrape:

```
# TYPE process_open_fds gauge
# HELP process_open_fds Number of open file descriptors.
process_open_fds 13
# TYPE process_max_fds gauge
# HELP process_max_fds Maximum number of open file descriptors.
process_max_fds 20000
# TYPE process_start_time_seconds gauge
# HELP process_start_time_seconds Start time of the process since unix epoch in seconds.
process_start_time_seconds 1508230997
# TYPE process_uptime_seconds counter
# HELP process_uptime_seconds Process uptime in seconds.
process_uptime_seconds 76
# TYPE process_threads_total gauge
# HELP process_threads_total Process Threads count.
process_threads_total 22
# TYPE process_virtual_memory_bytes gauge
# HELP process_virtual_memory_bytes Virtual memory size in bytes.
process_virtual_memory_bytes 3015249920
# TYPE process_resident_memory_bytes gauge
# HELP process_resident_memory_bytes Resident memory size in bytes.
process_resident_memory_bytes 1224400
# TYPE process_cpu_seconds_total counter
# HELP process_cpu_seconds_total Process CPU seconds total.
process_cpu_seconds_total{kind="utime"} 0.768
process_cpu_seconds_total{kind="stime"} 0.368
# TYPE process_max_resident_memory_bytes gauge
# HELP process_max_resident_memory_bytes Maximum resident set size used.
process_max_resident_memory_bytes 50192384
# TYPE process_noio_pagefaults_total counter
# HELP process_noio_pagefaults_total Number of page faules serviced without any I/O activity.
process_noio_pagefaults_total 16015
# TYPE process_io_pagefaults_total counter
# HELP process_io_pagefaults_total Number of page faults serviced that required I/O activity.
process_io_pagefaults_total 0
# TYPE process_swaps_total counter
# HELP process_swaps_total Number of times a process was "swapped" out of main memory.
process_swaps_total 0
# TYPE process_disk_reads_total counter
# HELP process_disk_reads_total Number of times the file system had to perform input.
process_disk_reads_total 0
# TYPE process_disk_writes_total counter
# HELP process_disk_writes_total Number of times the file system had to perform output.
process_disk_writes_total 80
# TYPE process_signals_delivered_total counter
# HELP process_signals_delivered_total Number of signals delivered.
process_signals_delivered_total 0
# TYPE process_voluntary_context_switches_total counter
# HELP process_voluntary_context_switches_total Number of times a context switch resulted due to a process voluntarily giving up the processor.
process_voluntary_context_switches_total 1131
# TYPE process_involuntary_context_switches_total counter
# HELP process_involuntary_context_switches_total Number of times a context switch resulted due to a higher priority process becoming runnable or because the current process exceeded its time slice.
process_involuntary_context_switches_total 208
```

Usage
-----

You can register this collector manually using `prometheus_process_collector/0,1` or use `default_collectors` env entry for `prometheus`.

With [Prometheus Plugs](https://github.com/prometheus-erl/prometheus-plugs) - just add prometheus_process_collector dependency to top-level project (i.e. [like here](https://github.com/prometheus-erl/prometheus-plugs-example/edit/master/mix.exs)).

## Integrations / Collectors / Instrumenters
 - [Ecto collector](https://github.com/prometheus-erl/prometheus-ecto)
 - [Plugs Instrumenter/Exporter](https://github.com/prometheus-erl/prometheus-plugs)
 - [Elli middleware](https://github.com/elli-lib/elli_prometheus)
 - [Fuse plugin](https://github.com/jlouis/fuse#fuse_stats_prometheus)
 - [Phoenix instrumenter](https://github.com/prometheus-erl/prometheus-phoenix)
 - [Process Info Collector](https://github.com/prometheus-erl/prometheus_process_collector)
 - [Prometheus.erl](https://github.com/prometheus-erl/prometheus.erl)
 - [Prometheus.ex](https://github.com/prometheus-erl/prometheus.ex)
 - [RabbitMQ Exporter](https://github.com/prometheus-erl/prometheus_rabbitmq_exporter)

License
-----

FreeBSD-specific part uses copy-modified code from standard utils (limits and procstat) or standard API in some places.

MIT
