# Terraform & Kubernetes patterns

## Terraform: minimal AWS S3 bucket with least-privilege access
```hcl
resource "aws_s3_bucket" "app_data" {
  bucket = var.bucket_name
}

resource "aws_s3_bucket_public_access_block" "app_data" {
  bucket                  = aws_s3_bucket.app_data.id
  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}

variable "bucket_name" {
  type = string
}
```
Note the explicit public-access block — S3 buckets are private by default in modern AWS, but making the block explicit in code documents the intent and guards against future account-level default changes.

## Terraform: remote state (S3 backend)
```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```
The DynamoDB table provides state locking so two people (or two CI runs) can't apply concurrently and corrupt state.

## Kubernetes: Deployment with resource limits and probes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  namespace: production
spec:
  replicas: 3
  selector:
    matchLabels: {app: app}
  template:
    metadata:
      labels: {app: app}
    spec:
      containers:
        - name: app
          image: myregistry/app:1.0.0
          resources:
            requests: {cpu: "100m", memory: "128Mi"}
            limits: {cpu: "500m", memory: "512Mi"}
          livenessProbe:
            httpGet: {path: /healthz, port: 3000}
            initialDelaySeconds: 10
          readinessProbe:
            httpGet: {path: /ready, port: 3000}
            initialDelaySeconds: 5
```
Never use `:latest` as the image tag in a real deployment manifest — pin a specific version so rollbacks are possible and deploys are reproducible.
