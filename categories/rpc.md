Fluentd's HTTP RPC
==================

This article explains how `Fluentd` handles HTTP RPC.

[]{#overview}

::: {#table-of-contents .section}
### Table of Contents

[Overview](#overview)

[Configuration](#configuration)

[RPCs](#rpcs)

-   [/api/processes.interruptWorkers](#/api/processes.interruptworkers)
-   [/api/processes.killWorkers](#/api/processes.killworkers)
-   [/api/plugins.flushBuffers](#/api/plugins.flushbuffers)
-   [/api/config.reload](#/api/config.reload)
:::

Overview
--------

HTTP RPC is one way of managing fluentd instance. Several provided RPCs
are replacement of [signals](signals). The response body is JSON format.

On signal unsupported environment, e.g. Windows, you can use RPC instead
of signals.

[]{#configuration}

Configuration
-------------

RPC is off by default. If you want to enable RPC, set `rpc_endpoint` in
`<system>` section.

``` {.CodeRay}
<system>
  rpc_endpoint 127.0.0.1:24444
</system>
```

After that, you can access to RPC like below.

``` {.CodeRay}
$ curl http://127.0.0.1:24444/api/plugins.flushBuffers
{"ok":true}
```

[]{#rpcs}

RPCs
----

[]{#/api/processes.interruptworkers}

### /api/processes.interruptWorkers

Replacement of signal's [SIGINT](signals#sigint-or-sigterm). Stop the
daemon.

[]{#/api/processes.killworkers}

### /api/processes.killWorkers

Replacement of signal's [SIGTERM](signals#sigint-or-sigterm). Stop the
daemon.

[]{#/api/plugins.flushbuffers}

### /api/plugins.flushBuffers

Replacement of signal's [SIGUSR1](signals#sigusr1). Flushes buffered
messages.

[]{#/api/config.reload}

### /api/config.reload

Replacement of signal's [SIGHUP](signals#sighup). reload configuration.

::: {style="text-align:right"}
Last updated: 2016-03-01 13:42:40 UTC
:::

------------------------------------------------------------------------

::: {style="text-align:right"}
Versions \| [v1.0 (td-agent3)](/v1.0/articles/rpc) \| ***v0.12*
(td-agent2) **
:::

------------------------------------------------------------------------

If this article is incorrect or outdated, or omits critical information,
please [let us
know](https://github.com/fluent/fluentd-docs/issues?state=open).
[Fluentd](http://www.fluentd.org/) is a open source project under [Cloud
Native Computing Foundation (CNCF)](https://cncf.io/). All components
are available under the Apache 2 License.