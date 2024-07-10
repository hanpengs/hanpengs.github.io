# Frequently Asked Questions

This page contains answers to frequently asked questions about WAP.

1. **Can I reset my password?**

   The password can be reset, but only users with admin privileges can perform this operation

2. **Can the host under a project be moved to another project?** 

   Yes, you need to move it out of the old project before moving it to another project.

3. **What types of deployment can I create in WAP?**

   Using WAP, you can configure all MongoDB deployment types: sharded clusters, replica sets, and standalones.

4. **Is the monitoring frequency once per second? Can I define the time frequency myself?**

   You can adjust it yourself, in the **settings**, monitor the granularity.

5. **After configuring the alert rules, how can I receive the alert information?**

   When the alert condition is configured and the alert is triggered, the alert information can be notified via email, DingTalk, SMS, etc.

6. **What MongoDB versions does WAP support?**

   WAP supports 98% of MongoDB on the market, and supports versions 5.0 to 7.0.

7. **Does WAP support changes to the MongoDB cluster architecture?**

   Currently supported mongodb architecture changes include single-machine conversion to replica set, replica set conversion to sharding

8. **What MongoDB authentication methods are supported?**

   Currently supported authentication methods include account and password, account and password and CA certificate

9. **After the agent server is restarted, do you need to manually start the agent process?**

   The agent startup script will configure the agent as a system service and set it to start automatically at boot

10. **Is the node shut down when it leaves the management?**

    When a cluster is removed from management, it is not managed or displayed on the platform, but is not shut down on the host. Deleting a node means shutting down the node.

11. **How to receive alerts after configuring them?**

    When the start is triggered after the start conditions are configured, the start information will be notified via email, DingTalk, SMS, etc.

12. **Does mongo support synchronization?**

    Support, you can use the backup and restore function to synchronize data

13. **What is the principle of horizontal expansion of WAP platform?**

    Horizontal expansion is to build multiple WAP services. The Agents managed by the same appdb can be hashed and assigned to different WAP services to reduce the pressure on a single WAP. When a WAP service fails, other WAP services are not affected. The affected agents will be re-hashed and assigned to healthy WAP services.

14. **How long will the oplog be stored?**

    Depends on the number of recovery days configured by the user, with a maximum retention period of half a year and a minimum retention period of one day

15. **Can the Home page be searched and displayed based on the cluster name?**

    The home page does not allow you to select a cluster for display. You can only view monitoring information for a specific cluster on the MongoDB page.



