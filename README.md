
# Cloud watch agent installation

Steps to insatll cloud watch agent


## 1. Create a IAM role for EC2 Instance

```bash
  * Create a Windows EC2 Instances in Running state *

  Go to IAM > Roles > Create role
  1. AWS services.
  2. Use case: EC2 > next
  3. Select CloudwatchAgentAdminPolicy,CloudwatchAgentServerPolicy, AmazonSSMFullAccess, AmazonSSMManageInstanceCore > next
  4. Role Name:  
```

## 2. Attach the role to EC2 Instance

```bash
Select the Instance > action > Security > Modify IAM role > Select the role which created.
```

## 3. Install CloudWatch agent using System manager

```bash
* Cross check the Instance in Fleet Manager *
1. run command
2. Command Document: AWS-ConfigureAWSPackage.
3. Command parameter:
    -Name: AmazonCloudWatchAgent.
    -Version: Latest
4. Target Selection: Choose Instances Manually
  (Slect the Instance)   

  Run 
```
## 4. Configure Cloud Watch Agent
```bash
Take RDP of the Instance

Cross cheak
1. Thispc > C:\ > programfiles > Amazon > AmazonCloudWatchAgent 
2. Copy the folloing path C:\ > programfiles > Amazon > AmazonCloudWatchAgent 
3. Open cmd as a administrator.
4. cd C:\ > programfiles > Amazon > AmazonCloudWatchAgent 
5. dir Enter.
6. amazon-cloudwatch-agent-config-wizard.exe 
```

## 5. Outputs

