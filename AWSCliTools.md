### AWS CLI Configuration

| Command | Notes / Explanation |
|---------|-------------------|
| `aws configure --profile <PROFILE>` | Configure AWS CLI for a profile |
| `aws configure list-profiles` | List all configured profiles |
| `aws configure set region <REGION> --profile <PROFILE>` | Set default region |
| `aws configure set output json --profile <PROFILE>` | Set output format |
| `aws configure get region --profile <PROFILE>` | Show configured region |
| `aws configure get output --profile <PROFILE>` | Show output format |

### IAM Users, Roles, Policies

| Command | Notes / Explanation |
|---------|-------------------|
| `aws iam list-users --profile <PROFILE>` | List IAM users |
| `aws iam create-user --user-name <USERNAME> --profile <PROFILE>` | Create IAM user |
| `aws iam delete-user --user-name <USERNAME> --profile <PROFILE>` | Delete IAM user |
| `aws iam list-roles --profile <PROFILE>` | List IAM roles |
| `aws iam create-role --role-name <ROLE> --assume-role-policy-document file://<TRUST_POLICY_FILE>` | Create IAM role |
| `aws iam delete-role --role-name <ROLE> --profile <PROFILE>` | Delete IAM role |
| `aws iam attach-user-policy --user-name <USERNAME> --policy-arn arn:aws:iam::aws:policy/AdministratorAccess` | Attach policy to user |
| `aws iam detach-user-policy --user-name <USERNAME> --policy-arn arn:aws:iam::aws:policy/AdministratorAccess` | Detach policy from user |
| `aws iam attach-role-policy --role-name <ROLE> --policy-arn arn:aws:iam::aws:policy/AdministratorAccess` | Attach policy to role |
| `aws iam detach-role-policy --role-name <ROLE> --policy-arn arn:aws:iam::aws:policy/AdministratorAccess` | Detach policy from role |
| `aws iam list-policies --scope Local --profile <PROFILE>` | List custom policies |
| `aws sts get-caller-identity --profile <PROFILE>` | Show current identity |
| `aws sts assume-role --role-arn arn:aws:iam::<ACCOUNT_ID>:role/<ROLE> --role-session-name <SESSION_NAME> --profile <PROFILE>` | Assume a role |

### S3 Buckets & Objects

| Command | Notes / Explanation |
|---------|-------------------|
| `aws s3 ls --profile <PROFILE>` | List all buckets |
| `aws s3 ls s3://<BUCKET> --profile <PROFILE>` | List bucket contents |
| `aws s3 mb s3://<BUCKET> --profile <PROFILE>` | Create bucket |
| `aws s3 rb s3://<BUCKET> --profile <PROFILE>` | Delete bucket |
| `aws s3 cp <LOCAL_FILE> s3://<BUCKET>/<DEST_FILE> --profile <PROFILE>` | Upload file |
| `aws s3 cp s3://<BUCKET>/<FILE> <LOCAL_FILE> --profile <PROFILE>` | Download file |
| `aws s3 sync <LOCAL_FOLDER> s3://<BUCKET> --profile <PROFILE>` | Sync local folder to bucket |
| `aws s3 sync s3://<BUCKET> <LOCAL_FOLDER> --profile <PROFILE>` | Sync bucket to local folder |
| `aws s3 rm s3://<BUCKET>/<FILE> --profile <PROFILE>` | Delete object |
| `aws s3 rm s3://<BUCKET> --recursive --profile <PROFILE>` | Delete all objects |
| `aws s3api put-bucket-versioning --bucket <BUCKET> --versioning-configuration Status=Enabled --profile <PROFILE>` | Enable versioning |
| `aws s3api put-bucket-lifecycle-configuration --bucket <BUCKET> --lifecycle-configuration file://<LIFECYCLE_JSON> --profile <PROFILE>` | Set lifecycle policy |

### EC2 Instances

