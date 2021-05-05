# cfn-helper-script-bootstraping

#### Overview
This project provides cloudformation automation template to bootstrap an Amazon EC2 instance using cloudformation helper scripts and cloudformation meta data.
Using Cloudformation helper scripts provides the following benefits

### cfn-init and meta-data
cfn-init helper script can be used to read meta data from "AWS::CloudFormation::Init" to bootstrap an EC2 instance. "cfn-init" helper script is executed from user-data. meta data can be used to configure the following
•	Packages to be installed along with their versions

•	Download software archives from an external source and unpackage them 

•	Create files on the EC2 instance. Contents for the files can be specified in-line or can be pulled from an URL

•	Create Users and Groups at the operating system level

•	Enable/disable and start/stop services at the operating system level


### Creation Policy and signal
when you bootstrap an EC2 instance using user-data scripts, the scripts is executed by the operating system. Cloudformation execution does not wait for the scripts to finish its execution and it does not check for the status of the execution. So even if there is any failure in the user-data script execution, the cloudformation resource will be marked as "CREATE COMPLETE".
Cloudformation "creationpolicy" can be configured to wait for a signal. "cfn-signal" helper script can be used to send success or failure signal to be creation policy. 

### Configuration Updates
User-data scripts gets executed only once when an EC2 instance gets created. Any changes to the user- data scripts will not be executed again as part of the cloudformation update. 
"cfn-hup" helper daemon can be configured to detect the changes to the meta data. This allows you to make configuration changes on the existing EC2 instances during cloudformation update process
