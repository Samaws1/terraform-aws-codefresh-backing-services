## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| acm_enabled | Set to false to prevent the acm module from creating any resources | string | `true` | no |
| acm_primary_domain | A domain name for which the certificate should be issued | string | - | yes |
| acm_san_domains | A list of domains that should be SANs in the issued certificate | list | `<list>` | no |
| attributes | Additional attributes (e.g. `1`) | list | `<list>` | no |
| chamber_format | Format to store parameters in SSM, for consumption with `chamber` | string | `/%s/%s` | no |
| chamber_service | `chamber` service name. See [chamber usage](https://github.com/segmentio/chamber#usage) for more details | string | `` | no |
| delimiter | Delimiter to be used between `namespace`, `stage`, `name` and `attributes` | string | `-` | no |
| documentdb_apply_immediately | Specifies whether any cluster modifications are applied immediately, or during the next maintenance window | string | `true` | no |
| documentdb_cluster_enabled | Set to false to prevent the module from creating DocumentDB cluster | string | `true` | no |
| documentdb_cluster_family | The family of the DocumentDB cluster parameter group. For more details, see https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-parameter-group-create.html | string | `docdb3.6` | no |
| documentdb_cluster_parameters | List of DB parameters to apply | list | `<list>` | no |
| documentdb_cluster_size | Number of DB instances to create in the cluster | string | `3` | no |
| documentdb_enabled_cloudwatch_logs_exports | List of log types to export to CloudWatch. The following log types are supported: audit, error, general, slowquery | list | `<list>` | no |
| documentdb_engine | The name of the database engine to be used for this DB cluster. Defaults to `docdb`. Valid values: `docdb` | string | `docdb` | no |
| documentdb_engine_version | The version number of the database engine to use | string | `` | no |
| documentdb_instance_class | The instance class to use. For more details, see https://docs.aws.amazon.com/documentdb/latest/developerguide/db-instance-classes.html#db-instance-class-specs | string | `db.r4.large` | no |
| documentdb_master_password | Password for the master DB user. If left empty, will be generated automatically. Note that this may show up in logs, and it will be stored in the state file | string | `` | no |
| documentdb_master_username | Username for the master DB user. If left empty, will be generated automatically | string | `` | no |
| documentdb_port | DocumentDB port | string | `27017` | no |
| documentdb_preferred_backup_window | Daily time range during which the backups happen | string | `07:00-09:00` | no |
| documentdb_retention_period | Number of days to retain backups for | string | `5` | no |
| documentdb_skip_final_snapshot | Determines whether a final DB snapshot is created before the DB cluster is deleted | string | `true` | no |
| documentdb_storage_encrypted | Specifies whether the DB cluster is encrypted | string | `true` | no |
| enabled | Set to false to prevent the module from creating any resources | string | `true` | no |
| kms_key_id | KMS key ID used to encrypt SSM parameters | string | `` | no |
| name | Name  (e.g. `cf` or `codefresh`) | string | `cf` | no |
| namespace | Namespace (e.g. `eg` or `cp`) | string | - | yes |
| overwrite_ssm_parameter | Whether to overwrite an existing SSM parameter | string | `true` | no |
| postgres_admin_password | Postgres password for the admin user | string | `` | no |
| postgres_admin_user | Postgres admin user name | string | `` | no |
| postgres_cluster_enabled | Set to false to prevent the module from creating any resources | string | `true` | no |
| postgres_cluster_family | Postgres cluster DB family. Currently supported values are `aurora-postgresql9.6` and `aurora-postgresql10` | string | `aurora-postgresql9.6` | no |
| postgres_cluster_size | Postgres cluster size | string | `2` | no |
| postgres_db_name | Postgres database name | string | `` | no |
| postgres_instance_type | EC2 instance type for Postgres cluster | string | `db.r4.large` | no |
| postgres_maintenance_window | Weekly time range during which system maintenance can occur, in UTC | string | `sun:03:00-sun:04:00` | no |
| redis_apply_immediately | Whether to apply changes immediately or during the next maintenance window | string | `true` | no |
| redis_at_rest_encryption_enabled | Enable Redis encryption at rest | string | `true` | no |
| redis_auth_token | Auth token for password protecting Redis. `transit_encryption_enabled` must be set to `true`! Password must be longer than 16 chars | string | `` | no |
| redis_automatic_failover | Whether to enable automatic failover | string | `true` | no |
| redis_cluster_enabled | Set to false to prevent the module from creating any resources | string | `true` | no |
| redis_cluster_size | Redis cluster size | string | `2` | no |
| redis_engine_version | Version of Redis engine | string | `5.0.0` | no |
| redis_instance_type | EC2 instance type for Redis cluster | string | `cache.t2.medium` | no |
| redis_maintenance_window | Weekly time range during which system maintenance can occur, in UTC | string | `sun:03:00-sun:04:00` | no |
| redis_params | A list of Redis parameters to apply. Note that parameters may differ from a Redis family to another | list | `<list>` | no |
| redis_transit_encryption_enabled | Enable TLS for Redis cluster | string | `true` | no |
| s3_access_key_name | S3 user IAM access key name for storing in SSM. Default to aws_acces_key_id so chamber exports as AWS_ACCESS_KEY_ID, a standard AWS IAM ENV variable | string | `aws_access_key_id` | no |
| s3_allowed_bucket_actions | List of actions to permit for S3 bucket | list | `<list>` | no |
| s3_enabled | Set to false to prevent the module from creating any resources | string | `` | no |
| s3_secret_key_name | S3 user IAM secret key name for storing in SSM. Default to aws_secret_acces_key so chamber exports as AWS_SECRET_ACCESS_KEY, a standard AWS IAM ENV variable | string | `aws_secret_access_key` | no |
| s3_user_enabled | Set to `true` to create an S3 user with permission to access the bucket | string | `` | no |
| s3_versioning_enabled | Whether to enable versioning on the S3 bucket. | string | `false` | no |
| security_groups | List of security groups to be allowed to connect to the CodeFresh backing services | list | `<list>` | no |
| stage | Stage (e.g. `prod`, `dev`, `staging`) | string | - | yes |
| subnet_ids | A list of subnet IDs to launch the CodeFresh backing services in | list | `<list>` | no |
| tags | Additional tags (e.g. map(`Cluster`,`us-east-1.cloudposse.co`) | map | `<map>` | no |
| vpc_id | VPC ID for the CodeFresh backing services | string | - | yes |
| zone_name | DNS zone name | string | - | yes |

## Outputs

| Name | Description |
|------|-------------|
| acm_arn | The ARN of the certificate |
| acm_domain_validation_options | CNAME records that are added to the DNS zone to complete certificate validation |
| aurora_postgres_cluster_name | Aurora Postgres Cluster Identifier |
| aurora_postgres_database_name | Aurora Postgres Database name |
| aurora_postgres_master_hostname | Aurora Postgres DB Master hostname |
| aurora_postgres_master_username | Aurora Postgres Username for the master DB user |
| aurora_postgres_replicas_hostname | Aurora Postgres Replicas hostname |
| documentdb_arn | Amazon Resource Name (ARN) of the DocumentDB cluster |
| documentdb_cluster_name | DocumentDB Cluster Identifier |
| documentdb_endpoint | Endpoint of the DocumentDB cluster |
| documentdb_master_host | DocumentDB master hostname |
| documentdb_master_username | DocumentDB Username for the master DB user |
| documentdb_reader_endpoint | Read-only endpoint of the DocumentDB cluster, automatically load-balanced across replicas |
| documentdb_replicas_host | DocumentDB replicas hostname |
| elasticache_redis_host | Elasticache Redis host |
| elasticache_redis_id | Elasticache Redis cluster ID |
| elasticache_redis_security_group_id | Elasticache Redis security group ID |
| s3_access_key_id | The access key ID |
| s3_bucket_arn | The s3 bucket ARN |
| s3_secret_access_key | The secret access key. This will be written to the state file in plain-text |
| s3_user_arn | The ARN assigned by AWS for the user |
| s3_user_name | Normalized IAM user name |
| s3_user_unique_id | The user unique ID assigned by AWS |

