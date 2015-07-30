---
menu:
  main:
    parent: apps
title: Deploying Rails
weight: 10
---

See the official CF guide: [Getting Started Deploying Ruby on Rails Apps](http://docs.cloudfoundry.org/buildpacks/ruby/gsg-ror.html). Here are the minimal steps for a basic Rails app:

1. Follow the setup instructions in [Getting Started](/getting-started/setup/) and review [concepts](/getting-started/concepts/).  If you are just getting started learning CloudFoundry, you can use the sandbox space:
  ```
  cf target -o sandbox
  ```
1. [Exclude files ignored by Git]({{< relref "apps/deployment.md#excluding-files" >}}).
1. Create the application on Cloud Foundry.

    ```bash
    cf push <APP_NAME>
    ```

1. [Set up the database](/apps/databases/).
1. Set additional [environment variables](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html).

    ```bash
    cf set-env <APP_NAME> SECRET_TOKEN `rake secret`
    # etc.
    ```

1. [SSH into the application](/getting-started/cf-ssh/), then run `rake db:setup`.

Your app should now be live at `APP_NAME.18f.gov`!

## Troubleshooting Asset Precompilation

By default, the Rails buildpack performs asset precompilation during the staging phase. This is fine for
most Rails apps, but it won't work for those which need to connect to services (such as the database)
during asset compilation. (For an example, see [MyUSA issue #636](https://github.com/18F/myusa/issues/636))

There are multiple potential solutions for this. For more advice, see
[the Cloud Foundry document on the subject](https://docs.cloudfoundry.org/buildpacks/ruby/ruby-tips.html#precompile).

