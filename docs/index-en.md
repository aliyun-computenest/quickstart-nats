<!DOCTYPE html>
<body>

<h1 id="overview">Overview</h1>
<p>NATS is an open-source, lightweight, high-performance distributed messaging middleware.</p>
<p>With the emergence of NATS 2.0, the NATS ecosystem has developed significantly. NATS 2.0 provides distributed security, decentralized management, multi-tenancy, larger networks, global scalability, and secure data sharing. However, NATS Streaming had many limitations in adapting to NATS 2.0, and the streaming system had not yet evolved to meet the challenges of next-generation IoT and edge computing.</p>
<p>The next-generation NATS streaming system for NATS 2.0 is called <strong>NATS JetStream</strong>, which features distributed security, multi-tenancy, and horizontal scalability.</p>
<p>Compute Nest provides the NATS Community Edition service. You do not need to configure cloud hosts yourself; you can quickly deploy NATS services on Compute Nest and implement operation and maintenance monitoring, thereby facilitating the construction of your own cloud-native, distributed, and microservices-based business applications based on NATS.</p>
<p>This document introduces how to activate the NATS Community Edition service on Compute Nest, as well the deployment process and usage instructions.</p>

<h1 id="billing-information">Billing Information</h1>
<p>The costs for NATS Community Edition on Compute Nest mainly involve:</p>
<ul>
    <li>Selected vCPU and memory specifications</li>
    <li>Disk capacity</li>
    <li>Public network bandwidth (if public network service is enabled)</li>
</ul>
<p>Billing methods include:</p>
<ul>
    <li>Pay-As-You-Go (Hourly)</li>
    <li>Subscription (Yearly/Monthly)</li>
</ul>
<p>Estimated costs can be seen in real-time when creating the instance.</p>

<h1 id="deployment-architecture">Deployment Architecture</h1>
<p>NATS Community Edition offers two architectural options: standalone deployment and cluster deployment.</p>
<p>The cluster version currently supports deploying an odd number of nodes ranging from 3 to 11.</p>

<h1 id="required-permissions">Required Permissions</h1>
<p>The NATS service requires access and creation operations for resources such as ECS and VPC. If you use a RAM user to create a service instance, you must add the corresponding resource permissions to the RAM user account before creating the service instance.</p>
<p>For detailed operations on adding RAM permissions, please refer to <a href="https://help.aliyun.com/document_detail/121945.html">Authorize RAM Users</a>. The required permissions are listed in the table below.</p>

<table>
    <thead>
        <tr>
            <th>Permission Policy Name</th>
            <th>Remarks</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>AliyunECSFullAccess</td>
            <td>Permission to manage Elastic Compute Service (ECS)</td>
        </tr>
        <tr>
            <td>AliyunVPCFullAccess</td>
            <td>Permission to manage Virtual Private Cloud (VPC)</td>
        </tr>
        <tr>
            <td>AliyunROSFullAccess</td>
            <td>Permission to manage Resource Orchestration Service (ROS)</td>
        </tr>
        <tr>
            <td>AliyunComputeNestUserFullAccess</td>
            <td>User-side permission to manage Compute Nest services</td>
        </tr>
        <tr>
            <td>AliyunCloudMonitorFullAccess</td>
            <td>Permission to manage Cloud Monitor</td>
        </tr>
    </tbody>
</table>

<h1 id="deployment-process">Deployment Process</h1>
<p>This document demonstrates the process for deploying the cluster version.</p>

<h2 id="parameter-description">Parameter Description</h2>
<p>During the process of creating a service instance, you need to configure service instance information. The following details the input parameters for the NATS Community Edition service instance.</p>

