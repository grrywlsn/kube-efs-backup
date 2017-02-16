# kube-efs-backup

Kubernetes Docker container to backup EFS to S3 on schedule.

#### about the container

We like running Kubernetes with EFS, but we wanted a nice way to maintain backups of the file system.

This Docker container is designed to run as a simple CronJob / ScheduledJob within Kubernetes, to allow us to backup EFS to S3 on schedule.

You can set the backup schdule within the Kubernetes yaml; the only things you need to pass to the Docker container are the source directory (the EFS point) and the S3 bucket in which to copy it to.

#### usage

see the scheduledjob.yaml on how to deploy container to Kubernetes:

- ***required*** update the NFS server to match the EFS id/region for your account
- ***required*** update the S3_DIR env variable to the S3 bucket name for backups
- ideally, pass S3 bucket write access in via IAM role on the ec2 instance
- use lifecycle policies on the S3 bucket for a nice, reliable way to manage backup retention
