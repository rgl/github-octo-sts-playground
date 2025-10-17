# About

My [Octo STS](https://github.com/octo-sts/app) playground.

This uses the [Octo STS GitHub App](https://github.com/octo-sts) and the [octo-sts/action GitHub Action](https://github.com/octo-sts/action) to request a token for accessing the [rgl-example/github-octo-sts-example](https://github.com/rgl-example/github-octo-sts-example) repository.

# Usage

Install the [Octo STS GitHub App](https://github.com/apps/octo-sts) in your target GitHub Organization.

Modify your GitHub Actions Workflow to use the [octo-sts/action](https://github.com/octo-sts/action) to create a token for a target repository, like in the [test workflow](.github/workflows/test.yml).

Use the created token to access the target repository.

# Notes

* The Octo STS GitHub App service is hosted at https://octo-sts.dev.
  * It is currently hosted in GCP in the `us-central1` region of the USA.
    * That is defined in the [Octo STS infrastructure code](https://github.com/octo-sts/app/blob/main/iac/terraform.tfvars).
* The Octo STS GitHub App creates a GitHub Token from a GitHub Actions Workflow OIDC ID Token and a security policy stored in a `.sts.yaml` file inside the target repository, e.g., at [rgl-example/github-octo-sts-example/.github/chainguard/playground.sts.yaml](https://github.com/rgl-example/github-octo-sts-example/blob/main/.github/chainguard/playground.sts.yaml).
  * The security profile can use some of the OIDC ID Token claims, e.g., `sub` (aka `subject`), which contains the repository name and git ref, something like `repo:rgl/github-octo-sts-playground:ref:refs/heads/main`.
    * You can see a full example of a GitHub Actions Workflow ID Token JWT at https://github.com/rgl/github-actions-validate-jwt.
* The created GitHub Token is an [Octo STS GitHub App installation access token](https://docs.github.com/en/rest/apps/apps?apiVersion=2022-11-28#create-an-installation-access-token-for-an-app).
* The access token can be used to access the [GitHub REST/HTTP API](https://docs.github.com/en/rest), and also the [Git HTTP API](https://git-scm.com/docs/gitprotocol-http).
  * You can configure the git credentials like the [actions/checkout action](https://github.com/actions/checkout), in the `.git/config` file, as the `Authorization` HTTP header:
    ```ini
    [http "https://github.com/"]
      extraheader = AUTHORIZATION: basic <base64(x-access-token:<GITHUB_TOKEN>)>
    ```

# Alternatives

* [qoomon/actions--access-token](https://github.com/qoomon/actions--access-token).