<table>
    <thead>
        <tr>
            <th>Parameter Group</th>
            <th>Parameter Item</th>
            <th>Example</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Select Template</td>
            <td>Template Selection</td>
            <td>Cluster Version</td>
            <td>Template architecture type</td>
        </tr>
        <tr>
            <td>Service Instance Name</td>
            <td></td>
            <td>test</td>
            <td>Name of the instance</td>
        </tr>
        <tr>
            <td>Region</td>
            <td></td>
            <td>China (Hangzhou)</td>
            <td>Region where the service instance is located. It is recommended to select the nearest region to obtain better network latency.</td>
        </tr>
        <tr>
            <td>Availability Zone Configuration</td>
            <td>Deployment Area</td>
            <td>Zone I</td>
            <td>Different availability zones within the region</td>
        </tr>
        <tr>
            <td>Billing Type Configuration</td>
            <td>Billing Type</td>
            <td>Pay-As-You-Go or Subscription</td>
            <td></td>
        </tr>
        <tr>
            <td>Select Existing Basic Resource Configuration</td>
            <td>VPC ID</td>
            <td>vpc-xxx</td>
            <td>Select the ID of the Virtual Private Cloud.</td>
        </tr>
        <tr>
            <td>Select Existing Basic Resource Configuration</td>
            <td>VSwitch ID</td>
            <td>vsw-xxx</td>
            <td>Select the VSwitch ID. If the VSwitch cannot be found, try switching regions and availability zones.</td>
        </tr>
        <tr>
            <td>ECS Instance Configuration</td>
            <td>Instance Type</td>
            <td>ecs.g7.large</td>
            <td>Instance specification, can be selected based on actual needs</td>
        </tr>
        <tr>
            <td>ECS Instance Configuration</td>
            <td>System Disk Space</td>
            <td>40</td>
            <td>System disk space, can be selected based on actual needs</td>
        </tr>
        <tr>
            <td>ECS Instance Configuration</td>
            <td>Data Disk Space</td>
            <td>40</td>
            <td>Data disk space, can be selected based on actual needs</td>
        </tr>
        <tr>
            <td>ECS Instance Configuration</td>
            <td>Instance Password</td>
            <td>********</td>
            <td>Set the instance password. Length 8~30 characters, must contain three of the following categories: uppercase letters, lowercase letters, numbers, special symbols ()`~!@#$%^&*-+={}[]:;'<>,.?/</td>
        </tr>
        <tr>
            <td>ECS Instance Configuration</td>
            <td>Enable Public IP</td>
            <td>true</td>
            <td>Whether to enable a public IP address</td>
        </tr>
        <tr>
            <td>NATS Configuration</td>
            <td>Cluster Node Count</td>
            <td>3</td>
            <td>Number of nodes for the cluster version</td>
        </tr>
        <tr>
            <td>NATS Configuration</td>
            <td>Admin Password</td>
            <td>*****</td>
            <td>Password for the default admin user, 22-30 characters</td>
        </tr>
    </tbody>
</table>

<h2 id="deployment-steps">Deployment Steps</h2>
<p>Click the <a href="https://computenest.console.aliyun.com/user/cn-hangzhou/serviceInstanceCreate?ServiceId=service-c63f342f7c7f48e8bbb5">Deployment Link</a> to enter the service instance deployment interface. Following the prompts, you can choose the default deployment template for quick deployment, or use a custom template for personalized parameter configuration.</p>
<p>The detailed deployment page is shown below:</p>

<p>The convenient method is to select the default package, then simply select the availability zone, VPC information, configure the instance password and NATS password, and click to create the cluster.</p>

<p>Wait approximately 1 minute. When the status changes to "Deployed", the cluster creation is complete.</p>

<p>At this point, click the service instance name to connect and enter the connection page:</p>

<p>You can see the public and private network access pages.</p>
<p>The following demonstrates operating NATS via the public network address.</p>

<h1 id="cluster-configuration-exploration">Cluster Configuration Exploration</h1>
<p>NATS configuration file:</p>
<pre><code class="language-bash">[root@iZbp139ju1kmizva7adgdbZ ~]# cat /etc/nats/nats.conf 
server_name=iZbp139ju1kmizva7adgdbZ-172-16-0-155
listen: 0.0.0.0:4222
http: 8222
accounts {
  $SYS {
    users = [
      { user: "admin",
        pass: "$2a$11$GUizXsS82Y.dll.uZXDic.qMDePF2IT6d3t5iWIs.rQ3lY1p6mDKC"
      }
    ]
  }
}

jetstream {
   store_dir=/data/nats-storage
}

cluster {
  name: C1
  listen: 0.0.0.0:4248
  routes = [
      
      nats-route://172.16.0.155:4248
      nats-route://172.16.0.157:4248
      nats-route://172.16.0.156:4248
  ]
}
</code></pre>
<p>From the configuration, it can be seen that the JetStream feature is enabled by default, and the persistence directory is stored on the data disk under <code>/data</code>.</p>
<pre><code class="language-bash">[root@iZbp19f7ptaaw66l28h5bnZ ~]# df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        3.8G     0  3.8G   0% /dev
tmpfs           3.8G     0  3.8G   0% /dev/shm
tmpfs           3.8G  512K  3.8G   1% /run
tmpfs           3.8G     0  3.8G   0% /sys/fs/cgroup
/dev/vda1        40G  2.5G   35G   7% /
/dev/vdb1        40G   49M   38G   1% /data
tmpfs           768M     0  768M   0% /run/user/0
[root@iZbp19f7ptaaw66l28h5bnZ ~]# tree /data/nats-storage/
/data/nats-storage/
└── jetstream
    ├── $G
    │   └── streams
    │       └── my_stream
    │           ├── meta.inf
    │           ├── meta.sum
    │           ├── msgs
    │           │   ├── 1.blk
    │           │   ├── 1.fss
    │           │   └── 1.idx
    │           └── obs
    │               ├── foo_comsumer
    │               │   ├── meta.inf
    │               │   ├── meta.sum
    │               │   └── o.dat
    │               ├── foo_consumer
    │               │   ├── meta.inf
    │               │   ├── meta.sum
    │               │   └── o.dat
    │               └── foo_consumer2
    │                   ├── meta.inf
    │                   ├── meta.sum
    │                   └── o.dat
</code></pre>
<p>NATS systemd startup configuration is as follows:</p>
<pre><code class="language-bash">
$ cat /etc/systemd/system/natsd.service 
[Unit]
Description=natsd.service

[Service]
Type=simple
ExecStart=/usr/bin/nats-server --config /etc/nats/nats.conf
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
</code></pre>

<h1 id="nats-cluster-practice">NATS Cluster Practice</h1>

<h2 id="create-context">Create Context</h2>
<pre><code class="language-shell">$ nats context save computenest-nats --server nats://47.98.102.138:4222,nats://47.98.102.138:4222,nats://47.98.102.138:4222 --description 'ComputeNest NATS Cluster' --select
NATS Configuration Context "computenest-nats"

Description: ComputeNest NATS Cluster
Server URLs: nats://47.98.102.138:4222,nats://47.98.102.138:4222,nats://47.98.102.138:4222
Path: /root/.config/nats/context/computenest-nats.json
Connection: OK

$ nats context ls
╭──────────────────────────────────────────────╮
│                Known Contexts                │
├───────────────────┬──────────────────────────┤
│ Name              │ Description              │
├───────────────────┼──────────────────────────┤
│ computenest-nats* │ ComputeNest NATS Cluster │
│ local             │ Local Host               │
╰───────────────────┴──────────────────────────┘
</code></pre>
<p>All subsequent steps will default to using the ComputeNest NATS cluster configured above.</p>

<h2 id="create-stream">Create Stream</h2>
<pre><code class="language-bash">$ nats stream add my_stream
? Subjects foo
? Storage file
? Replication 3
? Retention Policy Limits
? Discard Policy Old
? Stream Messages Limit -1
? Per Subject Messages Limit -1
? Total Stream Size -1
? Message TTL -1
? Max Message Size -1
? Duplicate tracking time window 2m0s
? Allow message Roll-ups No
? Allow message deletion Yes
? Allow purging subjects or the entire stream Yes

Stream my_stream was created

Information for Stream my_stream created 2023-04-09 08:28:33

             Subjects: foo
             Replicas: 3
              Storage: File

Options:

            Retention: Limits
     Acknowledgements: true
       Discard Policy: Old
     Duplicate Window: 2m0s
    Allows Msg Delete: true
         Allows Purge: true
       Allows Rollups: false

Limits:

     Maximum Messages: unlimited
  Maximum Per Subject: unlimited
        Maximum Bytes: unlimited
          Maximum Age: unlimited
 Maximum Message Size: unlimited
    Maximum Consumers: unlimited


Cluster Information:

                 Name: C1
               Leader: iZbp139ju1kmizva7adgdcZ-172-16-0-157
              Replica: iZbp139ju1kmizva7adgdbZ-172-16-0-155, current, seen 0.00s ago
              Replica: iZbp139ju1kmizva7adgddZ-172-16-0-156, current, seen 0.00s ago

State:

             Messages: 0
                Bytes: 0 B
             FirstSeq: 0
              LastSeq: 0
     Active Consumers: 0
</code></pre>
<p><strong>Note:</strong></p>
<ul>
    <li>Replication is configured to 3, indicating that the created stream has a highly available version with three replicas. NATS implements high availability through data backup based on the RAFT protocol.</li>
</ul>

<h2 id="publish-messages">Publish Messages</h2>
<p>This section uses the <code>nats pub</code> command to publish messages.</p>
<pre><code class="language-bash">$ nats pub foo --count=1000 --sleep 1s "publication #{{Count}} @ {{TimeStamp}}"
 27 / 1000 [====&gt;--------------------------------------------] 26 
</code></pre>

<h2 id="create-consumer">Create Consumer</h2>
<p>To consume messages, you must first create a consumer:</p>
<pre><code class="language-bash">$ nats consumer add
? Consumer name foo_consumer
? Delivery target (empty for Pull Consumers) 
? Start policy (all, new, last, subject, 1h, msg sequence) all
? Acknowledgement policy explicit
? Replay policy instant
? Filter Stream by subject (blank for all) 
? Maximum Allowed Deliveries -1
? Maximum Acknowledgements Pending 0
? Deliver headers only without bodies No
? Add a Retry Backoff Policy No
? Select a Stream my_stream
Information for Consumer my_stream &gt; foo_consumer created 2023-04-09T08:31:23+08:00

Configuration:

        Durable Name: foo_consumer
           Pull Mode: true
      Deliver Policy: All
          Ack Policy: Explicit
            Ack Wait: 30s
       Replay Policy: Instant
     Max Ack Pending: 1,000
   Max Waiting Pulls: 512

Cluster Information:

                Name: C1
              Leader: iZbp139ju1kmizva7adgddZ-172-16-0-156
             Replica: iZbp139ju1kmizva7adgdbZ-172-16-0-155, current, not seen
             Replica: iZbp139ju1kmizva7adgdcZ-172-16-0-157, current, seen 0.00s ago

State:

   Last Delivered Message: Consumer sequence: 0 Stream sequence: 0
     Acknowledgment floor: Consumer sequence: 0 Stream sequence: 0
         Outstanding Acks: 0 out of maximum 1,000
     Redelivered Messages: 0
     Unprocessed Messages: 45
            Waiting Pulls: 0 of maximum 512
</code></pre>

<h2 id="consume-messages">Consume Messages</h2>
<p>After creating the consumer, you can consume data:</p>
<pre><code class="language-bash">$ nats consumer next my_stream foo_consumer --count 1000
[09:05:18] subj: foo / tries: 1 / cons seq: 1 / str seq: 1 / pending: 27

publication #1 @ 2023-04-06T15:17:18+08:00

Acknowledged message

[09:05:18] subj: foo / tries: 1 / cons seq: 2 / str seq: 2 / pending: 26

publication #2 @ 2023-04-06T15:17:19+08:00

Acknowledged message

[09:05:18] subj: foo / tries: 1 / cons seq: 3 / str seq: 3 / pending: 25
...
</code></pre>

<h2 id="multi-instance-consumption">Multi-Instance Consumption</h2>
<p>Multi-instance consumption demonstrates that when multiple instances consume a topic simultaneously, NATS performs load balancing to ensure that each started instance evenly distributes the produced messages. This can be used for load balancing and horizontal scaling of consumers in actual business scenarios.</p>
<p>Consumer Instance 1:</p>
<pre><code class="language-bash">$ nats consumer next my_stream foo_consumer --count 1000
...
[08:33:45] subj: foo / tries: 1 / cons seq: 186 / str seq: 186 / pending: 0

publication #186 @ 2023-04-09T08:33:45+08:00

Acknowledged message

[08:33:47] subj: foo / tries: 1 / cons seq: 188 / str seq: 188 / pending: 0

publication #188 @ 2023-04-09T08:33:47+08:00

Acknowledged message

[08:33:49] subj: foo / tries: 1 / cons seq: 190 / str seq: 190 / pending: 0

publication #190 @ 2023-04-09T08:33:49+08:00

Acknowledged message

[08:33:51] subj: foo / tries: 1 / cons seq: 192 / str seq: 192 / pending: 0

publication #192 @ 2023-04-09T08:33:51+08:00

Acknowledged message
...
</code></pre>
<p>Consumer Instance 2:</p>
<pre><code class="language-bash">$ nats consumer next my_stream foo_consumer --count 1000
[08:33:46] subj: foo / tries: 1 / cons seq: 187 / str seq: 187 / pending: 0

publication #187 @ 2023-04-09T08:33:46+08:00

Acknowledged message

[08:33:48] subj: foo / tries: 1 / cons seq: 189 / str seq: 189 / pending: 0

publication #189 @ 2023-04-09T08:33:48+08:00

Acknowledged message

[08:33:50] subj: foo / tries: 1 / cons seq: 191 / str seq: 191 / pending: 0

publication #191 @ 2023-04-09T08:33:50+08:00

Acknowledged message

[08:33:52] subj: foo / tries: 1 / cons seq: 193 / str seq: 193 / pending: 0

publication #193 @ 2023-04-09T08:33:52+08:00

Acknowledged message
</code></pre>

<h2 id="view-stream-status">View Stream Status</h2>
<pre><code class="language-bash">$ nats stream info my_stream
nats stream info my_stream
Information for Stream my_stream created 2023-04-09 08:28:33

             Subjects: foo
             Replicas: 3
              Storage: File

Options:

            Retention: Limits
     Acknowledgements: true
       Discard Policy: Old
     Duplicate Window: 2m0s
    Allows Msg Delete: true
         Allows Purge: true
       Allows Rollups: false

Limits:

     Maximum Messages: unlimited
  Maximum Per Subject: unlimited
        Maximum Bytes: unlimited
          Maximum Age: unlimited
 Maximum Message Size: unlimited
    Maximum Consumers: unlimited


Cluster Information:

                 Name: C1
               Leader: iZbp139ju1kmizva7adgdcZ-172-16-0-157
              Replica: iZbp139ju1kmizva7adgdbZ-172-16-0-155, current, seen 0.85s ago
              Replica: iZbp139ju1kmizva7adgddZ-172-16-0-156, current, seen 0.85s ago

State:

             Messages: 350
                Bytes: 26 KiB
             FirstSeq: 1 @ 2023-04-09T00:30:38 UTC
              LastSeq: 350 @ 2023-04-09T00:36:30 UTC
     Active Consumers: 1
   Number of Subjects: 1
</code></pre>
<p>Description:</p>
<ul>
    <li>The stream replica count is 3.</li>
    <li>In the cluster information section, you can see that node <code>iZbp139ju1kmizva7adgdcZ-172-16-0-157</code> is the Leader, while the other nodes are Followers.</li>
</ul>
<p>Next, we will shut down the leader node to observe the stream's behavior.</p>

<h2 id="high-availability-verification">High Availability Verification</h2>
<p>By checking the stream status, we found that the leader node of the created stream is "<code>iZbp139ju1kmizva7adgdcZ-172-16-0-157</code>". Now, shut down this node.</p>
<p>Then check the stream status again:</p>
<pre><code class="language-bash">$ nats stream info my_stream
Information for Stream my_stream created 2023-04-09 08:28:33

             Subjects: foo
             Replicas: 3
              Storage: File

Options:

            Retention: Limits
     Acknowledgements: true
       Discard Policy: Old
     Duplicate Window: 2m0s
    Allows Msg Delete: true
         Allows Purge: true
       Allows Rollups: false

Limits:

     Maximum Messages: unlimited
  Maximum Per Subject: unlimited
        Maximum Bytes: unlimited
          Maximum Age: unlimited
 Maximum Message Size: unlimited
    Maximum Consumers: unlimited


Cluster Information:

                 Name: C1
               Leader: iZbp139ju1kmizva7adgddZ-172-16-0-156
              Replica: iZbp139ju1kmizva7adgdbZ-172-16-0-155, current, seen 0.38s ago
              Replica: iZbp139ju1kmizva7adgdcZ-172-16-0-157, outdated, OFFLINE, seen 20.64s ago, 548 operations behind

State:

             Messages: 545
                Bytes: 41 KiB
             FirstSeq: 1 @ 2023-04-09T00:30:38 UTC
              LastSeq: 545 @ 2023-04-09T00:39:46 UTC
     Active Consumers: 1
   Number of Subjects: 1
</code></pre>
<p>It can be seen that in the cluster status, node 156 has become the new Leader, and node 157 status is OFFLINE.</p>
<p>At this time, create a new consumer to re-consume data:</p>
<pre><code class="language-bash">nats consumer add
? Consumer name foo_consumer2
? Delivery target (empty for Pull Consumers) 
? Start policy (all, new, last, subject, 1h, msg sequence) all
? Acknowledgement policy explicit
? Replay policy instant
? Filter Stream by subject (blank for all) 
? Maximum Allowed Deliveries -1
? Maximum Acknowledgements Pending 0
? Deliver headers only without bodies No
? Add a Retry Backoff Policy No
? Select a Stream my_stream

Information for Consumer my_stream &gt; foo_consumer2 created 2023-04-09T08:42:07+08:00

Configuration:

        Durable Name: foo_consumer2
           Pull Mode: true
      Deliver Policy: All
          Ack Policy: Explicit
            Ack Wait: 30s
       Replay Policy: Instant
     Max Ack Pending: 1,000
   Max Waiting Pulls: 512

Cluster Information:

                Name: C1
              Leader: iZbp139ju1kmizva7adgdbZ-172-16-0-155
             Replica: iZbp139ju1kmizva7adgdcZ-172-16-0-157, outdated, not seen
             Replica: iZbp139ju1kmizva7adgddZ-172-16-0-156, current, seen 0.00s ago

State:

   Last Delivered Message: Consumer sequence: 0 Stream sequence: 0
     Acknowledgment floor: Consumer sequence: 0 Stream sequence: 0
         Outstanding Acks: 0 out of maximum 1,000
     Redelivered Messages: 0
     Unprocessed Messages: 685
            Waiting Pulls: 0 of maximum 512
 
$ nats consumer next my_stream foo_consumer2 --count 3
[08:42:27] subj: foo / tries: 1 / cons seq: 1 / str seq: 1 / pending: 703

publication #1 @ 2023-04-09T08:30:38+08:00

Acknowledged message

[08:42:27] subj: foo / tries: 1 / cons seq: 2 / str seq: 2 / pending: 702

publication #2 @ 2023-04-09T08:30:39+08:00

Acknowledged message

[08:42:27] subj: foo / tries: 1 / cons seq: 3 / str seq: 3 / pending: 701

publication #3 @ 2023-04-09T08:30:40+08:00

Acknowledged message
</code></pre>
<p>After the failed node recovers, check the stream status again:</p>
<pre><code class="language-bash">$  nats stream info my_stream
Information for Stream my_stream created 2023-04-09 08:28:33

             Subjects: foo
             Replicas: 3
              Storage: File

Options:

            Retention: Limits
     Acknowledgements: true
       Discard Policy: Old
     Duplicate Window: 2m0s
    Allows Msg Delete: true
         Allows Purge: true
       Allows Rollups: false

Limits:

     Maximum Messages: unlimited
  Maximum Per Subject: unlimited
        Maximum Bytes: unlimited
          Maximum Age: unlimited
 Maximum Message Size: unlimited
    Maximum Consumers: unlimited


Cluster Information:

                 Name: C1
               Leader: iZbp139ju1kmizva7adgddZ-172-16-0-156
              Replica: iZbp139ju1kmizva7adgdbZ-172-16-0-155, current, seen 0.22s ago
              Replica: iZbp139ju1kmizva7adgdcZ-172-16-0-157, current, seen 0.22s ago

State:

             Messages: 780
                Bytes: 58 KiB
             FirstSeq: 1 @ 2023-04-09T00:30:38 UTC
              LastSeq: 780 @ 2023-04-09T00:43:43 UTC
     Active Consumers: 2
   Number of Subjects: 1
</code></pre>
<p>It can be seen that all three nodes in the stream's cluster information have returned to an available state. The previously abnormal node 2 has recovered and automatically became a follower after joining the cluster of the two healthy nodes.</p>

<h1 id="next-steps">Next Steps</h1>
<p>NATS is gradually evolving into an ecosystem with many features to practice and demonstrate, including but not limited to:</p>
<ul>
    <li><strong>Security Authentication</strong>: Supports Token, user/pass, TLS, NKEY, JWT, and other security configurations.</li>
    <li><strong>Connection Protocols</strong>: In addition to the default NATS connection protocol, it also supports WebSocket and MQTT connections, and traffic from other messaging systems can be transferred to NATS via Kafka Bridge JMS.</li>
    <li>JetStream <a href="https://docs.nats.io/nats-concepts/jetstream">More Features</a>: JetStream is the latest generation high-availability streaming system of NATS, supporting many advanced features:
        <ul>
            <li>Stream replay policies</li>
            <li>Streaming storage</li>
            <li>Retention policies</li>
            <li>Message quotas</li>
            <li>Persistence</li>
            <li>Stream Mirror</li>
            <li>End-to-end flow control</li>
            <li>Exactly-Once semantic support</li>
        </ul>
    </li>
    <li><strong>Multi-Tenant Management</strong>: Multi-tenant account configuration management based on the <a href="https://docs.nats.io/using-nats/nats-tools/nsc">nsc</a> tool.</li>
    <li><strong>Edge Scenarios</strong>: To support edge computing and IoT scenarios, NATS supports deploying local NATS clusters at the edge to interact with central clusters. This allows edge devices to quickly produce business data by connecting to the local edge cluster without strongly relying on the network stability with the remote central cluster. See <a href="https://docs.nats.io/running-a-nats-service/configuration/leafnodes">Edge Scenario Reference</a>.</li>
</ul>

</body>
</html>