| Command | Notes / Explanation |
|---------|-------------------|
| `aws ec2 describe-instances --profile <PROFILE>` | List instances |
| `aws ec2 start-instances --instance-ids <INSTANCE_ID> --profile <PROFILE>` | Start instance |
| `aws ec2 stop-instances --instance-ids <INSTANCE_ID> --profile <PROFILE>` | Stop instance |
| `aws ec2 reboot-instances --instance-ids <INSTANCE_ID> --profile <PROFILE>` | Reboot instance |
| `aws ec2 terminate-instances --instance-ids <INSTANCE_ID> --profile <PROFILE>` | Terminate instance |
| `aws ec2 create-key-pair --key-name <KEY_NAME> --query 'KeyMaterial' --output text > <KEY_FILE>.pem` | Create key pair |
| `aws ec2 describe-security-groups --profile <PROFILE>` | List security groups |
| `aws ec2 authorize-security-group-ingress --group-id <SG_ID> --protocol tcp --port 22 --cidr 0.0.0.0/0` | Add inbound rule |
| `aws ec2 revoke-security-group-ingress --group-id <SG_ID> --protocol tcp --port 22 --cidr 0.0.0.0/0` | Remove inbound rule |
| `aws ec2 describe-images --owners self --profile <PROFILE>` | List owned AMIs |
| `aws ec2 create-image --instance-id <INSTANCE_ID> --name "<IMAGE_NAME>" --profile <PROFILE>` | Create AMI |
| `aws ec2 deregister-image --image-id <IMAGE_ID> --profile <PROFILE>` | Deregister AMI |
| `aws ec2 describe-volumes --profile <PROFILE>` | List EBS volumes |
| `aws ec2 create-volume --size <SIZE_GB> --availability-zone <AZ> --profile <PROFILE>` | Create EBS volume |
| `aws ec2 attach-volume --volume-id <VOLUME_ID> --instance-id <INSTANCE_ID> --device /dev/sdf --profile <PROFILE>` | Attach volume |
| `aws ec2 detach-volume --volume-id <VOLUME_ID> --profile <PROFILE>` | Detach volume |

### VPC / Networking

| Command | Notes / Explanation |
|---------|-------------------|
| `aws ec2 describe-vpcs --profile <PROFILE>` | List VPCs |
| `aws ec2 create-vpc --cidr-block <CIDR_BLOCK> --profile <PROFILE>` | Create VPC |
| `aws ec2 delete-vpc --vpc-id <VPC_ID> --profile <PROFILE>` | Delete VPC |
| `aws ec2 describe-subnets --profile <PROFILE>` | List subnets |
| `aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block <CIDR_BLOCK> --availability-zone <AZ> --profile <PROFILE>` | Create subnet |
| `aws ec2 describe-internet-gateways --profile <PROFILE>` | List IGWs |
| `aws ec2 attach-internet-gateway --vpc-id <VPC_ID> --internet-gateway-id <IGW_ID> --profile <PROFILE>` | Attach IGW |
| `aws ec2 detach-internet-gateway --internet-gateway-id <IGW_ID> --vpc-id <VPC_ID> --profile <PROFILE>` | Detach IGW |
| `aws ec2 delete-internet-gateway --internet-gateway-id <IGW_ID> --profile <PROFILE>` | Delete IGW |
| `aws ec2 describe-route-tables --profile <PROFILE>` | List route tables |
| `aws ec2 create-route --route-table-id <RTB_ID> --destination-cidr-block 0.0.0.0/0 --gateway-id <IGW_ID> --profile <PROFILE>` | Add route |
| `aws ec2 delete-route --route-table-id <RTB_ID> --destination-cidr-block 0.0.0.0/0 --profile <PROFILE>` | Delete route |
| `aws ec2 describe-network-acls --profile <PROFILE>` | List NACLs |
| `aws ec2 create-network-acl --vpc-id <VPC_ID> --profile <PROFILE>` | Create NACL |
| `aws ec2 delete-network-acl --network-acl-id <NACL_ID> --profile <PROFILE>` | Delete NACL |
| `aws ec2 describe-vpc-peering-connections --profile <PROFILE>` | List VPC peering connections |
| `aws ec2 create-vpc-peering-connection --vpc-id <VPC_ID_1> --peer-vpc-id <VPC_ID_2> --profile <PROFILE>` | Create VPC peering |
| `aws ec2 accept-vpc-peering-connection --vpc-peering-connection-id <PCX_ID> --profile <PROFILE>` | Accept peering |

