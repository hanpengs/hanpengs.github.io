# MongoDB Alert

When you use Whaleal to manage a host for the first time, Whaleal will detect that the host is a new host and initialize it. The alarm method directly inherits the alarm indicators in the current project. If you want to configure different alarm indicators in the project, you can select the host where the server is located in the MongoDB drop-down box in MongoDB Alert and configure it separately.

## Select Project

1. Click Alert in the navigation bar.
2. Click MongoDB Alert on the Alert Message page.
3. In the MongoDB drop-down box, select the server for which you want to configure an alarm.

![image-20240628171055358](../images/09-Alert/MongoDBAlert.png)

## Indicator Configuration

After selecting the target hsot, the configuration options shown in the following picture may appear.

![image-20240628171055358](../images/09-Alert/MongoDBAlertConfig.png)

Configuration items：

| Alert Strategy Type      | Time interval: To count indicators over a period of time, you need to configure the start time and end time in Statistics Granularity/S.<br/> Continuous Time: Configure the indicator statistics within a continuous time, which counts the indicator value at the current time. |
| ------------------------ | ------------------------------------------------------------ |
| If Item                  | Configure specific Alert indicators here                     |
| Statistics Granularity/S | Configure the granularity of statistics. If the granularity is too large, you may ignore the fact that the Alert indicator is too high at a certain point in time. |
| Trigger Condition        | Configure indicator values according to plan">","<","=",">=" ,or "<=". |
| Trigger Value            | Alert trigger value. When the Alert indicator value configured in the If Item reaches this value, an alarm will be triggered. |
| Trigger Count            | The number of times the alarm is triggered within the time configured in then Alert Frequency/M |
| then Alert Frequency/M   | Control alarm frequency                                      |



## Send alerts

When the alarm value is triggered, we can see the current alarm in open Alert, and we can search in MSG or configure the time interval to view the alarm within a period of time.

![image-20240628171055358](../images/09-Alert/MongoDBAlertapp.png)

Alert will also send the alert to a specific platform through the information configured in the alert platform configured in Groups in the Project. For the configuration process, refer to [Project Alert](./03-ProjectAlert.md).

