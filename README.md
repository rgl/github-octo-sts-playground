# About

My [Octo STS](https://github.com/octo-sts/app) playground.

This uses the [Octo STS GitHub App](https://github.com/octo-sts) and the [octo-sts/action GitHub Action](https://github.com/octo-sts/action) to request a token for accessing the [rgl-example/github-octo-sts-example](https://github.com/rgl-example/github-octo-sts-example) repository.

# Usage

Install the [Octo STS GitHub App](https://github.com/apps/octo-sts) in your target GitHub Organization.

Modify your GitHub Actions Workflow to use the [octo-sts/action](https://github.com/octo-sts/action) to create a token for a target repository, like in the [test workflow](.github/workflows/test.yml).

Use the created token to access the target repository.

# Notes

* The Octo STS GitHub App is hosted at https://octo-sts.dev.
  * It is currently hosted in GCP in the `us-central1` region of the USA.
    * That is defined in the [Octo STS infrastructure code](https://github.com/octo-sts/app/blob/main/iac/terraform.tfvars).