### CloudFormation

| Command | Notes / Explanation |
|---------|-------------------|
| `aws cloudformation list-stacks --profile <PROFILE>` | List all stacks |
| `aws cloudformation describe-stacks --stack-name <STACK_NAME> --profile <PROFILE>` | Describe a specific stack |
| `aws cloudformation create-stack --stack-name <STACK_NAME> --template-body file://<TEMPLATE_FILE> --capabilities CAPABILITY_NAMED_IAM --profile <PROFILE>` | Create a new stack |
| `aws cloudformation update-stack --stack-name <STACK_NAME> --template-body file://<TEMPLATE_FILE> --capabilities CAPABILITY_NAMED_IAM --profile <PROFILE>` | Update an existing stack |
| `aws cloudformation delete-stack --stack-name <STACK_NAME> --profile <PROFILE>` | Delete a stack |
| `aws cloudformation validate-template --template-body file://<TEMPLATE_FILE>` | Validate template syntax |
| `aws cloudformation describe-stack-events --stack-name <STACK_NAME> --profile <PROFILE>` | View stack events |
| `aws cloudformation list-stack-resources --stack-name <STACK_NAME> --profile <PROFILE>` | List resources in a stack |
| `aws cloudformation detect-stack-drift --stack-name <STACK_NAME> --profile <PROFILE>` | Detect drift in stack resources |
| `aws cloudformation describe-stack-drift-detection-status --stack-drift-detection-id <DETECTION_ID> --profile <PROFILE>` | Check drift status |

### Lambda & Step Functions

| Command | Notes / Explanation |
|---------|-------------------|
| `aws lambda list-functions --profile <PROFILE>` | List all Lambda functions |
| `aws lambda create-function --function-name <FUNCTION_NAME> --runtime python3.9 --role arn:aws:iam::<ACCOUNT_ID>:role/<ROLE> --handler lambda_function.lambda_handler --zip-file fileb://<ZIP_FILE>` | Create Lambda function |
| `aws lambda update-function-code --function-name <FUNCTION_NAME> --zip-file fileb://<ZIP_FILE> --profile <PROFILE>` | Update Lambda code |
| `aws lambda invoke --function-name <FUNCTION_NAME> --payload '{"key":"value"}' <OUTPUT_FILE> --profile <PROFILE>` | Invoke Lambda |
| `aws lambda delete-function --function-name <FUNCTION_NAME> --profile <PROFILE>` | Delete Lambda |
| `aws lambda add-permission --function-name <FUNCTION_NAME> --statement-id <STATEMENT_ID> --action lambda:InvokeFunction --principal <PRINCIPAL> --profile <PROFILE>` | Add permission |
| `aws stepfunctions list-state-machines --profile <PROFILE>` | List Step Functions state machines |
| `aws stepfunctions describe-state-machine --state-machine-arn <STATE_MACHINE_ARN> --profile <PROFILE>` | Describe state machine |
| `aws stepfunctions start-execution --state-machine-arn <STATE_MACHINE_ARN> --name <EXECUTION_NAME> --input '{"key":"value"}' --profile <PROFILE>` | Start execution |
| `aws stepfunctions stop-execution --execution-arn <EXECUTION_ARN> --profile <PROFILE>` | Stop execution |
| `aws stepfunctions get-execution-history --execution-arn <EXECUTION_ARN> --profile <PROFILE>` | View execution history |

### RDS / Aurora

