# github-app

This readme documents the process for creating GitHub Apps for the deployment of the GlueOps Platform.  The GitHub App is used by the Platform to access Tenant GitHub Organizations to provide the following services:

* Deployment of Tenant Applications via a [tenant-stack-repository](https://github.com/GlueOps/platform-helm-chart-platform/blob/main/templates/application-tenant-application-stack.yaml)
* Pull Request comments, generated by the [pull-request-bot](https://github.com/GlueOps/pull-request-bot), to display helpful links associated with preview environments.

## Overview

The GitHub App will be created within a Tenant's GitHub Organization and installed within the same organization.

At the end of this process, the following values used to deploy [terraform-module-cloud-multy-prerequisites](https://github.com/GlueOps/terraform-module-cloud-multy-prerequisites) will be available:

* `github_tenant_app_id`
* `github_tenant_app_installation_id`
* `github_tenant_app_b64enc_private_key`

## Create the GitHub App

1. Assuming the tenant organization is `example-tenant`, navigate to: <https://github.com/organizations/example-tenant/settings/apps/new>

2. Configure the application

    * `GitHub App name`: The Application name must be globally unique, and a combination of the Tenant Name and GlueOps is recommended.

    * `Homepage URL`: The URL can be anything, and <http://glueops.dev> is recommended.
  
    * `Webhook`:  deselect `Active` as Webhooks are not currently required by the GitHub App.
  
    * `Permissions`: grand the following `Repository permissions` to the GitHub APP:
      * `Contents`: Read and write
      * `Discussions`: Read and write
      * `Issues`: Read and write
      * `Metadata`: Read-only (mandatory)
      * `Pull requests`: Read and Write

    * `Where can this GitHub App be installed?`: ensure `Only on this account` is selected, as this app is local to a specific Tenant GitHub Organization.

    * Select `Create GitHub App`

3. Retrieve values required for [terraform-module-cloud-multy-prerequisites](https://github.com/GlueOps/terraform-module-cloud-multy-prerequisites) module deployment.

    * `github_tenant_app_id`: Appears as `App ID` after `Create GitHub App` has been selected.
    * `github_tenant_app_b64enc_private_key`
      * On the App's homepage, select `Generate a private key`, which will download a private key file
      * Create a base64 encoded version of the key file, using

        ```sh
        cat <downloaded-keyfile>.pem | base64 -w 0
        ```

4. Install the application in the Tenant GitHub Organization.
    * Select `Install App` in the left rail of the GitHub App's homepage and confirm installation
    * Retrieve the `github_tenant_app_installation_id` from the URL of the App Installation Homepage.  If the Tenant Organization is `example-tenant`, the url would be <https://github.com/organizations/example-tenant/settings/installations/12345678> and the `github_tenant_app_installation_id` would be `12345678`