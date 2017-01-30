# aws-cloudwatch-logs

One of the easiest ways to get logs from distributed systems running on AWS. Some tips and tricks.

## Unattended install on non AWS Linux Systems

```bash
# Create a folder to hold our AWS logs config.
mkdir -p /var/awslogs/etc

# Download and run the AWS logs agent.
curl https://s3.amazonaws.com/aws-cloudwatch/downloads/latest/awslogs-agent-setup.py -O
python ./awslogs-agent-setup.py --non-interactive  --region us-east-1 -c /var/awslogs/etc/awslogs.conf

# Configure the logs.
# e.g: Create a the awslogs config.
cat >> /var/awslogs/etc/awslogs.conf <<- EOF
[/var/log/user-data.log]
file = /var/log/user-data.log
log_group_name = /var/log/user-data.log
log_stream_name = {instance_id}
EOF

# Start the awslogs service, also start on reboot.
# Note: Errors go to /var/log/awslogs.log
service awslogs restart
chkconfig awslogs on
```
