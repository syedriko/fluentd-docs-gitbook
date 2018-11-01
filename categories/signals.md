Fluentd's Signal Handling
=========================

This article explains how `Fluentd` handles UNIX signals.

[]{#process-model}

::: {#table-of-contents .section}
### Table of Contents

[Process Model](#process-model)

[Signals](#signals)

-   [SIGINT or SIGTERM](#sigint-or-sigterm)
-   [SIGUSR1](#sigusr1)
-   [SIGHUP](#sighup)
-   [SIGCONT](#sigcont)
:::

Process Model
-------------

When you launch Fluentd, it creates two processes: supervisor and
worker. The supervisor process controls the life cycle of the worker
process. Please make sure to send any signals to the supervisor process.

[]{#signals}

Signals
-------

[]{#sigint-or-sigterm}

### SIGINT or SIGTERM

Stops the daemon gracefully. Fluentd will try to flush the entire memory
buffer at once, but will not retry if the flush fails. Fluentd will not
flush the file buffer; the logs are persisted on the disk by default.

[]{#sigusr1}

### SIGUSR1

Forces the buffered messages to be flushed and reopens Fluentd's log.
Fluentd will try to flush the current buffer (both memory and file)
immediately, and keep flushing at `flush_interval`.

[]{#sighup}

### SIGHUP

Reloads the configuration file by gracefully restarting the worker
process. Fluentd will try to flush the entire memory buffer at once, but
will not retry if the flush fails. Fluentd will not flush the file
buffer; the logs are persisted on the disk by default.

[]{#sigcont}

### SIGCONT

Call sigdump to dump fluentd internal status. See
[trouble-shooting](trouble-shooting#dump-fluentd-internal-information)
article.

::: {style="text-align:right"}
Last updated: 2016-06-06 04:47:13 UTC
:::

------------------------------------------------------------------------

::: {style="text-align:right"}
Versions \| [v1.0 (td-agent3)](/v1.0/articles/signals) \| ***v0.12*
(td-agent2) **
:::

------------------------------------------------------------------------

If this article is incorrect or outdated, or omits critical information,
please [let us
know](https://github.com/fluent/fluentd-docs/issues?state=open).
[Fluentd](http://www.fluentd.org/) is a open source project under [Cloud
Native Computing Foundation (CNCF)](https://cncf.io/). All components
are available under the Apache 2 License.