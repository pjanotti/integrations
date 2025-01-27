
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->
<!--- GENERATED BY gomplate from scripts/docs/templates/monitor-page.md.tmpl --->

# filesystems

Monitor Type: `filesystems` ([Source](https://github.com/signalfx/signalfx-agent/tree/main/pkg/monitors/filesystems))

**Accepts Endpoints**: No

**Multiple Instances Allowed**: Yes

## Overview

This monitor reports metrics about free disk space on mounted devices.

On Linux hosts, this monitor relies on the `/proc` filesystem.
If the underlying host's `/proc` file system is mounted somewhere other than
/proc please specify the path using the top level configuration `procPath`.

```yaml
procPath: /hostfs/proc
monitors:
 - type: filesystems
   hostFSPath: /hostfs
```

## Migrating from collectd/df
The `collectd/df` monitor is being deprecated in favor of the `filesystems`
monitor.  While the `collectd/df` monitor will still be available in
5.0, it is recommended that you switch to the `filesystems` monitor soon
after upgrading.  There are a few incompatibilities to be aware of between
the two monitors:

 - `collectd/df` used a dimension called `plugin_instance` to identify the
   mount point or device of the filesystem.  This dimension is completely
   removed in the `filesystems` monitor and replaced by the `mountpoint`
   and `device` dimensions.  You no longer have to select between the two
   (the `reportByDevice` option on `collectd/df`) as both are always
   reported.

 - The mountpoints in the `plugin_instance` dimension of `collectd/df`
   were reported with `-` instead of the more conventional `/` separated
   path segments.  The `filesystems` monitor always reports mountpoints in
   the `mountpoint` dimension and uses the conventional `/` separator.

 - The `collectd/df` plugin set a dimension `plugin: df` on all datapoints,
   but `filesystems` has no such comparable dimension.


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: filesystems
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](../monitor-config.html#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `hostFSPath` | no | `string` | Path to the root of the host filesystem.  Useful when running in a container and the host filesystem is mounted in some subdirectory under /.  The disk usage metrics emitted will be based at this path. |
| `fsTypes` | no | `list of strings` | The filesystem types to include/exclude.  This is an [overridable set](https://docs.splunk.com/observability/gdi/smart-agent/smart-agent-resources.html#filtering-data-using-the-smart-agent). If this is not set, the default value is the set of all **non-logical/virtual filesystems** on the system.  On Linux this list is determined by reading the `/proc/filesystems` file and choosing the filesystems that do not have the `nodev` modifier. |
| `mountPoints` | no | `list of strings` | The mount paths to include/exclude. This is an [overridable set](https://docs.splunk.com/observability/gdi/smart-agent/smart-agent-resources.html#filtering-data-using-the-smart-agent). NOTE: If you are using the hostFSPath option you should not include the `/hostfs/` mount in the filter.  If both this and `fsTypes` is specified, the two filters combine in an AND relationship. |
| `sendModeDimension` | no | `bool` | Set to true to emit the "mode" dimension, which represents whether the mount is "rw" or "ro". (**default:** `false`) |


## Metrics

These are the metrics available for this monitor.
Metrics that are categorized as
[container/host](https://docs.splunk.com/observability/admin/subscription-usage/monitor-imm-billing-usage.html#about-custom-bundled-and-high-resolution-metrics)
(*default*) are ***in bold and italics*** in the list below.


 - ***`df_complex.free`*** (*gauge*)<br>    Free disk space in bytes
 - `df_complex.reserved` (*gauge*)<br>    Measures disk space in bytes reserved for the super-user on this file system.
 - ***`df_complex.used`*** (*gauge*)<br>    Used disk space in bytes
 - ***`disk.summary_utilization`*** (*gauge*)<br>    Percent of disk space utilized on all volumes on this host.
 - ***`disk.utilization`*** (*gauge*)<br>    Percent of disk used on this volume.

#### Group inodes
All of the following metrics are part of the `inodes` metric group. All of
the non-default metrics below can be turned on by adding `inodes` to the
monitor config option `extraGroups`:
 - `df_inodes.free` (*gauge*)<br>    (Linux Only) Number of inodes that are free.
 - `df_inodes.used` (*gauge*)<br>    (Linux Only) Number of inodes that are used.
 - `percent_inodes.free` (*gauge*)<br>    (Linux Only) Free inodes on the file system, expressed as a percentage.
 - `percent_inodes.used` (*gauge*)<br>    (Linux Only) Used inodes on the file system, expressed as a percentage.

#### Group percentage
All of the following metrics are part of the `percentage` metric group. All of
the non-default metrics below can be turned on by adding `percentage` to the
monitor config option `extraGroups`:
 - `percent_bytes.free` (*gauge*)<br>    Free disk space on the file system, expressed as a percentage.
 - `percent_bytes.reserved` (*gauge*)<br>    Measures disk space reserved for the super-user as a percentage of total disk space of this file system.
 - `percent_bytes.used` (*gauge*)<br>    Used disk space on the file system, expressed as a percentage.

### Non-default metrics (version 4.7.0+)

To emit metrics that are not _default_, you can add those metrics in the
generic monitor-level `extraMetrics` config option.  Metrics that are derived
from specific configuration options that do not appear in the above list of
metrics do not need to be added to `extraMetrics`.

To see a list of metrics that will be emitted you can run `agent-status
monitors` after configuring this monitor in a running agent instance.



