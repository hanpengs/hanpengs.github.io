# Case

#### The agent.gz package has a problem and cannot be downloaded.
Server-web did not start properly.



#### The new version of the configuration file is named after the port, and the previous one is in the form of ip+port. Do you need to manually modify the configuration file name of the old cluster?

The old cluster does not need to be modified and will not be affected.



#### Monitoring indicator = 'cpuInfo_id' this corresponds to: user cpu?

No, Id stands for cpu idle rate.



#### More than 60% in 60 seconds, will the alarm be triggered 10 times, but this value is not more than 40% at present, but it has been reported all the time.

Within 60s, if the cpu utilization rate is greater than 60% and occurs ten times, the alarm will be triggered. Once the alarm message is sent every 10 minutes, the alarm message will be sent with a granularity of 1 minute. In this case, the average cpu utilization rate within one minute is 40%. Click real-time to see the cpu information at the seconds level.



#### Use the latest version of prometheus to collect Datagram errors. Whether it is related to the version relationship ts=2024-04-08T03:51:34.306Z caller=refresh.go:90 level=error component= "" discovery manager scrape "" discovery=http config=wap-monitor msg= "" Unable to refresh target groups "" err= "" invalid character 'W'looking for beginning of value ""

The prometheus configuration file tries this approach.
```
job_name: wap-monitor
scrape_interval: 10s
metrics_path: '/api/server/mongo/getMongoDBForPrometheus'
params:
  id: ["public"]
  type: ["project"]
basic_auth:
  username: 'admin'
  password: xxxxx
static_configs:

  - targets: ['172.xx.xx.xx:8080']
    labels:
      instance: wap
```



#### At present, after the monitoring is turned on, is the frequency of monitoring once per second? can you define the time frequency by yourself?
You can adjust it yourself and monitor the granularity in setting.



#### The whaleal-mongodb-log file is so large that the disk is full and the mongo service cannot be started. Won't he clean it up himself? Do you have to clean it manually every time?

What is saved in whaleal-mongodb-log can be cleared from the logs of mongoDB nodes. By default, save for one month. Configure the saving time of mongodb logs in the setting page.



#### In the logic of deploying mongo, is there a default log level of 3, frequent mongo.log refresh, is there any relationship between opening monitoring and enabling log monitoring in the platform?

It's a cpython connection. Our agent doesn't involve Python stuff.



#### The monitoring information cannot be viewed. The mongo log has just been cut by the hour. Does this matter?

The MongoDB log has nothing to do with this. This general situation is caused by the network. Delete all the host alarm policies configured on this host and see if there is any monitoring data.



#### Prometheus configures multiple project gathering to report an error.

Only one project can be configured at a time.



#### After using the cluster rename, only the cluster display has changed, and the name of the replica set of the cluster will not change, will it?

The cluster name will not change.



#### What data is stored in Nacos? Will the loss of the data catalog affect the service?

Store the routing information of the java service. Nacos does not save data and can be rebuilt.



#### When backing up, the DDT host randomly selects which node to back up from. Is it possible for him to choose the hidden node? If he selects the slave node, will the cpu be very high?

DDT is a server used to perform backup tasks. It is completed by executing the JAVA backup process. Try not to place this on the server where MongoDB is located. Try to add an extra server to do backup. The backup operation does not consume much CPU on the source side, which is equivalent to performing a query operation. There will be a little stress during the first full backup.



#### There is a problem with backup configuration S3

If the bucket name is filled in incorrectly, create a backup policy and refresh the page according to the new configuration. After this key is triggered once, the backend will re-encrypt the key, so there is a problem with the connection, so you need to re-enter key accesskey.



#### After the agent server is restarted, you need to start the agent process manually

Use the agent script to configure agent to serve the system and set up boot self-boot.



#### When converting from a replica architecture to a fragmented architecture, all of them are on the same group of machines (in the form of multiple instances). When converting to a fragmented architecture, will it be different when allocating memory? If not, will it simply oom? When allocating memory, he won't know whether it is multiple instances or 50% of physical memory?

When the amount of data is large, it will oom. If not set by default in platform, MongoDB defaults to 50% of the physical memory.



#### After the backup strategy is created, when is its trigger time? this can be seen there.

After the first creation, you can go to the source MongoDB event group to check the progress.



#### What configuration is recommended for DDT hosts?

DDT recommends high CPU, 8C+ 16GB+



#### What is the DDT backup logic like?

This is how DDT works in real time: https://docs.whaleal.com/guide/en/documentDataTransfer/Introduction/Architecture.html.



