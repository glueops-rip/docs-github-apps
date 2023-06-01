# github-oauth-app

This readme documents the process for creating GitHub OAuth apps for the deployment of the GlueOps Platform.  The OAuth app is used for Authentication into various services deployed on the Platform.

## Before you start

For this example we will assume your GitHub organization is called `glueops-rocks`. You will need to update the URL's/links below accordingly to use your organization name in place of `glueops-rocks`. Secondly, we will assume your `captain_domain` is `nonprod.antoniostacos.glueopshosted.com`

### Create the ArgoCD Application

1. Go to: <https://github.com/organizations/glueops-rocks/settings/applications>

2. Click on `New OAuth App`
3. Let's create an the first app.

    - `Application name`: GlueOps-Dex _(This Application name can be whatever you want.)_

    - `Homepage URL`: <https://dex.nonprod.antoniostacos.glueopshosted.com>
  
    - `Authorization callback URL`: <https://dex.nonprod.antoniostacos.glueopshosted.com/callback>

4. Save the Client ID and Client Secret as it will be used in the deployment of the [terraform-module-cloud-multy-prerequisites](https://github.com/GlueOps/terraform-module-cloud-multy-prerequisites) module as the values for:
    - `github_oauth_app_client_id`
    - `github_oauth_app_client_secret`
