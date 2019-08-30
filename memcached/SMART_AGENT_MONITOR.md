
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->

### INSTALLATION

This integration is part of the [SignalFx Smart Agent](https://github.com/signalfx/integrations/tree/master/signalfx-agent)[](sfx_link:signalfx-agent)
as the `collectd/memcached` monitor. You should first deploy the Smart Agent to the
same host as the service you want to monitor, and then continue with the
configuration instructions below.

<!--- GENERATED BY gomplate from scripts/docs/monitor-page.md.tmpl --->

# collectd/memcached

Monitor Type: `collectd/memcached` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/internal/monitors/collectd/memcached))

**Accepts Endpoints**: **Yes**

**Multiple Instances Allowed**: Yes


## Description

**This integration primarily consists of the Smart Agent monitor `collectd/memcached`.
Below is an overview of that monitor.**

### Smart Agent Monitor


Monitors an instance of memcached using the [collectd memcached
plugin](https://collectd.org/wiki/index.php/Plugin:memcached).  Requires
Memcached 1.1 or later.

The monitor collects the following information from Memcached nodes:

* request information (including hits, misses & evictions)
* current connections
* net input/output bytes
* number of items cached

Documentation for Memcached can be found at https://github.com/memcached/memcached/wiki.


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: collectd/memcached
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](https://github.com/signalfx/signalfx-agent/tree/master/docs/monitors/../monitor-config.md#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `host` | **yes** | `string` |  |
| `port` | **yes** | `integer` |  |
| `name` | no | `string` |  |
| `reportHost` | no | `bool` |  (**default:** `false`) |


## Metrics

These are the metrics available for this monitor.
Metrics that are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
(*default*) are ***in bold and italics*** in the list below.


 - `connections.opened` (*cumulative*)<br>    Number of connections opened since server began running
 - ***`df.cache.free`*** (*gauge*)<br>    Unused storage bytes
 - ***`df.cache.used`*** (*gauge*)<br>    Current number of bytes used to store items
 - `memcached_command.flush` (*cumulative*)<br>    Number of flush requests
 - ***`memcached_command.get`*** (*cumulative*)<br>    Number of retrieval requests
 - ***`memcached_command.set`*** (*cumulative*)<br>    Number of storage requests
 - `memcached_command.touch` (*cumulative*)<br>    Number of touch requests
 - ***`memcached_connections.current`*** (*gauge*)<br>    Current number of open connections
 - ***`memcached_items.current`*** (*gauge*)<br>    Current number of items stored by this instance
 - ***`memcached_octets.rx`*** (*cumulative*)<br>    Total network bytes read by this server
 - ***`memcached_octets.tx`*** (*cumulative*)<br>    Total network bytes written by this server
 - `memcached_ops.decr_hits` (*cumulative*)<br>    Number of successful Decr requests
 - `memcached_ops.decr_misses` (*cumulative*)<br>    Number of decr requests against missing keys
 - `memcached_ops.delete_hits` (*cumulative*)<br>    Number of successful delete requests
 - `memcached_ops.delete_misses` (*cumulative*)<br>    Number of delete requests against missing keys
 - ***`memcached_ops.evictions`*** (*cumulative*)<br>    Number of valid items removed from cache
 - ***`memcached_ops.hits`*** (*cumulative*)<br>    Number of keys that have been requested and found present
 - `memcached_ops.incr_hits` (*cumulative*)<br>    Number of successful incr requests
 - `memcached_ops.incr_misses` (*cumulative*)<br>    Number of incr requests against missing keys
 - ***`memcached_ops.misses`*** (*cumulative*)<br>    Number of items that have been requested and not found
 - `ps_count.threads` (*gauge*)<br>    Number of worker threads requested
 - `ps_cputime.syst` (*cumulative*)<br>    Total system time for this instance
 - `ps_cputime.user` (*cumulative*)<br>    Total user time for this instance
 - `total_events.listen_disabled` (*cumulative*)<br>    Number of times connection limit has been exceeded

### Non-default metrics (version 4.7.0+)

**The following information applies to the agent version 4.7.0+ that has
`enableBuiltInFiltering: true` set on the top level of the agent config.**

To emit metrics that are not _default_, you can add those metrics in the
generic monitor-level `extraMetrics` config option.  Metrics that are derived
from specific configuration options that do not appear in the above list of
metrics do not need to be added to `extraMetrics`.

To see a list of metrics that will be emitted you can run `agent-status
monitors` after configuring this monitor in a running agent instance.

### Legacy non-default metrics (version < 4.7.0)

**The following information only applies to agent version older than 4.7.0. If
you have a newer agent and have set `enableBuiltInFiltering: true` at the top
level of your agent config, see the section above. See upgrade instructions in
[Old-style whitelist filtering](https://github.com/signalfx/signalfx-agent/tree/master/docs/monitors/../legacy-filtering.md#old-style-whitelist-filtering).**

If you have a reference to the `whitelist.json` in your agent's top-level
`metricsToExclude` config option, and you want to emit metrics that are not in
that whitelist, then you need to add an item to the top-level
`metricsToInclude` config option to override that whitelist (see [Inclusion
filtering](https://github.com/signalfx/signalfx-agent/tree/master/docs/monitors/../legacy-filtering.md#inclusion-filtering).  Or you can just
copy the whitelist.json, modify it, and reference that in `metricsToExclude`.