| Command | Notes / Explanation |
|---------|-------------------|
| `aws rds describe-db-instances --profile <PROFILE>` | List RDS instances |
| `aws rds create-db-instance --db-instance-identifier <DB_NAME> --db-instance-class db.t3.micro --engine mysql --master-username <USER> --master-user-password <PASSWORD> --allocated-storage 20 --profile <PROFILE>` | Create RDS instance |
| `aws rds delete-db-instance --db-instance-identifier <DB_NAME> --skip-final-snapshot --profile <PROFILE>` | Delete RDS instance |
| `aws rds reboot-db-instance --db-instance-identifier <DB_NAME> --profile <PROFILE>` | Reboot RDS instance |
| `aws rds describe-db-snapshots --profile <PROFILE>` | List RDS snapshots |
| `aws rds create-db-snapshot --db-instance-identifier <DB_NAME> --db-snapshot-identifier <SNAPSHOT_NAME> --profile <PROFILE>` | Create DB snapshot |
| `aws rds restore-db-instance-from-db-snapshot --db-instance-identifier <NEW_DB_NAME> --db-snapshot-identifier <SNAPSHOT_NAME> --profile <PROFILE>` | Restore from snapshot |
| `aws rds describe-db-clusters --profile <PROFILE>` | List Aurora clusters |
| `aws rds create-db-cluster --db-cluster-identifier <CLUSTER_NAME> --engine aurora-mysql --master-username <USER> --master-user-password <PASSWORD> --profile <PROFILE>` | Create Aurora cluster |
| `aws rds delete-db-cluster --db-cluster-identifier <CLUSTER_NAME> --skip-final-snapshot --profile <PROFILE>` | Delete Aurora cluster |

### DynamoDB

| Command | Notes / Explanation |
|---------|-------------------|
| `aws dynamodb list-tables --profile <PROFILE>` | List DynamoDB tables |
| `aws dynamodb create-table --table-name <TABLE_NAME> --attribute-definitions AttributeName=<NAME>,AttributeType=S --key-schema AttributeName=<NAME>,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 --profile <PROFILE>` | Create table |
| `aws dynamodb delete-table --table-name <TABLE_NAME> --profile <PROFILE>` | Delete table |
| `aws dynamodb describe-table --table-name <TABLE_NAME> --profile <PROFILE>` | Describe table |
| `aws dynamodb put-item --table-name <TABLE_NAME> --item '{"<KEY>": {"S": "<VALUE>"}}' --profile <PROFILE>` | Insert item |
| `aws dynamodb get-item --table-name <TABLE_NAME> --key '{"<KEY>": {"S": "<VALUE>"}}' --profile <PROFILE>` | Get item |
| `aws dynamodb update-item --table-name <TABLE_NAME> --key '{"<KEY>": {"S": "<VALUE>"}}' --update-expression "SET <ATTRIBUTE>=:val1" --expression-attribute-values '{":val1":{"S":"<NEW_VALUE>"}}' --profile <PROFILE>` | Update item |
| `aws dynamodb delete-item --table-name <TABLE_NAME> --key '{"<KEY>": {"S": "<VALUE>"}}' --profile <PROFILE>` | Delete item |
| `aws dynamodb query --table-name <TABLE_NAME> --key-condition-expression "<KEY>=:val" --expression-attribute-values '{":val":{"S":"<VALUE>"}}' --profile <PROFILE>` | Query items |
| `aws dynamodb scan --table-name <TABLE_NAME> --profile <PROFILE>` | Scan table |

### EKS (Elastic Kubernetes Service)

| Command | Notes / Explanation |
|---------|-------------------|
| `aws eks list-clusters --profile <PROFILE>` | List EKS clusters |
| `aws eks describe-cluster --name <CLUSTER_NAME> --profile <PROFILE>` | Describe cluster |
| `aws eks update-kubeconfig --name <CLUSTER_NAME> --profile <PROFILE>` | Update kubeconfig for kubectl |
| `aws eks create-cluster --name <CLUSTER_NAME> --role-arn arn:aws:iam::<ACCOUNT_ID>:role/<ROLE> --resources-vpc-config subnetIds=<SUBNET_IDS>,securityGroupIds=<SG_IDS> --profile <PROFILE>` | Create cluster |
| `aws eks delete-cluster --name <CLUSTER_NAME> --profile <PROFILE>` | Delete cluster |

