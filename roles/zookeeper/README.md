# Apache ZooKeeper

zookeeper_version: 3.7.2
zookeeper_mirror: https://www-eu.apache.org/dist/zookeeper
zookeeper_package: apache-zookeeper-{{ zookeeper_version }}-bin.tar.gz
zookeeper_source_dir: zoo_source

zookeeper_create_user_group: true
zookeeper_group: zookeeper
zookeeper_user: zookeeper

zookeeper_root_dir: /opt
zookeeper_install_dir: "{{ zookeeper_root_dir }}/apache-zookeeper-{{ zookeeper_version }}"

# The zookeeper_dir is created as a symlik to the actual installation directory.

# All other configuration and variables use the symlinked directory.

zookeeper_dir: "{{ zookeeper_root_dir }}/zookeeper"
zookeeper_log_dir: /var/log/zookeeper

# Start zookeeper after installation

zookeeper_start: yes

# Restart zookeeper on configuration change

zookeeper_restart: yes

# Configuration variables

# The unit of time for ZooKeeper translated to milliseconds.

# This governs all ZooKeeper time dependent operations. It is used for heartbeats and timeouts especially.

# Note that the minimum session timeout will be two ticks.

zookeeper_ticktime: 3000

# Amount of time, in ticks (see tickTime), to allow followers to connect and sync to a leader.

# Increased this value as needed, if the amount of data managed by ZooKeeper is large.

zookeeper_init_limit: 10

# Amount of time, in ticks (see tickTime), to allow followers to sync with ZooKeeper.

# If followers fall too far behind a leader, they will be dropped.

zookeeper_sync_limit: 5

# The directory where ZooKeeper in-memory database snapshots and, unless specified in dataLogDir, the transaction log of updates to the database.

# This location should be a dedicated disk that is ideally an SSD.

# For more information, see the ZooKeeper Administration Guide (https://zookeeper.apache.org/doc/current/zookeeperAdmin.html).

zookeeper_data_dir: /var/lib/zookeeper

# The location where the transaction log is written to. If you don’t specify this option, the log is written to dataDir.

# By specifying this option, you can use a dedicated log device, and help avoid competition between logging and snapshots.

# For more information, see the ZooKeeper Administration Guide (https://zookeeper.apache.org/doc/current/zookeeperAdmin.html).

zookeeper_data_log_dir: /var/lib/zookeeper

# This is the port where ZooKeeper clients will listen on. This is where the Brokers will connect to ZooKeeper. Typically this is set to 2181.

zookeeper_client_port: 2181

# The maximum allowed number of client connections for a ZooKeeper server. To avoid running out of allowed connections set this to 0 (unlimited).

zookeeper_max_client_cnxns: 60

# When enabled, ZooKeeper auto purge feature retains the autopurge.snapRetainCount most recent snapshots and the corresponding transaction logs

# in the dataDir and dataLogDir respectively and deletes the rest.

zookeeper_autopurge_snap_retain_count: 3

# The time interval in hours for which the purge task has to be triggered. Set to a positive integer (1 and above) to enable the auto purging.

zookeeper_purge_interval: 0

# Uniquely identifies the ZooKeeper instance when clustering ZooKeeper nodes.

# This value is placed in the /var/lib/zookeeper/myid file.

zookeeper_id: 1
zookeeper_leader_port: 2888
zookeeper_election_port: 3888
zookeeper_servers: "{{ groups['kafka_servers'] }}"
zookeeper_environment: {}

# Set to "false" to disable the AdminServer. By default the AdminServer is enabled.

zookeeper_enable_server: yes

# The address the embedded Jetty server listens on. Defaults to 0.0.0.0.

zookeeper_server_address: 0.0.0.0

# The port the embedded Jetty server listens on. Defaults to 8080.

zookeeper_server_port: 8080

# Set the maximum idle time in milliseconds that a connection can wait before sending or receiving data. Defaults to 30000 ms.

zookeeper_idle_timeout: 30000

# The URL for listing and issuing commands relative to the root URL. Defaults to "/commands".

zookeeper_command_url: /commands

# See https://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_4lw. Use \* to allow all commands.

zookeeper_command_whitelist: stat, ruok, conf, isro

# Set to "org.apache.zookeeper.metrics.prometheus.PrometheusMetricsProvider" to enable Prometheus.io exporter.

zookeeper_metricsprovider_classname: org.apache.zookeeper.metrics.prometheus.PrometheusMetricsProvider

# Prometheus.io exporter will start a Jetty server and bind to this port, it default to 7000. Prometheus end point will be http://hostname:httPort/metrics.

zookeeper_metricsprovider_httpport: 7000

# If this property is set to true Prometheus.io will export useful metrics about the JVM. The default is true.

zookeeper_metricsprovider_exportjvminfo: yes
