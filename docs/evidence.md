# Deployment evidence

This record ties the showcase screenshots to the implementation and recorded release. It documents a deployment observed on 7–8 October 2026 (Pacific/Auckland); it does not claim ongoing availability.

## Release identifiers

- Implementation: https://github.com/YMKT-95/terraform-cloud-platform-demo
- Successful workflow: https://github.com/YMKT-95/terraform-cloud-platform-demo/actions/runs/37365003260/attempts/4
- Source commit: `5a9e6f82ae0e0344de04d975265c1529790e09fe`
- Application version: `0.2.0`
- AWS region: `ap-southeast-2`
- Availability zone: `ap-southeast-2a`
- Published image:

```text
ghcr.io/ymkt-95/terraform-cloud-platform-demo@sha256:b1fc86e116671002ea10bf74fc13dcca48e373461b2a44f5681a31dc896f42ff
```

The image digest matches the publishing and deployment summaries in the workflow screenshot. The source revision matches both the deployment summary and the application screenshot. The workflow was successful on attempt 4 after earlier runner allocation failures.

## Included evidence

1. [Application](../assets/application.png): rendered showcase, healthy response, version and source revision. The response time is a browser measurement, not a performance benchmark.
2. [Architecture](../assets/architecture.svg): explanatory diagram of the implemented design. It is authored documentation, not an automatically discovered resource map.
3. [CI/CD](../assets/pipeline-success.png): completed validation, publication and deployment, with a release summary confirming health and source revision.
4. [Terraform plan](../assets/terraform-no-changes.png): resource refresh followed by a no-change result. This checks managed infrastructure, not runtime container drift.
5. [EC2 instance](../assets/ec2-instance.png): running instance, `t3.micro`, Sydney availability zone and three passed EC2 checks.
6. [Security group](../assets/security-group.png): TCP 80 allowed from a single `/32` client source and no displayed SSH ingress rule.

The five PNGs are copied unchanged from the supplied captures. Filenames were normalized for repository links. The supplied SVG retains the reviewed design, with a long validation label split across two lines for readability.

## What is and is not verified

The successful release verifies the normal publish-and-deploy path, application health and the expected runtime source revision. The implementation also includes mocked Terraform and deployment recovery tests, as shown by successful validation jobs.

The evidence does not establish zero-downtime deployment, high availability, sustained performance, live failure rollback, restart recovery or successful resource destruction. The initial apply is documented in the implementation repository; the supplied Terraform screenshot shows a later no-change plan rather than the initial apply output.

Infrastructure state remains on the developer workstation. The GitHub OIDC provider and deployment role were configured by an administrator, while Terraform manages the EC2 instance role and instance profile. Application releases do not automatically update Terraform's bootstrap image.

## Repository boundary

This showcase contains documentation and presentation assets only. Source code, executable CI/CD workflows and deployment instructions remain in the linked implementation repository. No deployment is triggered by pushing to this showcase repository.
