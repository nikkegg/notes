# AWS

## Quick CLI reference

`$ aws logs tail "/ecs/app-api" --follow --format short > logs_dev.txt --profile=dev` - stream
logs from the log-group defined in "" into a file for a given profile. Useful
when tailling lambda logs (log group "/aws/lambda/lambda-name")
Can then use cut to format logs and tail the file in terminal with
`$ tail -f log.txt | cut -d " " -f "3-" | log_formatter_of_choice`

`$ aws sts assume-role --role-arn arn:aws:iam:<Environment ARN>:role/<desiredRoleName> --role-session-name <role-name>` - get temporary aws credentials

`$ aws ssm get-parameters --names "app_ecs_SECRENT_NAME" --with-decryption --profile=profile` - get values from param store

`$ aws ssm describe-parameters —profile=dev` - view secret names which exist in
param store

`$ aws sqs list-queues` - list sqs queues

## AWS cli config

To be able to easily switch between roles, create `config` file in
`${HOME}/.aws` folder and add the following:

```
[default]
output=json
mfa_serial = arn:aws:iam::<User IAM id>:mfa/<aws_user_name>
[profile profile1]
role_arn = arn:aws:iam::<Environment ARN>:role/app-preview-poweruser
region=eu-west-1
source_profile = default
mfa_serial = arn:aws:iam::<USER IAM id>:mfa/nik.vschenko

```

Above allows to pass `--profile=<profile>` flag to `aws` commands for each
profile defined in the `config` file.

## Cloud Practioner examp prep