### ECS (Elastic Container Service) & ECR (Elastic Container Registry)

| Command | Notes / Explanation |
|---------|-------------------|
| `aws ecs list-clusters --profile <PROFILE>` | List ECS clusters |
| `aws ecs describe-clusters --clusters <CLUSTER_NAME> --profile <PROFILE>` | Describe ECS cluster |
| `aws ecs list-services --cluster <CLUSTER_NAME> --profile <PROFILE>` | List services in cluster |
| `aws ecs describe-services --cluster <CLUSTER_NAME> --services <SERVICE_NAME> --profile <PROFILE>` | Describe service |
| `aws ecs update-service --cluster <CLUSTER_NAME> --service <SERVICE_NAME> --desired-count <COUNT> --profile <PROFILE>` | Update service |
| `aws ecs create-service --cluster <CLUSTER_NAME> --service-name <SERVICE_NAME> --task-definition <TASK_DEF> --desired-count <COUNT> --profile <PROFILE>` | Create service |
| `aws ecs delete-service --cluster <CLUSTER_NAME> --service <SERVICE_NAME> --force --profile <PROFILE>` | Delete service |
| `aws ecr create-repository --repository-name <REPO_NAME> --profile <PROFILE>` | Create ECR repo |
| `aws ecr delete-repository --repository-name <REPO_NAME> --force --profile <PROFILE>` | Delete ECR repo |
| `aws ecr list-images --repository-name <REPO_NAME> --profile <PROFILE>` | List images |
| `aws ecr batch-delete-image --repository-name <REPO_NAME> --image-ids imageTag=<TAG> --profile <PROFILE>` | Delete image |
| `aws ecr get-login-password --region <REGION> --profile <PROFILE>` | Authenticate Docker to ECR |

### CloudWatch Metrics, Logs, Alarms

| Command | Notes / Explanation |
|---------|-------------------|
| `aws cloudwatch list-metrics --namespace <NAMESPACE> --profile <PROFILE>` | List metrics |
| `aws cloudwatch get-metric-statistics --namespace <NAMESPACE> --metric-name <METRIC> --dimensions Name=<NAME>,Value=<VALUE> --start-time <START> --end-time <END> --period 300 --statistics Average --profile <PROFILE>` | Get metric stats |
| `aws cloudwatch put-metric-alarm --alarm-name <ALARM_NAME> --metric-name <METRIC> --namespace <NAMESPACE> --statistic Average --period 300 --threshold <THRESHOLD> --comparison-operator GreaterThanThreshold --evaluation-periods 1 --alarm-actions <SNS_TOPIC_ARN> --profile <PROFILE>` | Create alarm |
| `aws cloudwatch describe-alarms --profile <PROFILE>` | List alarms |
| `aws cloudwatch delete-alarms --alarm-names <ALARM_NAME> --profile <PROFILE>` | Delete alarm |
| `aws logs describe-log-groups --profile <PROFILE>` | List log groups |
| `aws logs describe-log-streams --log-group-name <LOG_GROUP> --profile <PROFILE>` | List log streams |
| `aws logs get-log-events --log-group-name <LOG_GROUP> --log-stream-name <LOG_STREAM> --start-time <START_MS> --end-time <END_MS> --profile <PROFILE>` | Retrieve logs |
| `aws logs create-log-group --log-group-name <LOG_GROUP> --profile <PROFILE>` | Create log group |
| `aws logs create-log-stream --log-group-name <LOG_GROUP> --log-stream-name <LOG_STREAM> --profile <PROFILE>` | Create log stream |
| `aws logs put-log-events --log-group-name <LOG_GROUP> --log-stream-name <LOG_STREAM> --log-events file://<LOG_EVENTS_JSON> --profile <PROFILE>` | Push logs |

