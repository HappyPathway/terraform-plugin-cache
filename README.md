
[![Terraform Validation](https://github.com/HappyPathway/terraform-plugin-cache/actions/workflows/terraform.yaml/badge.svg)](https://github.com/HappyPathway/terraform-plugin-cache/actions/workflows/terraform.yaml)

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.0.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 4.20.1 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | 5.58.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_codebuild_terraform"></a> [codebuild\_terraform](#module\_codebuild\_terraform) | ./modules/codebuild | n/a |
| <a name="module_codepipeline_iam_role"></a> [codepipeline\_iam\_role](#module\_codepipeline\_iam\_role) | ./modules/iam-role | n/a |
| <a name="module_codepipeline_kms"></a> [codepipeline\_kms](#module\_codepipeline\_kms) | ./modules/kms | n/a |
| <a name="module_codepipeline_terraform"></a> [codepipeline\_terraform](#module\_codepipeline\_terraform) | ./modules/codepipeline | n/a |
| <a name="module_s3_artifacts_bucket"></a> [s3\_artifacts\_bucket](#module\_s3\_artifacts\_bucket) | ./modules/s3 | n/a |

## Resources

| Name | Type |
|------|------|
| [aws_iam_access_key.build_user](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_access_key) | resource |
| [aws_iam_user.build_user](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user) | resource |
| [aws_iam_user_policy.build_user](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_policy) | resource |
| [aws_secretsmanager_secret.credentials](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret) | resource |
| [aws_secretsmanager_secret_version.credentials](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret_version) | resource |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity) | data source |
| [aws_region.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/region) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_build_environment_variables"></a> [build\_environment\_variables](#input\_build\_environment\_variables) | n/a | <pre>list(object({<br>    name  = string<br>    value = string<br>    type  = string<br>  }))</pre> | `[]` | no |
| <a name="input_build_permissions_iam_doc"></a> [build\_permissions\_iam\_doc](#input\_build\_permissions\_iam\_doc) | n/a | `any` | n/a | yes |
| <a name="input_build_projects"></a> [build\_projects](#input\_build\_projects) | Tags to be attached to the CodePipeline | `list(string)` | <pre>[<br>  "validate",<br>  "plan",<br>  "apply"<br>]</pre> | no |
| <a name="input_builder_compute_type"></a> [builder\_compute\_type](#input\_builder\_compute\_type) | Relative path to the Apply and Destroy build spec file | `string` | `"BUILD_GENERAL1_SMALL"` | no |
| <a name="input_builder_image"></a> [builder\_image](#input\_builder\_image) | Docker Image to be used by codebuild | `string` | `"aws/codebuild/amazonlinux2-x86_64-standard:3.0"` | no |
| <a name="input_builder_image_pull_credentials_type"></a> [builder\_image\_pull\_credentials\_type](#input\_builder\_image\_pull\_credentials\_type) | Image pull credentials type used by codebuild project | `string` | `"CODEBUILD"` | no |
| <a name="input_builder_type"></a> [builder\_type](#input\_builder\_type) | Type of codebuild run environment | `string` | `"LINUX_CONTAINER"` | no |
| <a name="input_codepipeline_iam_role_name"></a> [codepipeline\_iam\_role\_name](#input\_codepipeline\_iam\_role\_name) | Name of the IAM role to be used by the Codepipeline | `string` | `"codepipeline-role"` | no |
| <a name="input_create_new_repo"></a> [create\_new\_repo](#input\_create\_new\_repo) | Whether to create a new repository. Values are true or false. Defaulted to true always. | `bool` | `true` | no |
| <a name="input_create_new_role"></a> [create\_new\_role](#input\_create\_new\_role) | Whether to create a new IAM Role. Values are true or false. Defaulted to true always. | `bool` | `true` | no |
| <a name="input_efs_id"></a> [efs\_id](#input\_efs\_id) | n/a | `string` | n/a | yes |
| <a name="input_efs_location"></a> [efs\_location](#input\_efs\_location) | n/a | `string` | n/a | yes |
| <a name="input_efs_mount_options"></a> [efs\_mount\_options](#input\_efs\_mount\_options) | n/a | `string` | n/a | yes |
| <a name="input_efs_mount_point"></a> [efs\_mount\_point](#input\_efs\_mount\_point) | n/a | `string` | n/a | yes |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment in which the script is run. Eg: dev, prod, etc | `string` | n/a | yes |
| <a name="input_project_name"></a> [project\_name](#input\_project\_name) | Unique name for this project | `string` | n/a | yes |
| <a name="input_source_repo_branch"></a> [source\_repo\_branch](#input\_source\_repo\_branch) | Default branch in the Source repo for which CodePipeline needs to be configured | `string` | n/a | yes |
| <a name="input_source_repo_name"></a> [source\_repo\_name](#input\_source\_repo\_name) | Source repo name of the CodeCommit repository | `string` | n/a | yes |
| <a name="input_stage_input"></a> [stage\_input](#input\_stage\_input) | Tags to be attached to the CodePipeline | `list(map(any))` | <pre>[<br>  {<br>    "category": "Test",<br>    "input_artifacts": "SourceOutput",<br>    "name": "validate",<br>    "output_artifacts": "ValidateOutput",<br>    "owner": "AWS",<br>    "provider": "CodeBuild"<br>  },<br>  {<br>    "category": "Test",<br>    "input_artifacts": "ValidateOutput",<br>    "name": "plan",<br>    "output_artifacts": "PlanOutput",<br>    "owner": "AWS",<br>    "provider": "CodeBuild"<br>  },<br>  {<br>    "category": "Approval",<br>    "name": "approval",<br>    "owner": "AWS",<br>    "provider": "Manual"<br>  },<br>  {<br>    "category": "Build",<br>    "input_artifacts": "PlanOutput",<br>    "name": "apply",<br>    "output_artifacts": "ApplyOutput",<br>    "owner": "AWS",<br>    "provider": "CodeBuild"<br>  }<br>]</pre> | no |
| <a name="input_terraform_version"></a> [terraform\_version](#input\_terraform\_version) | Terraform CLI Version | `string` | `"1.7.5"` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_codebuild_arn"></a> [codebuild\_arn](#output\_codebuild\_arn) | The ARN of the Codebuild Project |
| <a name="output_codebuild_name"></a> [codebuild\_name](#output\_codebuild\_name) | The Name of the Codebuild Project |
| <a name="output_codepipeline_arn"></a> [codepipeline\_arn](#output\_codepipeline\_arn) | The ARN of the CodePipeline |
| <a name="output_codepipeline_name"></a> [codepipeline\_name](#output\_codepipeline\_name) | The Name of the CodePipeline |
| <a name="output_iam_arn"></a> [iam\_arn](#output\_iam\_arn) | The ARN of the IAM Role used by the CodePipeline |
| <a name="output_kms_arn"></a> [kms\_arn](#output\_kms\_arn) | The ARN of the KMS key used in the codepipeline |
| <a name="output_s3_arn"></a> [s3\_arn](#output\_s3\_arn) | The ARN of the S3 Bucket |
| <a name="output_s3_bucket_name"></a> [s3\_bucket\_name](#output\_s3\_bucket\_name) | The Name of the S3 Bucket |
<!-- END_TF_DOCS -->