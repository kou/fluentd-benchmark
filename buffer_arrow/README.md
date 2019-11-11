# Fluentd benchmark - buffer_arrow

This benchmarks following architecture scenario:

```
  Agent Node
  +----------------------------------------+
  | +-----------+      +-----------------+ |
  | |           |      |                 | |
  | | Log File  +----->|  Fluentd        | |
  | |           |      |                 | |
  | +-----------+  in_tail -- out_file --+ |
  |                              +         |
  |                        buffer_arrow    |
  +----------------------------------------+
```

## Setup Fluentd Agent

Assume ruby and Red Parquet are installed.

```
git clone https://github.com/fluent/fluentd-benchmark
cd fluentd-benchmark/buffer_arrow
bundle
bundle exec fluentd -c agent.conf
```

## Run benchmark tool and measure

Run at Fluentd agent server.

This tool outputs logs to `dummy.log`, and Fluentd agent reads it and sends data to a receiver. 

```
cd fluentd-benchmark/buffer_arrow
bundle exec dummer -c dummer.conf
```

You may increase the rate (messages/sec) of log generation by -r option to benchmark. 

```
bundle exec dummer -c dummer.conf -r 100000
```

You should see an output on Fluentd receiver as followings. This tells you the performance of fluentd processing. 

```
2014-02-20 17:20:55 +0900 [info]: plugin:out_flowcounter_simple count:500       indicator:num   unit:second
2014-02-20 17:20:56 +0900 [info]: plugin:out_flowcounter_simple count:500       indicator:num   unit:second
2014-02-20 17:20:57 +0900 [info]: plugin:out_flowcounter_simple count:500       indicator:num   unit:second
```

You may use `iostat -dkxt 1`, `vmstat 1`, `top -c`, `free`, or `dstat` commands to measure system resources. 

## Sample Result

TODO
