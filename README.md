# gh-custom-action-aws-deploy

## Introduction

This GitHub Action deploys a static website to an S3 bucket.

## Prerequisites

- AWS_ACCESS_KEY_ID: Your AWS access key ID. This should be set up in your GitHub secrets.
- AWS_SECRET_ACCESS_KEY: Your AWS secret access key. This should also be set up in your GitHub secrets.

## Inputs

- `bucket`: The name of the S3 bucket where the website will be deployed. (Required).
- `website-content-dir`: The directory that contains the website content to be deployed. (Required).
- `bucket-region`: The AWS region where the S3 bucket is located. (Default: `us-east-1`).

## Outputs

- `website-url`: The URL of the deployed website.

## Complete usage

```yaml
jobs:
    deploy:
        needs: build
        runs-on: ubuntu-latest
        steps:
        - name: Deploy site
            id: deploy
            uses: maurya-anand/gh-custom-action-aws-deploy@v1
            env:
              AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
              AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
            with:
                bucket: test-bucket-id
                website-content-dir: ./dist
                bucket-region: us-east-2
        - name: Output deployed site URL
        run: |
            echo "Website deployed at: ${{ steps.deploy.outputs.website-url }}"
```

This example deploys the content of the `./dist` directory to the `test-bucket-id` S3 bucket in the `us-west-2` region.
