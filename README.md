# AWS ECS Infrastructure with Terraform

A Terraform configuration for provisioning a containerized application environment on AWS using ECS, ECR, and an Application Load Balancer. Shared for educational purposes — to demonstrate how these AWS services fit together in a real-world infrastructure-as-code setup.

## What this deploys

- **VPC & Networking** — custom VPC, subnets, routing (`vpc.tf`, `networking.tf`)
- **ECR** — container image repositories (`ecr.tf`)
- **ECS Cluster** — cluster definition for running containerized services (`ecs_cluster.tf`)
- **ECS Task Definitions & Services** — task/service configuration for the app (`ecs_task_and_service.tf`)
- **Launch Templates & Auto Scaling Group** — EC2 instances backing the ECS cluster (`launch_template_asg.tf`)
- **ALB & Target Groups** — load balancing and routing to ECS services (`alb_and_tg.tf`)
- **IAM** — roles and policies for ECS tasks/instances (`iam.tf`)
- **User Data** — EC2 bootstrap script for ECS agent registration (`ecs_instance_user_data.tpl`, `user_data/`)

## Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/downloads) >= 1.x
- An AWS account with credentials configured (via `aws configure`, environment variables, or an IAM profile)
- Appropriate IAM permissions to create VPC, ECS, ECR, ALB, and IAM resources

## Usage

```bash
terraform init
terraform plan
terraform apply
```

Review the plan output carefully before applying — this will create billable AWS resources.

## Configuration

Adjust values in `variables.tf` to match your environment (region, instance sizes, naming, etc.). Do not commit a populated `terraform.tfvars` file — see `.gitignore`.

## Notes

- This repo is intended as a **learning reference**, not a drop-in production template. Review and adapt security groups, IAM policies, and scaling settings for your own use case.
- State files (`.tfstate`) are intentionally excluded from version control since they can contain sensitive data in plaintext. In a real deployment, use a remote backend (e.g., S3 with encryption + DynamoDB locking) instead of local state.

## License

Feel free to use this as a learning resource. No warranty provided — review before using in any real environment.