#### Will the process above DDT be retained all the time, so that if there are more instances, there will be many such process on ddt machines?

There are two processes during a DDT backup. After the full backup is completed, the full DDT process exits, leaving a DDT process that synchronizes the oplog synchronized in real time.



#### If there is a ddt host to configure backup tasks, is there a place to configure the time to avoid time conflicts.

Currently, custom times are not supported, but if you want to achieve the effect of avoiding time conflicts, different MongoDB clusters can also be created at different times when the backup policy is first configured.



#### There is a problem with ddt backup  "Cannot allocate memory (errno=12)"

All DDT processes died, DDT died due to insufficient memory.



#### Use WAP marketplace to start platform services through mirroring, but the service process did not start successfully? Do I still need to deploy it manually?

The EC2 server cannot connect to the external network, causing the script not to run



#### How did the machines in server be added to project? no machines can be added to the project now. After clicking on the project on the platform, they are all empty.

All the newly added hosts are on public.
1. Configuration file "parameters.properties" in / opt/agent after the agent instance is started
Write foreign_url= parameters in the format foreign_url= http://54.175.147.38:8080
2. Execute the command after configuration to check whether the process starts "systemctl status whaleal_agent"
Wait about 30 seconds after startup
3. All launched agent hosts will be in public project by default.
You can create a new Project, remove the hosts from the public and put them in the new public.
4. You can create a MongoDB cluster based on Project



#### The ddt machine used for synchronization does not have agent. This does not affect data synchronization, can I just configure mong on it?

If you don't use backup features on the platform, there will be no impact.



#### Do you want to write all the sourceDsUrl addresses configured by DDT, or just write the main node?

Both are fine. Master node, slave node, and cluster URI are all available, or only slave nodes can be configured to relieve the pressure on the master node



#### Backup issu，In configuration:

1. Full volume and real-time
2. Full volume and increment
Do these two mean the same?
I want to synchronize all the data now. After the synchronization of all the data is completed, I need to continue to synchronize incremental data. Which configuration should I use?
Full and real-time: full oplog (full start time to positive infinite time)
Full and incremental: full oplog (full start time to full end time)



#### After mongoDB was separated from the platform, the mongo process on the host also stopped. Do you need other pre-work to deploy MongoDB again with this machine?

Start the MongoDB service, and the data directory is different from the previous data directory.



#### The DDT server used for data synchronization does not have an Agent installed. Will it affect data synchronization? Can I directly deploy and configure MongoDB? If I need to use the backup function later, how should I restore it to the original DDT?

Does not affect data synchronization.
If the DDT server is subscribed by marketplace's agent
DDT machine clears data, services
Start the agent of the ddt machine and put it in the Project called DDT
Just start the backup normally.
If the DDT server is not created by subscription, you cannot use the backup function in wap.



#### DDT has an error. I configured ddt yesterday, ran for a while, then stopped, ran again today, and started in the following order: start-DDT.sh start-moitor.sh

If you see the log error report, it should be started repeatedly [tool for monitoring DDT synchronization]
DDT has two processes:

1. DDT synchronization MongoDB data tool
2. tools for monitoring DDT synchronization (this tool uses web and spring JAR)

If you execute start-all.sh, you will start both processes.
If you execute start-DDT.sh, only start the DDT synchronization data tool



#### Data check. DDT synchronization data destination is missing.

If the table is a dynamic table (operating in real time)
There will be data inconsistencies, and dynamic tables can be checked many times to determine data consistency.
Db.ns.count is a fuzzy calculation, sometimes because of cache and other problems, the amount of data may not be correct.
Can be used on the target side: use the exact count to view the number of library table documents db.ns.countDocuments ({})



#### Deploy another cluster and copy a ddt directory. You can run both of them. For example, project a is synchronized. Now project b needs to be migrated, and start two ddt at the same time.

DDT startup script needs to be modified. It is not supported by default.
The second DDT must be in a new directory
Then you can start run: 

```
nohup java-Xmx$max_heap_size-jar ../execute-1.0-SNAPSHOT.jar ../config/DDT.properties > /dev/null 2 > &1 & 
```



#### Help me confirm that DDT is synchronizing data in real time. If we want to switch the connection to a new cluster, can we replace it directly, or do we have to disconnect DDT synchronization first, stop business, stop DDT, and finally replace the connection URL?

Stop the business first, then stop the DDT service, and then replace the connection URL. This is the recommended action step and needs to be operated within the shutdown maintenance window.



#### If both the source and target sides of DDT synchronization have write operations, will DDT synchronization have an impact?

In this way, the data on the source side and the destination side will be inconsistent.