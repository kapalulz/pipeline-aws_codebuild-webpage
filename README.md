# AWS CodeBuild Container Pipeline Demo

A minimal static website packaged with Nginx and built by AWS CodeBuild for publication to Amazon ECR.

## Components

- `index.html` and `awslogo.png` — static website
- `Dockerfile` — Nginx container image
- `buildspec.yml` — CodeBuild build and registry workflow

## Run locally

```bash
docker build -t codebuild-demo-webpage .
docker run --rm -p 8080:80 codebuild-demo-webpage
```

Open [http://localhost:8080](http://localhost:8080).

## Pipeline flow

1. A source change starts CodeBuild.
2. CodeBuild authenticates to ECR.
3. Docker builds and tags the image.
4. The image is pushed to the configured ECR repository.

## Configuration

Keep AWS account IDs, repository names, Regions, and image tags in CodeBuild environment variables. Store sensitive values in AWS Secrets Manager or Systems Manager Parameter Store.

The CodeBuild role should have only the ECR and logging permissions required by the build.

> Review `buildspec.yml` before use and avoid relying on a floating `latest` tag for production deployments.
