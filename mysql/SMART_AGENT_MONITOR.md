
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->

### INSTALLATION

This integration is part of the [SignalFx Smart Agent](https://github.com/signalfx/integrations/tree/master/signalfx-agent)[](sfx_link:signalfx-agent)
as the `collectd/mysql` monitor. You should first deploy the Smart Agent to the
same host as the service you want to monitor, and then continue with the
configuration instructions below.

<!--- GENERATED BY gomplate from scripts/docs/monitor-page.md.tmpl --->

# collectd/mysql

Monitor Type: `collectd/mysql` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/internal/monitors/collectd/mysql))

**Accepts Endpoints**: **Yes**

**Multiple Instances Allowed**: Yes


## Description

**This integration primarily consists of the Smart Agent monitor `collectd/mysql`.
Below is an overview of that monitor.**

### Smart Agent Monitor


Monitors a MySQL database server using collectd's [MySQL
plugin](https://collectd.org/wiki/index.php/Plugin:MySQL). It supports
MySQL versions 5.x or later.

This monitor connects to a MySQL instance and reports on the values
returned by a `SHOW STATUS` command. This includes the following:

  - Number of commands processed
  - Table and row operations (handlers)
  - State of the query cache
  - Status of MySQL threads
  - Network traffic

<!--- SETUP --->
### Note on localhost
On Unix, MySQL programs treat the host name `localhost` specially, in a way
that is likely different from what is expected compared to other
network-based programs. For connections to `localhost`, MySQL programs
attempt to connect to the local server by using a Unix socket file. To ensure
that the client makes a TCP/IP connection to the local server specify a host
name value of `127.0.0.1`, or the IP address or name of the local server.

<!--- SETUP --->
### Databases
You have to specify each database you want to monitor individually under
the `databases` config option.  If you have a common authentication to all
databases being monitored, you can specify that in the top-level
`username`/`password` options, otherwise they can be specified at the
database level.


<!--- SETUP --->
### Example Config

Sample YAML configuration:

```
monitors:
 - type: collectd/mysql
   host: 127.0.0.1
   port: 3306
   databases:
     - name: dbname
     - name: securedb
       username: admin
       password: s3cr3t
   username: dbuser
   password: passwd
```


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: collectd/mysql
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](https://github.com/signalfx/signalfx-agent/tree/master/docs/monitors/../monitor-config.md#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `host` | **yes** | `string` |  |
| `port` | **yes** | `integer` |  |
| `name` | no | `string` |  |
| `databases` | **yes** | `list of objects (see below)` | A list of databases along with optional authentication credentials. |
| `username` | no | `string` | These credentials serve as defaults for all databases if not overridden |
| `password` | no | `string` |  |
| `reportHost` | no | `bool` | A SignalFx extension to the plugin that allows us to disable the normal behavior of the MySQL collectd plugin where the `host` dimension is set to the hostname of the MySQL database server.  When `false` (the recommended and default setting), the globally configured `hostname` config is used instead. (**default:** `false`) |


The **nested** `databases` config object has the following fields:

| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `name` | **yes** | `string` |  |
| `username` | no | `string` |  |
| `password` | no | `string` |  |


## Metrics

These are the metrics available for this monitor.
Metrics that are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
(*default*) are ***in bold and italics*** in the list below.


 - `cache_result.cache_size` (*gauge*)<br>    MySQL Qcache Size
 - ***`cache_result.qcache-hits`*** (*cumulative*)<br>    The number of hits on MySQL query cache.
 - ***`cache_result.qcache-inserts`*** (*cumulative*)<br>    The number of inserts into MySQL query cache.
 - `cache_result.qcache-not_cached` (*cumulative*)<br>    The number of MySQL queries that were not cacheable or not cached.
 - `cache_result.qcache-prunes` (*cumulative*)<br>    The number of queries that were pruned from query cache because of low-memory condition.
 - ***`cache_size.qcache`*** (*gauge*)<br>    The number of queries in MySQL query cache.
 - `mysql_commands.admin_commands` (*cumulative*)<br>    The number of MySQL ADMIN commands executed
 - `mysql_commands.alter_db` (*cumulative*)<br>    The number of MySQL ALTER DB commands executed
 - `mysql_commands.alter_db_upgrade` (*cumulative*)<br>    The number of MySQL ALTER DB UPGRADE commands executed
 - `mysql_commands.alter_event` (*cumulative*)<br>    The number of MySQL ALTER EVENT commands executed
 - `mysql_commands.alter_function` (*cumulative*)<br>    The number of MySQL ALTER FUNCTION commands executed
 - `mysql_commands.alter_procedure` (*cumulative*)<br>    The number of MySQL ALTER PROCEDURE commands executed
 - `mysql_commands.alter_server` (*cumulative*)<br>    The number of MySQL ALTER SERVER commands executed
 - `mysql_commands.alter_table` (*cumulative*)<br>    The number of MySQL ALTER TABLE commands executed
 - `mysql_commands.alter_tablespace` (*cumulative*)<br>    The number of MySQL ALTER TABLESPACE commands executed
 - `mysql_commands.alter_user` (*cumulative*)<br>    The number of MySQL ALTER USER commands executed
 - `mysql_commands.analyze` (*cumulative*)<br>    The number of MySQL ANALYZE commands executed
 - `mysql_commands.assign_to_keycache` (*cumulative*)<br>    The number of MySQL ASSIGN TO KEYCACHE commands executed
 - `mysql_commands.begin` (*cumulative*)<br>    The number of MySQL BEGIN commands executed
 - `mysql_commands.binlog` (*cumulative*)<br>    The number of MySQL BINLOG commands executed
 - `mysql_commands.call_procedure` (*cumulative*)<br>    The number of MySQL CALL PROCEDURE commands executed
 - `mysql_commands.change_db` (*cumulative*)<br>    The number of MySQL CHANGE DB commands executed
 - `mysql_commands.change_master` (*cumulative*)<br>    The number of MySQL CHANGE MASTER commands executed
 - `mysql_commands.check` (*cumulative*)<br>    The number of MySQL CHECK commands executed
 - `mysql_commands.checksum` (*cumulative*)<br>    The number of MySQL CHECKSUM commands executed
 - `mysql_commands.commit` (*cumulative*)<br>    The number of MySQL COMMIT commands executed
 - `mysql_commands.create_db` (*cumulative*)<br>    The number of MySQL CREATE DB commands executed
 - `mysql_commands.create_event` (*cumulative*)<br>    The number of MySQL CREATE EVENT commands executed
 - `mysql_commands.create_function` (*cumulative*)<br>    The number of MySQL CREATE FUNCTION commands executed
 - `mysql_commands.create_index` (*cumulative*)<br>    The number of MySQL CREATE INDEX commands executed
 - `mysql_commands.create_procedure` (*cumulative*)<br>    The number of MySQL CREATE PROCEDURE commands executed
 - `mysql_commands.create_server` (*cumulative*)<br>    The number of MySQL CREATE SERVER commands executed
 - `mysql_commands.create_table` (*cumulative*)<br>    The number of MySQL CREATE TABLE commands executed
 - `mysql_commands.create_trigger` (*cumulative*)<br>    The number of MySQL CREATE TRIGGER commands executed
 - `mysql_commands.create_udf` (*cumulative*)<br>    The number of MySQL CREATE UDF commands executed
 - `mysql_commands.create_user` (*cumulative*)<br>    The number of MySQL CREATE USER commands executed
 - `mysql_commands.create_view` (*cumulative*)<br>    The number of MySQL CREATE VIEW commands executed
 - `mysql_commands.dealloc_sql` (*cumulative*)<br>    The number of MySQL DEALLOC SQL commands executed
 - ***`mysql_commands.delete`*** (*cumulative*)<br>    The number of MySQL DELETE commands executed
 - `mysql_commands.delete_multi` (*cumulative*)<br>    The number of MySQL DELETE MULTI commands executed
 - `mysql_commands.do` (*cumulative*)<br>    The number of MySQL DO commands executed
 - `mysql_commands.drop_db` (*cumulative*)<br>    The number of MySQL DROP DB commands executed
 - `mysql_commands.drop_event` (*cumulative*)<br>    The number of MySQL DROP EVENT commands executed
 - `mysql_commands.drop_function` (*cumulative*)<br>    The number of MySQL DROP FUNCTION commands executed
 - `mysql_commands.drop_index` (*cumulative*)<br>    The number of MySQL DROP INDEX commands executed
 - `mysql_commands.drop_procedure` (*cumulative*)<br>    The number of MySQL DROP PROCEDURE commands executed
 - `mysql_commands.drop_server` (*cumulative*)<br>    The number of MySQL DROP SERVER commands executed
 - `mysql_commands.drop_table` (*cumulative*)<br>    The number of MySQL DROP TABLE commands executed
 - `mysql_commands.drop_trigger` (*cumulative*)<br>    The number of MySQL DROP TRIGGER commands executed
 - `mysql_commands.drop_user` (*cumulative*)<br>    The number of MySQL DROP USER commands executed
 - `mysql_commands.drop_view` (*cumulative*)<br>    The number of MySQL DROP VIEW commands executed
 - `mysql_commands.empty_query` (*cumulative*)<br>    The number of MySQL EMPTY QUERY commands executed
 - `mysql_commands.execute_sql` (*cumulative*)<br>    The number of MySQL EXECUTE SQL commands executed
 - `mysql_commands.flush` (*cumulative*)<br>    The number of MySQL FLUSH commands executed
 - `mysql_commands.get_diagnostics` (*cumulative*)<br>    The number of MySQL GET DIAGNOSTICS commands executed
 - `mysql_commands.grant` (*cumulative*)<br>    The number of MySQL GRANT commands executed
 - `mysql_commands.ha_close` (*cumulative*)<br>    The number of MySQL HA CLOSE commands executed
 - `mysql_commands.ha_open` (*cumulative*)<br>    The number of MySQL HA OPEN commands executed
 - `mysql_commands.ha_read` (*cumulative*)<br>    The number of MySQL HA READ commands executed
 - `mysql_commands.help` (*cumulative*)<br>    The number of MySQL HELP commands executed
 - ***`mysql_commands.insert`*** (*cumulative*)<br>    The number of MySQL INSERT commands executed
 - `mysql_commands.insert_select` (*cumulative*)<br>    The number of MySQL INSERT SELECT commands executed
 - `mysql_commands.install_plugin` (*cumulative*)<br>    The number of MySQL INSTALL PLUGIN commands executed
 - `mysql_commands.kill` (*cumulative*)<br>    The number of MySQL KILL commands executed
 - `mysql_commands.load` (*cumulative*)<br>    The number of MySQL LOAD commands executed
 - `mysql_commands.lock_tables` (*cumulative*)<br>    The number of MySQL LOCK TABLES commands executed
 - `mysql_commands.optimize` (*cumulative*)<br>    The number of MySQL OPTIMIZE commands executed
 - `mysql_commands.preload_keys` (*cumulative*)<br>    The number of MySQL PRELOAD KEYS commands executed
 - `mysql_commands.prepare_sql` (*cumulative*)<br>    The number of MySQL PREPARE SQL commands executed
 - `mysql_commands.purge` (*cumulative*)<br>    The number of MySQL PURGE commands executed
 - `mysql_commands.purge_before_date` (*cumulative*)<br>    The number of MySQL PURGE BEFORE DATE commands executed
 - `mysql_commands.release_savepoint` (*cumulative*)<br>    The number of MySQL RELEASE SAVEPOINT commands executed
 - `mysql_commands.rename_table` (*cumulative*)<br>    The number of MySQL RENAME TABLE commands executed
 - `mysql_commands.rename_user` (*cumulative*)<br>    The number of MySQL RENAME USER commands executed
 - `mysql_commands.repair` (*cumulative*)<br>    The number of MySQL REPAIR commands executed
 - `mysql_commands.replace` (*cumulative*)<br>    The number of MySQL REPLACE commands executed
 - `mysql_commands.replace_select` (*cumulative*)<br>    The number of MySQL REPLACE SELECT commands executed
 - `mysql_commands.reset` (*cumulative*)<br>    The number of MySQL RESET commands executed
 - `mysql_commands.resignal` (*cumulative*)<br>    The number of MySQL RESIGNAL commands executed
 - `mysql_commands.revoke` (*cumulative*)<br>    The number of MySQL REVOKE commands executed
 - `mysql_commands.revoke_all` (*cumulative*)<br>    The number of MySQL REVOKE ALL commands executed
 - `mysql_commands.rollback` (*cumulative*)<br>    The number of MySQL ROLLBACK commands executed
 - `mysql_commands.rollback_to_savepoint` (*cumulative*)<br>    The number of MySQL ROLLBACK TO SAVEPOINT commands executed
 - `mysql_commands.savepoint` (*cumulative*)<br>    The number of MySQL SAVEPOINT commands executed
 - ***`mysql_commands.select`*** (*cumulative*)<br>    The number of MySQL SELECT commands executed
 - `mysql_commands.set_option` (*cumulative*)<br>    The number of MySQL SET OPTION commands executed
 - `mysql_commands.show_binlog_events` (*cumulative*)<br>    The number of MySQL SHOW BINLOG EVENTS commands executed
 - `mysql_commands.show_binlogs` (*cumulative*)<br>    The number of MySQL SHOW BINLOGS commands executed
 - `mysql_commands.show_charsets` (*cumulative*)<br>    The number of MySQL SHOW CHARSETS commands executed
 - `mysql_commands.show_collations` (*cumulative*)<br>    The number of MySQL SHOW COLLATIONS commands executed
 - `mysql_commands.show_create_db` (*cumulative*)<br>    The number of MySQL SHOW CREATE DB commands executed
 - `mysql_commands.show_create_event` (*cumulative*)<br>    The number of MySQL SHOW CREATE EVENT commands executed
 - `mysql_commands.show_create_func` (*cumulative*)<br>    The number of MySQL SHOW CREATE FUNC commands executed
 - `mysql_commands.show_create_proc` (*cumulative*)<br>    The number of MySQL SHOW CREATE PROC commands executed
 - `mysql_commands.show_create_table` (*cumulative*)<br>    The number of MySQL SHOW CREATE TABLE commands executed
 - `mysql_commands.show_create_trigger` (*cumulative*)<br>    The number of MySQL SHOW CREATE TRIGGER commands executed
 - `mysql_commands.show_databases` (*cumulative*)<br>    The number of MySQL SHOW DATABASES commands executed
 - `mysql_commands.show_engine_logs` (*cumulative*)<br>    The number of MySQL SHOW ENGINE LOGS commands executed
 - `mysql_commands.show_engine_mutex` (*cumulative*)<br>    The number of MySQL SHOW ENGINE MUTEX commands executed
 - `mysql_commands.show_engine_status` (*cumulative*)<br>    The number of MySQL SHOW ENGINE STATUS commands executed
 - `mysql_commands.show_errors` (*cumulative*)<br>    The number of MySQL SHOW ERRORS commands executed
 - `mysql_commands.show_events` (*cumulative*)<br>    The number of MySQL SHOW EVENTS commands executed
 - `mysql_commands.show_fields` (*cumulative*)<br>    The number of MySQL SHOW FIELDS commands executed
 - `mysql_commands.show_function_code` (*cumulative*)<br>    The number of MySQL SHOW FUNCTION CODE commands executed
 - `mysql_commands.show_function_status` (*cumulative*)<br>    The number of MySQL SHOW FUNCTION STATUS commands executed
 - `mysql_commands.show_grants` (*cumulative*)<br>    The number of MySQL SHOW GRANTS commands executed
 - `mysql_commands.show_keys` (*cumulative*)<br>    The number of MySQL SHOW KEYS commands executed
 - `mysql_commands.show_master_status` (*cumulative*)<br>    The number of MySQL SHOW MASTER STATUS commands executed
 - `mysql_commands.show_open_tables` (*cumulative*)<br>    The number of MySQL SHOW OPEN TABLES commands executed
 - `mysql_commands.show_plugins` (*cumulative*)<br>    The number of MySQL SHOW PLUGINS commands executed
 - `mysql_commands.show_privileges` (*cumulative*)<br>    The number of MySQL SHOW PRIVILEGES commands executed
 - `mysql_commands.show_procedure_code` (*cumulative*)<br>    The number of MySQL SHOW PROCEDURE CODE commands executed
 - `mysql_commands.show_procedure_status` (*cumulative*)<br>    The number of MySQL SHOW PROCEDURE STATUS commands executed
 - `mysql_commands.show_processlist` (*cumulative*)<br>    The number of MySQL SHOW PROCESSLIST commands executed
 - `mysql_commands.show_profile` (*cumulative*)<br>    The number of MySQL SHOW PROFILE commands executed
 - `mysql_commands.show_profiles` (*cumulative*)<br>    The number of MySQL SHOW PROFILES commands executed
 - `mysql_commands.show_relaylog_events` (*cumulative*)<br>    The number of MySQL SHOW RELAYLOG EVENTS commands executed
 - `mysql_commands.show_slave_hosts` (*cumulative*)<br>    The number of MySQL SHOW SLAVE HOSTS commands executed
 - `mysql_commands.show_slave_status` (*cumulative*)<br>    The number of MySQL SHOW SLAVE STATUS commands executed
 - `mysql_commands.show_status` (*cumulative*)<br>    The number of MySQL SHOW STATUS commands executed
 - `mysql_commands.show_storage_engines` (*cumulative*)<br>    The number of MySQL SHOW STORAGE ENGINES commands executed
 - `mysql_commands.show_table_status` (*cumulative*)<br>    The number of MySQL SHOW TABLE STATUS commands executed
 - `mysql_commands.show_tables` (*cumulative*)<br>    The number of MySQL SHOW TABLES commands executed
 - `mysql_commands.show_triggers` (*cumulative*)<br>    The number of MySQL SHOW TRIGGERS commands executed
 - `mysql_commands.show_variables` (*cumulative*)<br>    The number of MySQL SHOW VARIABLES commands executed
 - `mysql_commands.show_warnings` (*cumulative*)<br>    The number of MySQL SHOW WARNINGS commands executed
 - `mysql_commands.signal` (*cumulative*)<br>    The number of MySQL SIGNAL commands executed
 - `mysql_commands.slave_start` (*cumulative*)<br>    The number of MySQL SLAVE START commands executed
 - `mysql_commands.slave_stop` (*cumulative*)<br>    The number of MySQL SLAVE STOP commands executed
 - `mysql_commands.truncate` (*cumulative*)<br>    The number of MySQL TRUNCATE commands executed
 - `mysql_commands.uninstall_plugin` (*cumulative*)<br>    The number of MySQL UNINSTALL PLUGIN commands executed
 - `mysql_commands.unlock_tables` (*cumulative*)<br>    The number of MySQL UNLOCK TABLES commands executed
 - ***`mysql_commands.update`*** (*cumulative*)<br>    The number of MySQL UPDATE commands executed
 - `mysql_commands.update_multi` (*cumulative*)<br>    The number of MySQL UPDATE MULTI commands executed
 - `mysql_commands.xa_commit` (*cumulative*)<br>    The number of MySQL XA COMMIT commands executed
 - `mysql_commands.xa_end` (*cumulative*)<br>    The number of MySQL XA END commands executed
 - `mysql_commands.xa_prepare` (*cumulative*)<br>    The number of MySQL XA PREPARE commands executed
 - `mysql_commands.xa_recover` (*cumulative*)<br>    The number of MySQL XA RECOVER commands executed
 - `mysql_commands.xa_rollback` (*cumulative*)<br>    The number of MySQL XA ROLLBACK commands executed
 - `mysql_commands.xa_start` (*cumulative*)<br>    The number of MySQL XA START commands executed
 - `mysql_handler.commit` (*cumulative*)<br>    The number of internal COMMIT statements.
 - `mysql_handler.delete` (*cumulative*)<br>    The number of times rows have been deleted from tables.
 - `mysql_handler.external_lock` (*cumulative*)<br>    The number of external_lock occurences.
 - `mysql_handler.prepare` (*cumulative*)<br>    The number of times "Prepare" phase was executed in the two-phase commit operations.
 - `mysql_handler.read_first` (*cumulative*)<br>    The number of times the first entry in an index was read.
 - `mysql_handler.read_key` (*cumulative*)<br>    The number of times a row was read based on a key.
 - `mysql_handler.read_next` (*cumulative*)<br>    The number of requests to read the next row in key order.
 - `mysql_handler.read_prev` (*cumulative*)<br>    The number of requests to read the previous row in key order.
 - `mysql_handler.read_rnd` (*cumulative*)<br>    The number of requests that read a random fixed position in the data file.
 - `mysql_handler.read_rnd_next` (*cumulative*)<br>    The number of requests for the next row in the data file.
 - `mysql_handler.rollback` (*cumulative*)<br>    The number of requests for a rollback operation on the storage engine.
 - `mysql_handler.savepoint` (*cumulative*)<br>    The number of requests to place a savepoint on the storage engine.  This can be used to roll back later.
 - `mysql_handler.savepoint_rollback` (*cumulative*)<br>    The number of requests to roll back to a savepoint.
 - `mysql_handler.update` (*cumulative*)<br>    The number of requests to update a row in a table.
 - `mysql_handler.write` (*cumulative*)<br>    The number of requests to insert a row in a table.
 - ***`mysql_locks.immediate`*** (*cumulative*)<br>    The number of MySQL table locks which were granted immediately.
 - ***`mysql_locks.waited`*** (*cumulative*)<br>    The number of MySQL table locks which had to wait before being granted.
 - ***`mysql_octets.rx`*** (*cumulative*)<br>    The number of bytes received by MySQL server from all clients.
 - ***`mysql_octets.tx`*** (*cumulative*)<br>    The number of bytes sent by MySQL server to all clients.
 - `mysql_select.full_join` (*cumulative*)<br>    The number of joins that perform full table scans.
 - `mysql_select.full_range_join` (*cumulative*)<br>    The number of joins that used a range search on a reference table.
 - `mysql_select.range` (*cumulative*)<br>    The number of joins that used a range on the first table.
 - `mysql_select.range_check` (*cumulative*)<br>    The number of joins without keys that check for key usage after each row.
 - `mysql_select.scan` (*cumulative*)<br>    The number of joins that did a full scan of the first table.
 - `mysql_slow_queries` (*cumulative*)<br>    The number of queries that have taken more than long_query_time seconds.
 - `mysql_sort.range` (*cumulative*)<br>    The number of sorts that were done using ranges.
 - `mysql_sort.scan` (*cumulative*)<br>    The number of sorts that were done by scanning the table.
 - `mysql_sort_merge_passes` (*cumulative*)<br>    The number of merge passes done by the sorting algorithm.
 - `mysql_sort_rows` (*cumulative*)<br>    The number of rows that were sorted.
 - ***`threads.cached`*** (*gauge*)<br>    The number of threads cached by MySQL for re-use on a new client connection.  A MySQL thread corresponds to a single MySQL connection.
 - ***`threads.connected`*** (*gauge*)<br>    The number of currently open MySQL connections.  A MySQL thread corresponds to a single MySQL connection.
 - `threads.running` (*gauge*)<br>    The number of MySQL threads that are processing a query.  A MySQL thread corresponds to a single MySQL connection.
 - `total_threads.created` (*cumulative*)<br>    The total number of threads created by MySQL for client connections.  A MySQL thread corresponds to a single MySQL connection.

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


