## "The Redapt Rancher POC" (alpha)
This is a non-client repo of the Rancher Proof of Concept (POC). This is, this repo does not have a specific client of Redapt in mind. The idea for this repo is to have it as an example Rancher POC to show any customer. It should always have the latest version of Rancher configured.

by Christoph Champ, Redapt, Inc. (January 2017)
<p><small>last updated: 2017-01-25</small></p>

## Requirements

### Local host
The Ansible playbooks are expecting the following packages and versions to be installed on the host (the Jenkins server, in this case) the playbooks will be run from:
* Ansible v2.2.x (tested on 2.2.1.0)
* Python v2.7.x (tested on 2.7.12)
* pip packages:
 * awscli==1.11.42
 * aws-adfs==0.2.0 (only needed for interacting with the AWS accounts sans IAM user accounts)
 * boto==2.45.0
 * boto3==1.4.4
 * botocore==1.5.5

NOTE: Below is an example of how to use `aws-adfs` for AWS accounts without IAM user accounts:
```
aws-adfs login --adfs-host aws-sso.example.com --profile nonprod
```

### EC2 instances
The remote hosts (EC2 instances) that will be running Rancher and/or Kubernetes will have the following packages and versions installed automatically by the related playbooks:
* Rancher v1.3.3
* Docker v1.12.x
* LVM2

There will also be some extra sysadmin-related packages useful for troubleshooting installed. For a complete list, see `roles/sysadmin/tasks/main.yml`

### Rancher / Kubernetes / Docker Compatibility Matrix

See [Compatibility Matrix](http://rancher.com/support-maintenance-terms/) for details.

| Rancher Version | Release Date | Host OS                                              | Kubernetes             | Docker        |
|-----------------|--------------|------------------------------------------------------|------------------------|---------------|
| 1.3.1           | 2017-01-13   | Ubuntu 14.04/16.04; RHEL/CentOS 7.x; RancherOS 0.7.1 | 1.4.6                  | 1.12.x        |
| 1.2.2           | 2016-12-01   | Ubuntu 14.04/16.04; RHEL/CentOS 7.x; RancherOS 0.7.1 | 1.4.6                  | 1.12.x        |
| 1.1.4           | 2016-06-30   | Ubuntu 14.04/15.10; RHEL/CentOS 7.x; RancherOS 0.5.0 | 1.2.4 + Docker 1.10.3<sup>$</sup> | 1.10.x 1.11.x |
| 1.0.2           | 2016-03-28   | Ubuntu 14.04/15.10; RHEL/CentOS 7.x; RancherOS 0.4.0 | 1.2.4                  | 1.10.3        |
<sup>$</sup> Kubernetes support is pinned to a specific version of Docker.

* [Rancher v1.2.3](https://github.com/rancher/rancher/releases/tag/v1.2.3) services/versions:
 * rancher/server:v1.2.3
 * rancher/agent:v1.1.2
 * rancher/lb-service-haproxy:v0.4.6
 * rancher-compose-v0.12.1
 * rancher-v0.4.1
* [Rancher v1.3.3](https://github.com/rancher/rancher/releases/tag/v1.3.3) services/versions:
 * rancher/server:v1.3.3
 * rancher/agent:v1.1.3
 * rancher/lb-service-haproxy:v0.4.9
 * rancher-compose-v0.12.1
 * rancher-v0.4.1

Starting with version 1.2.0, Rancher no longer supports AWS ELBs and only supports AWS ALB (Application Load Balancers). UPDATE: With Rancher 1.2.3, Rancher has re-introduced being able to [use ELBs with this release](http://docs.rancher.com/rancher/v1.2/en/installing-rancher/installing-server/#elb).
