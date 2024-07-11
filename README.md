
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
7. A

```