```bash
C:\Program Files\Amazon\AmazonCloudWatchAgent>amazon-cloudwatch-agent-config-wizard.exe
================================================================
= Welcome to the Amazon CloudWatch Agent Configuration Manager =
=                                                              =
= CloudWatch Agent allows you to collect metrics and logs from =
= your host and send them to CloudWatch. Additional CloudWatch =
= charges may apply.                                           =
================================================================
On which OS are you planning to use the agent?
1. linux
2. windows
3. darwin
default choice: [2]:
2
Trying to fetch the default region based on ec2 metadata...
I! imds retry client will retry 1 timesAre you using EC2 or On-Premises hosts?
1. EC2
2. On-Premises
default choice: [1]:
1
Do you want to turn on StatsD daemon?
1. yes
2. no
default choice: [1]:
1
Which port do you want StatsD daemon to listen to?
default choice: [8125]

What is the collect interval for StatsD daemon?
1. 10s
2. 30s
3. 60s
default choice: [1]:
1
What is the aggregation interval for metrics collected by StatsD daemon?
1. Do not aggregate
2. 10s
3. 30s
4. 60s
default choice: [4]:
2
Do you have any existing CloudWatch Log Agent configuration file to import for migration?
1. yes
2. no
default choice: [2]:
2
Do you want to monitor any host metrics? e.g. CPU, memory, etc.
1. yes
2. no
default choice: [1]:
1
Do you want to monitor cpu metrics per core?
1. yes
2. no
default choice: [1]:
1
Do you want to add ec2 dimensions (ImageId, InstanceId, InstanceType, AutoScalingGroupName) into all of your metrics if the info is available?
1. yes
2. no
default choice: [1]:
1
Do you want to aggregate ec2 dimensions (InstanceId)?
1. yes
2. no
default choice: [1]:
1
Would you like to collect your metrics at high resolution (sub-minute resolution)? This enables sub-minute resolution for all metrics, but you can customize for specific metrics in the output json file.
1. 1s
2. 10s
3. 30s
4. 60s
default choice: [4]:
2
Which default metrics config do you want?
1. Basic
2. Standard
3. Advanced
4. None
default choice: [1]:
2
Current config as follows:
{
        "metrics": {
                "aggregation_dimensions": [
                        [
                                "InstanceId"
                        ]
                ],
                "append_dimensions": {
                        "AutoScalingGroupName": "${aws:AutoScalingGroupName}",
                        "ImageId": "${aws:ImageId}",
                        "InstanceId": "${aws:InstanceId}",
                        "InstanceType": "${aws:InstanceType}"
                },
                "metrics_collected": {
                        "LogicalDisk": {
                                "measurement": [
                                        "% Free Space"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "Memory": {
                                "measurement": [
                                        "% Committed Bytes In Use"
                                ],
                                "metrics_collection_interval": 10
                        },
                        "Paging File": {
                                "measurement": [
                                        "% Usage"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "PhysicalDisk": {
                                "measurement": [
                                        "% Disk Time"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "Processor": {
                                "measurement": [
                                        "% User Time",
                                        "% Idle Time",
                                        "% Interrupt Time"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "statsd": {
                                "metrics_aggregation_interval": 10,
                                "metrics_collection_interval": 10,
                                "service_address": ":8125"
                        }
                }
        }
}
Are you satisfied with the above config? Note: it can be manually customized after the wizard completes to add additional items.
1. yes
2. no
default choice: [1]:
1
Do you want to monitor any customized log files?
1. yes
2. no
default choice: [1]:
1
Log file path:
/var/log/app.log
Log group name:
default choice: [app.log]

Log group class:
1. STANDARD
2. INFREQUENT_ACCESS
default choice: [1]:

Log stream name:
default choice: [{instance_id}]

Log Group Retention in days
1. -1
2. 1
3. 3
4. 5
5. 7
6. 14
7. 30
8. 60
9. 90
10. 120
11. 150
12. 180
13. 365
14. 400
15. 545
16. 731
17. 1096
18. 1827
19. 2192
20. 2557
21. 2922
22. 3288
23. 3653
default choice: [1]:
5
Do you want to specify any additional log files to monitor?
1. yes
2. no
default choice: [1]:
2
Do you want to monitor any Windows event log?
1. yes
2. no
default choice: [1]:
2
Do you want the CloudWatch agent to also retrieve X-ray traces?
1. yes
2. no
default choice: [1]:
2
Existing config JSON identified and copied to:  C:\Users\Administrator\AppData\Roaming\Amazon\CloudWatchAgent\etc\backup-configs
Saved config file to config.json successfully.
Current config as follows:
{
        "logs": {
                "logs_collected": {
                        "files": {
                                "collect_list": [
                                        {
                                                "file_path": "/var/log/app.log",
                                                "log_group_class": "STANDARD",
                                                "log_group_name": "app.log",
                                                "log_stream_name": "{instance_id}",
                                                "retention_in_days": 7
                                        }
                                ]
                        }
                }
        },
        "metrics": {
                "aggregation_dimensions": [
                        [
                                "InstanceId"
                        ]
                ],
                "append_dimensions": {
                        "AutoScalingGroupName": "${aws:AutoScalingGroupName}",
                        "ImageId": "${aws:ImageId}",
                        "InstanceId": "${aws:InstanceId}",
                        "InstanceType": "${aws:InstanceType}"
                },
                "metrics_collected": {
                        "LogicalDisk": {
                                "measurement": [
                                        "% Free Space"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "Memory": {
                                "measurement": [
                                        "% Committed Bytes In Use"
                                ],
                                "metrics_collection_interval": 10
                        },
                        "Paging File": {
                                "measurement": [
                                        "% Usage"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "PhysicalDisk": {
                                "measurement": [
                                        "% Disk Time"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "Processor": {
                                "measurement": [
                                        "% User Time",
                                        "% Idle Time",
                                        "% Interrupt Time"
                                ],
                                "metrics_collection_interval": 10,
                                "resources": [
                                        "*"
                                ]
                        },
                        "statsd": {
                                "metrics_aggregation_interval": 10,
                                "metrics_collection_interval": 10,
                                "service_address": ":8125"
                        }
                }
        }
}
Please check the above content of the config.
The config file is also located at config.json.
Edit it manually if needed.
Do you want to store the config in the SSM parameter store?
1. yes
2. no
default choice: [1]:
1
What parameter store name do you want to use to store your config? (Use 'AmazonCloudWatch-' prefix if you use our managed AWS policy)
default choice: [AmazonCloudWatch-windows]

Trying to fetch the default region based on ec2 metadata...
I! imds retry client will retry 1 timesWhich region do you want to store the config in the parameter store?
default choice: [ap-south-1]

Which AWS credential should be used to send json config to parameter store?
1. ASIAYCZKUJSBSVZ7M4MZ(From SDK)
2. Other
default choice: [1]:

Successfully put config to parameter store AmazonCloudWatch-windows.
Please press Enter to exit...

Program exits now.

C:\Program Files\Amazon\AmazonCloudWatchAgent>
```
## 7. links

```bash
https://youtu.be/NVfbUbfpsvw?si=zUGamMjYmcggZW0H
```
