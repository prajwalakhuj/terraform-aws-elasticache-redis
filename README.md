## Redis
![squareops_avatar]

[squareops_avatar]: https://squareops.com/wp-content/uploads/2022/12/squareops-logo.png

### [SquareOps Technologies](https://squareops.com/) Your DevOps Partner for Accelerating cloud journey.
<br>
This module is a Terraform module that provides an easy and efficient way to deploy and manage an Amazon ElastiCache Redis cluster in AWS. It simplifies the process of setting up a Redis cluster with customizable configurations, allowing you to focus on your application development and performance optimization.
Features

  1. Simple Configuration: The module offers a simple and intuitive configuration interface, allowing you to define your Redis cluster's properties, such as instance type, node count, subnet, security groups, and more.

  2. Scalability: Easily scale your Redis cluster up or down by modifying the number of cache nodes, enabling you to meet the changing demands of your application.

  3. High Availability: Enable multi-AZ deployment to achieve high availability and automatic failover in case of a node or zone failure. This ensures that your Redis cluster remains accessible and your data stays protected.

  4. Flexible Networking: Choose the VPC and subnets where you want to deploy your Redis cluster, providing you with control over network access and integration with other resources in your AWS environment.

  5. Encryption and Security: Enable encryption at rest with your own KMS key or use AWS-managed encryption. Control access to your Redis cluster using CIDR blocks and security groups, ensuring secure communication and data protection.

  6. Backup and Recovery: Configure automated daily snapshots and set the retention period for backups. You can also specify a final snapshot for a smooth and controlled cluster termination process.

  7. Logging and Monitoring: Easily configure logging destinations for slow logs and engine logs, allowing you to monitor the performance and troubleshoot any issues efficiently.

## Uses Example