### SNS (Simple Notification Service)

| Command | Notes / Explanation |
|---------|-------------------|
| `aws sns list-topics --profile <PROFILE>` | List SNS topics |
| `aws sns create-topic --name <TOPIC_NAME> --profile <PROFILE>` | Create topic |
| `aws sns delete-topic --topic-arn <TOPIC_ARN> --profile <PROFILE>` | Delete topic |
| `aws sns subscribe --topic-arn <TOPIC_ARN> --protocol <PROTOCOL> --notification-endpoint <ENDPOINT> --profile <PROFILE>` | Subscribe endpoint |
| `aws sns unsubscribe --subscription-arn <SUBSCRIPTION_ARN> --profile <PROFILE>` | Unsubscribe |
| `aws sns publish --topic-arn <TOPIC_ARN> --message "<MESSAGE>" --profile <PROFILE>` | Publish message |

### SQS (Simple Queue Service)

| Command | Notes / Explanation |
|---------|-------------------|
| `aws sqs list-queues --profile <PROFILE>` | List queues |
| `aws sqs create-queue --queue-name <QUEUE_NAME> --profile <PROFILE>` | Create queue |
| `aws sqs delete-queue --queue-url <QUEUE_URL> --profile <PROFILE>` | Delete queue |
| `aws sqs send-message --queue-url <QUEUE_URL> --message-body "<MESSAGE>" --profile <PROFILE>` | Send message |
| `aws sqs receive-message --queue-url <QUEUE_URL> --max-number-of-messages 10 --profile <PROFILE>` | Receive message |
| `aws sqs delete-message --queue-url <QUEUE_URL> --receipt-handle <RECEIPT_HANDLE> --profile <PROFILE>` | Delete message |

### EventBridge / CloudWatch Events

| Command | Notes / Explanation |
|---------|-------------------|
| `aws events list-rules --profile <PROFILE>` | List EventBridge rules |
| `aws events describe-rule --name <RULE_NAME> --profile <PROFILE>` | Describe rule |
| `aws events put-rule --name <RULE_NAME> --schedule-expression "rate(5 minutes)" --profile <PROFILE>` | Create or update rule |
| `aws events delete-rule --name <RULE_NAME> --profile <PROFILE>` | Delete rule |
| `aws events list-targets-by-rule --rule <RULE_NAME> --profile <PROFILE>` | List targets |
| `aws events put-targets --rule <RULE_NAME> --targets file://<TARGETS_JSON> --profile <PROFILE>` | Add targets to rule |
| `aws events remove-targets --rule <RULE_NAME> --ids <TARGET_ID> --profile <PROFILE>` | Remove targets |

### Secrets Manager

| Command | Notes / Explanation |
|---------|-------------------|
| `aws secretsmanager list-secrets --profile <PROFILE>` | List secrets |
| `aws secretsmanager create-secret --name <SECRET_NAME> --secret-string '{"username":"<USER>","password":"<PASSWORD>"}' --profile <PROFILE>` | Create secret |
| `aws secretsmanager get-secret-value --secret-id <SECRET_NAME> --profile <PROFILE>` | Retrieve secret value |
| `aws secretsmanager update-secret --secret-id <SECRET_NAME> --secret-string '{"username":"<USER>","password":"<PASSWORD>"}' --profile <PROFILE>` | Update secret |
| `aws secretsmanager delete-secret --secret-id <SECRET_NAME> --force-delete-without-recovery --profile <PROFILE>` | Delete secret immediately |

### SSM Parameter Store

| Command | Notes / Explanation |
|---------|-------------------|
| `aws ssm put-parameter --name <PARAM_NAME> --value "<VALUE>" --type String --profile <PROFILE>` | Create or update parameter |
| `aws ssm get-parameter --name <PARAM_NAME> --with-decryption --profile <PROFILE>` | Retrieve parameter |
| `aws ssm delete-parameter --name <PARAM_NAME> --profile <PROFILE>` | Delete parameter |
| `aws ssm describe-parameters --profile <PROFILE>` | List parameters |
| `aws ssm get-parameters --names <PARAM_NAME1> <PARAM_NAME2> --with-decryption --profile <PROFILE>` | Retrieve multiple parameters |

