#Install Cloudwatch unified agent on EC2 instance. Gather Custom Metrics using Amazon Linux AMI
```
1) First of all create required IAM roles for the EC2 instances to be able to send metrics to cloudwatch

In the list of policies while creating IAM Role for EC2 Instance, select the check box next to CloudWatchAgentServerPolicy. Use the search box to find the policy, if necessary.

2) Launch an EC2 instance with port 80 and 22 open in the security group.

3) SSH into the instance

4) Find the cloudwatch agent download link here: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-first-instance.html

5) Download the Cloudwatch Unified Agent. Find the right agent link for your OS by visiiting the above link

wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm

6) Install the Cloudwatch Agent
sudo rpm -U ./amazon-cloudwatch-agent.rpm
7) Configure the Cloudwatch agent with the help of a setup wizard:

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard

Choose all the default option except don't install statd and collectd. Selecy YES when asked to collect Memory Utilization metric. Select NO when asked if you want to monitor log files.

8)Start the agent
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```
