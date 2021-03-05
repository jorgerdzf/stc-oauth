# Create the oAuth API Stack

Run the following command to create the resources for the oAuth API stack. It will create the codePipeline stack and the oAuth API stack as well. Just provide the required parameters to deploy to the environment you desire.

The template.yml is an empty template so that you can create a stack that then will be linked to the pipeline. Once the pipeline is working, the template.yml will be updated with the one that is in the project repository.

## Create a connection to the repository

You need to create a connection to the repository in order to link the pipeline to the repo. Follow this steps [Create a connection](https://docs.aws.amazon.com/dtconsole/latest/userguide/connections-create.html)

The PIPELINE_CONNECTION_ARN is the arn of the connection you just created.

## Parameters

| Parameter               | Description                                                                     | Example                                                                                             |
| ----------------------- | :------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| AWS_CLI_PROFILE         | AWS IAM user with enough permissions to create the resources                    | tiempo-erick                                                                                        |
| ROLE_TRUST_POLICY_FILE  | Trust policy to allow cloudformation to assume the required role                | file://./pipeline/policies/stc-oauth-cloudformation-trust-policy.json                               |
| ROLE_POLICY_FILE        | Location of the trust policy file                                               | file://./pipeline/policies/stc-oauth-cloudformation-policy.json                                     |
| API_STACK_TEMPLATE      | Location of the cloudformation template for the oAuth API                       | file://./api/initial-template.yml                                                                   |
| PIPELINE_STACK_TEMPLATE | Location of the cloudformation template for the oAuth pipeline                  | file://./pipeline/pipeline.yml                                                                      |
| PIPELINE_CONNECTION_ARN | ARN of the connection you just created as described in previous steps           | arn:aws:codestar-connections:us-west-2:474455999118:connection/4b0f8c65-5c27-459c-9477-bb87f7bb0114 |
| REPOSITORY_ID           | User and repository name (<user>/<repository>) of where the oAuth API is stored | jorgerdzf/stc-oauth                                                                                 |
| REPOSITORY_BRANCH       | Name of the branch that pipeline will be listening to be triggered              | dev                                                                                                 |
| ENVIRONMENT_TYPE        | Must be dev, qa, staging or prod                                                | dev                                                                                                 |

## Script

The following script is an example to create the required stacks for a development envirnoment.

## Development Environment Script

```bash
AWS_CLI_PROFILE="personal-jorge" \
ROLE_TRUST_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-trust-policy.json" \
ROLE_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-policy.json" \
API_STACK_TEMPLATE="file://./api/initial-template.yml" \
PIPELINE_STACK_TEMPLATE="file://./pipeline/pipeline.yml" \
PIPELINE_CONNECTION_ARN="arn:aws:codestar-connections:us-west-2:474455999118:connection/4b0f8c65-5c27-459c-9477-bb87f7bb0114" \
REPOSITORY_ID="jorgerdzf/stc-oauth" \
REPOSITORY_BRANCH="dev" \
ENVIRONMENT_TYPE="dev" \
./create-oauth-stack.sh
```

## QA Environment Script

```bash
AWS_CLI_PROFILE="personal-jorge" \
ROLE_TRUST_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-trust-policy.json" \
ROLE_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-policy.json" \
API_STACK_TEMPLATE="file://./api/initial-template.yml" \
PIPELINE_STACK_TEMPLATE="file://./pipeline/pipeline.yml" \
PIPELINE_CONNECTION_ARN="arn:aws:codestar-connections:us-west-2:474455999118:connection/4b0f8c65-5c27-459c-9477-bb87f7bb0114" \
REPOSITORY_ID="jorgerdzf/stc-oauth" \
REPOSITORY_BRANCH="qa" \
ENVIRONMENT_TYPE="qa" \
./create-oauth-stack.sh
```

## Staging Environment Script

```bash
AWS_CLI_PROFILE="personal-jorge" \
ROLE_TRUST_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-trust-policy.json" \
ROLE_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-policy.json" \
API_STACK_TEMPLATE="file://./api/initial-template.yml" \
PIPELINE_STACK_TEMPLATE="file://./pipeline/pipeline.yml" \
PIPELINE_CONNECTION_ARN="arn:aws:codestar-connections:us-west-2:474455999118:connection/4b0f8c65-5c27-459c-9477-bb87f7bb0114" \
REPOSITORY_ID="jorgerdzf/stc-oauth" \
REPOSITORY_BRANCH="staging" \
ENVIRONMENT_TYPE="staging" \
./create-oauth-stack.sh
```

## Production Environment Script

```bash
AWS_CLI_PROFILE="personal-jorge" \
ROLE_TRUST_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-trust-policy.json" \
ROLE_POLICY_FILE="file://./pipeline/policies/stc-oauth-cloudformation-policy.json" \
API_STACK_TEMPLATE="file://./api/initial-template.yml" \
PIPELINE_STACK_TEMPLATE="file://./pipeline/pipeline.yml" \
PIPELINE_CONNECTION_ARN="arn:aws:codestar-connections:us-west-2:474455999118:connection/4b0f8c65-5c27-459c-9477-bb87f7bb0114" \
REPOSITORY_ID="jorgerdzf/stc-oauth" \
REPOSITORY_BRANCH="master" \
ENVIRONMENT_TYPE="prod" \
./create-oauth-stack.sh
```