### CloudFront

| Command | Notes / Explanation |
|---------|-------------------|
| `aws cloudfront list-distributions --profile <PROFILE>` | List distributions |
| `aws cloudfront get-distribution --id <DISTRIBUTION_ID> --profile <PROFILE>` | Describe distribution |
| `aws cloudfront create-distribution --distribution-config file://<CONFIG_JSON> --profile <PROFILE>` | Create distribution |
| `aws cloudfront update-distribution --id <DISTRIBUTION_ID> --distribution-config file://<CONFIG_JSON> --profile <PROFILE>` | Update distribution |
| `aws cloudfront delete-distribution --id <DISTRIBUTION_ID> --profile <PROFILE>` | Delete distribution |
| `aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*" --profile <PROFILE>` | Invalidate cache |

### Route53

| Command | Notes / Explanation |
|---------|-------------------|
| `aws route53 list-hosted-zones --profile <PROFILE>` | List hosted zones |
| `aws route53 get-hosted-zone --id <ZONE_ID> --profile <PROFILE>` | Get hosted zone details |
| `aws route53 create-hosted-zone --name <DOMAIN> --caller-reference <UNIQUE_REF> --profile <PROFILE>` | Create hosted zone |
| `aws route53 delete-hosted-zone --id <ZONE_ID> --profile <PROFILE>` | Delete hosted zone |
| `aws route53 list-resource-record-sets --hosted-zone-id <ZONE_ID> --profile <PROFILE>` | List DNS records |
| `aws route53 change-resource-record-sets --hosted-zone-id <ZONE_ID> --change-batch file://<CHANGES_JSON> --profile <PROFILE>` | Create/update/delete DNS records |

### WAF (Web Application Firewall)

| Command | Notes / Explanation |
|---------|-------------------|
| `aws wafv2 list-web-acls --scope REGIONAL --profile <PROFILE>` | List Web ACLs |
| `aws wafv2 get-web-acl --name <WEB_ACL_NAME> --scope REGIONAL --id <WEB_ACL_ID> --profile <PROFILE>` | Describe Web ACL |
| `aws wafv2 create-web-acl --name <WEB_ACL_NAME> --scope REGIONAL --default-action Allow={} --visibility-config file://<VISIBILITY_JSON> --profile <PROFILE>` | Create Web ACL |
| `aws wafv2 update-web-acl --name <WEB_ACL_NAME> --scope REGIONAL --id <WEB_ACL_ID> --default-action Allow={} --visibility-config file://<VISIBILITY_JSON> --profile <PROFILE>` | Update Web ACL |
| `aws wafv2 delete-web-acl --name <WEB_ACL_NAME> --scope REGIONAL --id <WEB_ACL_ID> --profile <PROFILE>` | Delete Web ACL |

### Backup / Glacier / Storage

| Command | Notes / Explanation |
|---------|-------------------|
| `aws backup list-backup-vaults --profile <PROFILE>` | List backup vaults |
| `aws backup create-backup-vault --backup-vault-name <VAULT_NAME> --profile <PROFILE>` | Create backup vault |
| `aws backup delete-backup-vault --backup-vault-name <VAULT_NAME> --profile <PROFILE>` | Delete backup vault |
| `aws backup list-backup-jobs --profile <PROFILE>` | List backup jobs |
| `aws backup start-backup-job --backup-vault-name <VAULT_NAME> --resource-arn <RESOURCE_ARN> --iam-role-arn <ROLE_ARN> --profile <PROFILE>` | Start backup job |
| `aws backup stop-backup-job --backup-job-id <JOB_ID> --profile <PROFILE>` | Stop backup job |
| `aws glacier list-vaults --profile <PROFILE>` | List Glacier vaults |
| `aws glacier create-vault --vault-name <VAULT_NAME> --profile <PROFILE>` | Create Glacier vault |
| `aws glacier delete-vault --vault-name <VAULT_NAME> --profile <PROFILE>` | Delete Glacier vault |
| `aws glacier initiate-job --vault-name <VAULT_NAME> --job-parameters file://<JOB_PARAMS_JSON> --profile <PROFILE>` | Initiate Glacier retrieval |
### Cost Explorer

