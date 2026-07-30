# TemplateProject  
 
This repository contains an automated set-up for a 3-account set-up for DevOps Account.
 
## Contributing
 
Please see our [Contribution Guide](CONTRIBUTING.md) and our [Component Guide](ADD_COMPONENT_GUIDE.md) if you want to contribute to the project.
 
1. ## AWS Accounts
 
| Account Name          | Account ID   | Purpose    |
|:---------------------:|:------------:|:----------:|
|  DevOps-bsioynhorm | 984492101631 | auto  (deprecated) | 
|  DevOps-ggvguynwha | 196615020824 | qa |
|  DevOps-cndioatelr | 091489542225 | prod |
 
 
 
## Initial Deployment
 
Initially we need to deploy the OIDC token, which is in the automation/github-oidc.yaml file.
Deployments are automated via GitHub Actions pipeline.
 
## For manual deployment:
 
Usage : Infrastructure is deployed automatically on push to main branch. Monitor deployments in GitHub Actions or AWS CloudFormation console. Access deployed resources using the output values from CloudFormation stacks.
 
License : Internal Covestro project with vendor licensed product. For more information see the CAR entry.
 
 
 # qa Deploy:
 aws cloudformation create-stack `
  --stack-name github-oidc-biwiki-infra `
  --template-body file://github-oidc.yaml `
  --parameters `
    ParameterKey=GitHubRepo,ParameterValue=covestro/biwiki-infra `
    ParameterKey=Environment,ParameterValue=qa `
  --capabilities CAPABILITY_NAMED_IAM `
  --region eu-central-1 `
  --profile <>
 
 
 
 # prod deploy:
 aws cloudformation create-stack `
  --stack-name github-oidc-biwiki-infra-prod `
  --template-body file://github-oidc.yaml `
  --parameters `
    ParameterKey=GitHubRepo,ParameterValue=covestro/biwiki-infra `
    ParameterKey=Environment,ParameterValue=prod `
  --capabilities CAPABILITY_NAMED_IAM `
  --region eu-central-1 `
  --profile <>
 
 
The plain project will contain a pipeline with a build to deploy QA , manual Approval and  Deploy Prod.
It will deploy the "infrastructure.yaml" via Cloduformation.
