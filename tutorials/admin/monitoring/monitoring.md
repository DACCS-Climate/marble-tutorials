# Monitoring the Marble stack

Marble is deployed using the [Birdhouse](https://github.com/bird-house/birdhouse-deploy) software. This software
includes some useful tools to monitor the usage and logs of your Marble node.

These tools help you check inspect how your node is being used and can help you understand how to better allocate 
resources to ensure that your users get the best experience possible from your node.

(grafana)=
## Monitoring with Grafana and Prometheus

[Prometheus](https://prometheus.io/) is a metrics reporting tool that collects information about your server and each of
the docker containers running on it to provide you an overview of how each is being used.

[Grafana](https://grafana.com/grafana/dashboards/) is a visualization dashboard that takes the information collected by
[Prometheus](https://prometheus.io/) and presents it to you in a visually useful manner.

These monitoring tools can also send you email alerts when certain thresholds are reached. The threshold checks are 
pre-defined and include, for example:

- the server is running low on memory, inodes, disk space, etc.
- the server is too hot (physical machines only)
- the server is swapping too much
- containers are using too large a percentage of total memory
- and many more.

For instructions on how to enable this component and customize it for your usage, see the birdhouse documentation for
this [monitoring component](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/components/README.html#monitoring).

### Inspecting the Dashboard

To inspect the Grafana dashboard, first log in as an administrator user and then navigate to 
`https://yournodeshostname.com/grafana` (replace `yournodehostname.com` with the actual hostname of your node).

You will be asked to log in to the Grafana service itself. Use the password that you set when you set up the monitoring
component to log in.

```{note}
Any administrator user will have access to the Grafana dashboard. If you want to give a user permission to access the
dashboard without giving them full administrator access, you can add them to the "monitoring" group in Magpie.

See the [user tutorials](../users/users.md) for details.
```

## Inspecting Docker logs

Sometimes you may want to inspect the Marble logs directly. This will allow you to investigate whether a specific
component is behaving as expected. Also, if you ever need to submit a bug report, you may be asked to include some of
the log output to help determine the cause of the bug.

Marble uses [docker](https://www.docker.com/) underlyingly to deploy the various components in the stack. Docker keeps
a log for each of the containers deployed in the stack. 

To inspect the logs, we first need to figure out which container's logs we want to inspect.

To see which containers are running in your stack, first navigate to the `birdhouse-deploy` source code directory on
your server and go to the `birdhouse/` subdirectory:

```shell
cd birdhouse-deploy/birdhouse
```

Then run the `pavics-compose.sh` script with the `ps` subcommand. This will show all running containers in the stack in
a table format.

```shell
./pavics-compose.sh ps
```

Select which container you want to inspect and take note of the value in the "Name" column in the table.

Now to inspect the logs of this container you can run the `docker logs <name here>` command (replace `<name here>` with
the name of the container you want to inspect). For example, to inspect the logs for the container named `proxy`:

```shell
docker logs proxy
```

If you're not sure which container to inspect, the container names should be the same as the component names as
described in the 
[Birdhouse documentation](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/components/README.html#).

## Provide a public status page with Canarie-API

Canarie-API provides a simple view of the status of various components of your Marble node. This is useful when you want
to allow users to easily check whether services are working as intended without making sensitive information about your
node public.

See the [documentation](https://birdhouse-deploy.readthedocs.io/en/latest/birdhouse/components/README.html#canarie-api) 
on how to enable the Canarie-API component for details.

```{warning}
If the Canarie component is enabled, the logs from the proxy service will not be available in the normal method.

In other words, the following will show the canarie logs, not the proxy logs:

:::
docker logs proxy
:::

To inspect the proxy logs when the canarie component is enabled:

:::
docker exec proxy cat /var/log/nginx/access_file.log
:::
```
