# Services

The Marble software can be configured to provide a variety of services to the users of your node. Services are 
user-facing tools that largely fall under the following categories:

- serving and cataloging data hosted on your server
- interactive development environment
- remote processing tools

(enable)=
## Enable an included service

The Marble software comes with several services already included. The list of services already included can be found
in the 
[Birdhouse documentation](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/components/README.html). This 
documentation explains what each service is used for and how to enable and configure it.

You can pick and choose which services you would like to offer your users by enabling them via the `env.local` file.

In general, the process to enable a service is a follows:

1. Take note of the directory that contains the service's code. In general this will be one of the directories in the
   `birdhouse/components` folder.
2. Edit the `EXTRA_CONF_DIRS` variable in the `env.local` file to include the service's directory. This is a relative 
   path from the `birdhouse/` directory *or* an absolute path. For example, to enable the Thredds service add the
   string `./components/thredds` to the `EXTRA_CONF_DIRS` variable.
3. Add or update any additional variables in `env.local` as required by the specific service (see the 
   [Birdhouse documentation](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/components/README.html)
   for customization options for each service).
4. Restart the software by running:

   ```shell
   ./pavics-compose.sh down
   ./pavice-compose.sh up -d
   ```

   in order for the changes to take effect.
5. Log in to [Magpie](https://pavics-magpie.readthedocs.io/) as an admin user to [set the access permissions for the new
   service](../users/permissions.md)

```{note}
Note that the [STAC catalog service](../../users/catalog/catalog.md) is always enabled by default.
```

### Service customizations

The Marble software also includes some useful service customizations. These are commonly used overrides that configure
the default services in different ways. Details can be found in the 
[Birdhouse documentation](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/optional-components/README.html).

To enable any of these customizations, follow the same steps as [enabling a service](enable). Make sure that the
customization is added to the `EXTRA_CONF_DIRS` variable **after** the service that it meant to customize. This is to 
ensure that any changes to the settings in the customization are applied after the default settings.

```{warning}
Some of the service customizations described in 
[Birdhouse documentation](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/optional-components/README.html)
are meant for testing purposes only and are **not** meant to be deployed on a production server. Please read the
description carefully before enabling any of these customizations.
```

## Enable an external service

You are not restricted to only using the services that are provided by the 
[Birdhouse software](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/components/README.html).
The Marble software is extendable, and we encourage you to create, share, and deploy custom services as needed for your
specific use cases.

To enable an external service, first download or create the service files in a folder outside the `birdhouse-deploy`
repository. Then enable the service [as described above](enable) with the following minor changes:

- ensure that the path added to `EXTRA_CONF_DIRS` in `env.local` is an *absolute* path. Relative paths from the
  `birdhouse` directory will not work for external services.
- carefully read any additional documentation that comes with the external component to ensure that you take any 
  additional configuration steps as well.