```hcl

module "redis" {
  source          = "squareops/elasticache-redis/aws"  
  environment     = "production"
  name            = "redis"
  family          = "redis6.x"
  vpc_id                     = "vpc-06eb7eskaf"
  subnets                    = ["subnet-0bfa3eskaf","subnet-0140bskaf"]
  node_type                  = "cache.t3.small"
  kms_key_arn                = "arn:aws:kms:us-east-2:222222222222:key/kms_key_arn"
  num_cache_nodes            = 2
  engine_version             = "6.x"
  multi_az_enabled           = false
  availability_zones         = 2
  automatic_failover_enabled = true
  snapshot_retention_limit   = 7
  at_rest_encryption_enabled = true
  transit_encryption_enabled = false
  notification_topic_arn     = null
  allowed_security_groups    = [sg-0132a18skaf]
  snapshot_window            = "07:00-08:00"
  maintenance_window         = "sun:09:00-sun:10:00"
}

```
Refer [examples](https://github.com/squareops/terraform-aws-elasticache-redis/tree/main/examples/complete) for more details.

 ## IAM Permissions
The required IAM permissions to create resources from this module can be found [here](https://github.com/squareops/terraform-aws-elasticache-redis/blob/main/IAM.md)

## Important Note
1. By default, the variable `create_random_password` is set to true. Therefore, even if the user provides a password, it will not be read. The `create_random_password` variable should be set to false and the `password` variable should have a non-null value to be read and used.

## Security & Compliance [<img src="	https://prowler.pro/wp-content/themes/prowler-pro/assets/img/logo.svg" width="250" align="right" />](https://prowler.pro/)

Security scanning is graciously provided by Prowler. Proowler is the leading fully hosted, cloud-native solution providing continuous cluster security and compliance.

| Benchmark | Description |
|--------|---------------|
| Ensure that encryption is enabled for RDS instances | Enabled for RDS created using this module. |

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 4.23 |
| <a name="requirement_random"></a> [random](#requirement\_random) | >= 3.0.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 4.23 |
| <a name="provider_random"></a> [random](#provider\_random) | >= 3.0.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_security_group_redis"></a> [security\_group\_redis](#module\_security\_group\_redis) | terraform-aws-modules/security-group/aws | 4.13.0 |

## Resources

| Name | Type |
|------|------|
| [aws_elasticache_parameter_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticache_parameter_group) | resource |
| [aws_elasticache_replication_group.redis](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticache_replication_group) | resource |
| [aws_elasticache_subnet_group.elasticache](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticache_subnet_group) | resource |
| [aws_secretsmanager_secret.secret_redis](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret) | resource |
| [aws_security_group_rule.cidr_ingress](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.default_ingress](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [random_password.password](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/password) | resource |
| [aws_availability_zones.available](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/availability_zones) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_allowed_cidr_blocks"></a> [allowed\_cidr\_blocks](#input\_allowed\_cidr\_blocks) | A list of CIDR blocks which are allowed to access the database | `list(any)` | `[]` | no |
| <a name="input_allowed_security_groups"></a> [allowed\_security\_groups](#input\_allowed\_security\_groups) | A list of Security Group ID's to allow access to | `list(any)` | `[]` | no |
| <a name="input_at_rest_encryption_enabled"></a> [at\_rest\_encryption\_enabled](#input\_at\_rest\_encryption\_enabled) | (Optional) Whether to enable encryption at rest | `bool` | `true` | no |
| <a name="input_automatic_failover_enabled"></a> [automatic\_failover\_enabled](#input\_automatic\_failover\_enabled) | Enable automatic failover | `bool` | `true` | no |
| <a name="input_availability_zones"></a> [availability\_zones](#input\_availability\_zones) | The no. of AZs | `string` | `2` | no |
| <a name="input_engine_log_destination"></a> [engine\_log\_destination](#input\_engine\_log\_destination) | The destination for engine logs(eg. Cloudwatch log-group name or kinesis firehose stream name) | `string` | `null` | no |
| <a name="input_engine_log_destination_type"></a> [engine\_log\_destination\_type](#input\_engine\_log\_destination\_type) | The type of destination for engine logs(eg . cloudwatch-logs or kinesis-firehose) | `string` | `""` | no |
| <a name="input_engine_log_format"></a> [engine\_log\_format](#input\_engine\_log\_format) | the format for logs eg. json/text | `string` | `"json"` | no |
| <a name="input_engine_version"></a> [engine\_version](#input\_engine\_version) | The redis engine version | `string` | `""` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | The name of environment | `string` | `""` | no |
| <a name="input_family"></a> [family](#input\_family) | Redis family | `string` | `"redis4.0"` | no |
| <a name="input_final_snapshot_identifier"></a> [final\_snapshot\_identifier](#input\_final\_snapshot\_identifier) | The name of your final node group (shard) snapshot. ElastiCache creates the snapshot from the primary node in the cluster. If omitted, no final snapshot will be made. | `string` | `null` | no |
| <a name="input_kms_key_arn"></a> [kms\_key\_arn](#input\_kms\_key\_arn) | The ARN of the key that you wish to use if encrypting at rest. If not supplied, uses service managed encryption. Can be specified only if at\_rest\_encryption\_enabled = true | `string` | `""` | no |
| <a name="input_maintenance_window"></a> [maintenance\_window](#input\_maintenance\_window) | Specifies the weekly time range for when maintenance on the cache cluster is performed. The format is ddd:hh24:mi-ddd:hh24:mi (24H Clock UTC). The minimum maintenance window is a 60 minute period | `string` | `"fri:08:00-fri:09:00"` | no |
| <a name="input_multi_az_enabled"></a> [multi\_az\_enabled](#input\_multi\_az\_enabled) | Enable multi az | `bool` | `false` | no |
| <a name="input_name"></a> [name](#input\_name) | The name of the redis cluster | `string` | `""` | no |
| <a name="input_node_type"></a> [node\_type](#input\_node\_type) | The instance size of the redis cluster | `string` | `"cache.t3.micro"` | no |
| <a name="input_notification_topic_arn"></a> [notification\_topic\_arn](#input\_notification\_topic\_arn) | (Optional) ARN of an SNS topic to send ElastiCache notifications | `string` | `null` | no |
| <a name="input_num_cache_nodes"></a> [num\_cache\_nodes](#input\_num\_cache\_nodes) | The number of cache nodes | `number` | `1` | no |
| <a name="input_parameter_group_description"></a> [parameter\_group\_description](#input\_parameter\_group\_description) | Parameter group | `string` | `null` | no |
| <a name="input_port"></a> [port](#input\_port) | The redis port | `number` | `6379` | no |
| <a name="input_recovery_window_aws_secret"></a> [recovery\_window\_aws\_secret](#input\_recovery\_window\_aws\_secret) | Number of days that AWS Secrets Manager waits before it can delete the secret. This value can be 0 to force deletion without recovery or range from 7 to 30 days. | `number` | `0` | no |
| <a name="input_slow_log_destination"></a> [slow\_log\_destination](#input\_slow\_log\_destination) | The destination for slow logs(eg. Cloudwatch log-group name or kinesis firehose stream name.) | `string` | `null` | no |
| <a name="input_slow_log_destination_type"></a> [slow\_log\_destination\_type](#input\_slow\_log\_destination\_type) | The type of destination for slow logs(eg . cloudwatch-logs or kinesis-firehose) | `string` | `""` | no |
| <a name="input_slow_log_format"></a> [slow\_log\_format](#input\_slow\_log\_format) | the format for logs eg. json/text | `string` | `"json"` | no |
| <a name="input_snapshot_arns"></a> [snapshot\_arns](#input\_snapshot\_arns) | (Optional) A single-element string list containing an Amazon Resource Name (ARN) of a Redis RDB snapshot file stored in Amazon S3. Example: arn:aws:s3:::my\_bucket/snapshot1.rdb . This will be used to add data to a fresh new instance. | `list(string)` | `[]` | no |
| <a name="input_snapshot_retention_limit"></a> [snapshot\_retention\_limit](#input\_snapshot\_retention\_limit) | The number of days for which ElastiCache will retain automatic cache cluster snapshots before deleting them. For example, if you set SnapshotRetentionLimit to 5, then a snapshot that was taken today will be retained for 5 days before being deleted. If the value of SnapshotRetentionLimit is set to zero (0), backups are turned off. Please note that setting a snapshot\_retention\_limit is not supported on cache.t1.micro or cache.t2.* cache nodes | `number` | `7` | no |
| <a name="input_snapshot_window"></a> [snapshot\_window](#input\_snapshot\_window) | The daily time range (in UTC) during which ElastiCache will begin taking a daily snapshot of your cache cluster. The minimum maintenance window is a 60 minute period. Example: 05:00-09:00 | `string` | `"03:00-05:00"` | no |
| <a name="input_subnets"></a> [subnets](#input\_subnets) | The subnets where the redis cluster is deployed | `list(string)` | `[]` | no |
| <a name="input_transit_encryption_enabled"></a> [transit\_encryption\_enabled](#input\_transit\_encryption\_enabled) | (Optional) Whether to enable encryption in transit | `bool` | `true` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | The vpc where we will put the redis cluster | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_auth_token_password"></a> [auth\_token\_password](#output\_auth\_token\_password) | Elasticache-redis auth token password(this password may be old, because Terraform doesn't track it after initial creation) |
| <a name="output_elastic_cache_redis_cluster_id"></a> [elastic\_cache\_redis\_cluster\_id](#output\_elastic\_cache\_redis\_cluster\_id) | ID of the elasticache-redis cluster |
| <a name="output_elastic_cache_redis_endpoint"></a> [elastic\_cache\_redis\_endpoint](#output\_elastic\_cache\_redis\_endpoint) | Elasticache-redis cluster primary endpoint address |
| <a name="output_elastic_cache_redis_port"></a> [elastic\_cache\_redis\_port](#output\_elastic\_cache\_redis\_port) | Port number of Redis |
| <a name="output_elastic_cache_redis_primary_endpoint_address"></a> [elastic\_cache\_redis\_primary\_endpoint\_address](#output\_elastic\_cache\_redis\_primary\_endpoint\_address) | Primary endpoint address of redis |
| <a name="output_elastic_cache_redis_security_group"></a> [elastic\_cache\_redis\_security\_group](#output\_elastic\_cache\_redis\_security\_group) | The security group ID of the cluster |
| <a name="output_elastic_cache_redis_subnet_group_name"></a> [elastic\_cache\_redis\_subnet\_group\_name](#output\_elastic\_cache\_redis\_subnet\_group\_name) | Subnet group name of the elasticache\_redis cluster |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Contribute & Issue Report

To report an issue with a project:

  1. Check the repository's [issue tracker](https://github.com/squareops/terraform-aws-elasticache-redis/issues) on GitHub
  2. Search to check if the issue has already been reported
  3. If you can't find an answer to your question in the documentation or issue tracker, you can ask a question by creating a new issue. Make sure to provide enough context and details.

## License

Apache License, Version 2.0, January 2004 (https://www.apache.org/licenses/LICENSE-2.0)

## Support Us

To support our GitHub project by liking it, you can follow these steps:

  1. Visit the repository: Navigate to the [GitHub repository](https://github.com/squareops/terraform-aws-elasticache-redis)

  2. Click the "Star" button: On the repository page, you'll see a "Star" button in the upper right corner. Clicking on it will star the repository, indicating your support for the project.

  3. Optionally, you can also leave a comment on the repository or open an issue to give feedback or suggest changes.

Staring a repository on GitHub is a simple way to show your support and appreciation for the project. It also helps to increase the visibility of the project and make it more discoverable to others.

## Who we are

We believe that the key to success in the digital age is the ability to deliver value quickly and reliably. That’s why we offer a comprehensive range of DevOps & Cloud services designed to help your organization optimize its systems & Processes for speed and agility.

  1. We are an AWS Advanced consulting partner which reflects our deep expertise in AWS Cloud and helping 100+ clients over the last 5 years.
  2. Expertise in Kubernetes and overall container solution helps companies expedite their journey by 10X.
  3. Infrastructure Automation is a key component to the success of our Clients and our Expertise helps deliver the same in the shortest time.
  4. DevSecOps as a service to implement security within the overall DevOps process and helping companies deploy securely and at speed.
  5. Platform engineering which supports scalable,Cost efficient infrastructure that supports rapid development, testing, and deployment.
  6. 24*7 SRE service to help you Monitor the state of your infrastructure and eradicate any issue within the SLA.

We provide [support](https://squareops.com/contact-us/) on all of our projects, no matter how small or large they may be.

To find more information about our company, visit [squareops.com](https://squareops.com/), follow us on [Linkedin](https://www.linkedin.com/company/squareops-technologies-pvt-ltd/), or fill out a [job application](https://squareops.com/careers/). If you have any questions or would like assistance with your cloud strategy and implementation, please don't hesitate to [contact us](https://squareops.com/contact-us/).