| Command | Notes / Explanation |
|---------|-------------------|
| `aws ce get-cost-and-usage --time-period Start=<START_DATE>,End=<END_DATE> --granularity MONTHLY --metrics "BlendedCost" "UnblendedCost" --profile <PROFILE>` | Retrieve cost and usage |
| `aws ce get-cost-forecast --time-period Start=<START_DATE>,End=<END_DATE> --metric BLENDED_COST --profile <PROFILE>` | Forecast costs |
| `aws ce list-cost-categories --profile <PROFILE>` | List cost categories |

### Budgets

| Command | Notes / Explanation |
|---------|-------------------|
| `aws budgets describe-budgets --account-id <ACCOUNT_ID> --profile <PROFILE>` | List budgets |
| `aws budgets create-budget --account-id <ACCOUNT_ID> --budget file://<BUDGET_JSON> --profile <PROFILE>` | Create budget |
| `aws budgets update-budget --account-id <ACCOUNT_ID> --budget-name <BUDGET_NAME> --new-budget file://<BUDGET_JSON> --profile <PROFILE>` | Update budget |
| `aws budgets delete-budget --account-id <ACCOUNT_ID> --budget-name <BUDGET_NAME> --profile <PROFILE>` | Delete budget |

### Trusted Advisor

| Command | Notes / Explanation |
|---------|-------------------|
| `aws support describe-trusted-advisor-checks --language en --profile <PROFILE>` | List all Trusted Advisor checks |
| `aws support describe-trusted-advisor-check-result --check-id <CHECK_ID> --profile <PROFILE>` | Get check result |
| `aws support refresh-trusted-advisor-check --check-id <CHECK_ID> --profile <PROFILE>` | Refresh check |

### Billing

| Command | Notes / Explanation |
|---------|-------------------|
| `aws ce get-dimension-values --time-period Start=<START_DATE>,End=<END_DATE> --dimension SERVICE --profile <PROFILE>` | Get dimension values (e.g., services) |
| `aws organizations list-accounts --profile <PROFILE>` | List all linked accounts |
| `aws organizations describe-account --account-id <ACCOUNT_ID> --profile <PROFILE>` | Get account details |

### CLI Utilities / Tips

| Command | Notes / Explanation |
|---------|-------------------|
| `aws <SERVICE> <COMMAND> --dry-run` | Simulate command without executing |
| `aws <SERVICE> <COMMAND> --output table` | Pretty-print output as table |
| `aws <SERVICE> <COMMAND> --query "<JMESPATH>"` | Filter output using JMESPath |
| `aws <SERVICE> <COMMAND> --profile <PROFILE>` | Run command using a specific profile |
| `aws <SERVICE> <COMMAND> --region <REGION>` | Run command in specific region |
| `aws configure get region --profile <PROFILE>` | Check region for profile |
| `aws configure get output --profile <PROFILE>` | Check output format |
| `aws <SERVICE> <COMMAND> (pipe) jq '.'` | Pipe output to jq for JSON filtering |
| `aws s3 ls s3://<BUCKET> --recursive --human-readable --summarize` | Detailed S3 bucket list |
| `aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"` | Filter EC2 instances by state |
| `aws iam get-policy --policy-arn <POLICY_ARN> --profile <PROFILE>` | Get IAM policy details |
| `aws iam get-policy-version --policy-arn <POLICY_ARN> --version-id <VERSION_ID> --profile <PROFILE>` | Get specific policy version |

---

