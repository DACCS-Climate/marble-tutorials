# Installation

This tutorial describes how to install a Marble node on a server. 

## Prerequisites

### Docker

Marble is deployed as a [Docker](https://www.docker.com/) application using the 
[compose](https://docs.docker.com/compose/) tool to manage various services that make up the application.

To install Docker on Unix/Linux either install [Docker Engine](https://docs.docker.com/engine/install/) (recommended) or
[Docker Desktop](https://docs.docker.com/desktop/). If using an operating system other than Unix/Linux, you must use
Docker Desktop.

```{warning}
We highly recommend installing Marble on a Unix/Linux machine, specifically Ubuntu 18.04+ if possible. All code is 
developed and tested on Ubuntu, and we cannot guarantee that the software will behave as expected on other operating 
systems.
```

### Secure Access Over the Internet

Marble is designed to be deployed as a web application on the internet. To make this possible, you must provide a domain
name where your Marble node can be reached online. Marble also requires that all internet traffic to and from your
Marble node be encrypted using an SSL certificate.

Specifically, you will need to ensure that your have the following:

- [](fqdn)
- [](public-ip)
- [](ssl-cert)

Depending on your situation and where your server is located (on premises at your institution, a VM in a cloud
environment, etc.) the details of how to acquire each of the above will vary.

However, here are some recommendations on where to look if you've never set up a publicly available web application like
this before.

(fqdn)=
#### A fully qualified domain name (FQDN)

You can usually purchase a domain name from one of the various domain name providers online. Search for "domain name
provider" online. You may have to shop around a bit to find one that best fits your needs and budget.

If you are hosting your Marble node in a cloud environment, most cloud service providers also provide a free or
discounted domain name with your purchase of a cloud based virtual machine.

(public-ip)=
#### A static public IP address for your server

A static public IP address is required so that the domain name server will know where to forward internet traffic to.

If you are hosting your Marble node in a cloud based environment, follow the instructions from your cloud service 
provider on how to forward internet traffic to your virtual machine.

If you are installing Marble on premises at an institution, contact the institution's IT department to ask how to
acquire your public static IP for the purposes of setting up a web application.

```{note}
Most residential internet service plans only provide *dynamic* public IP addresses, which are not suitable for hosting
a web application. You may be able to request a static IP address from your internet service provider (ISP) for a small 
fee depending on your ISP and/or geographical region.
```

(ssl-cert)=
#### An SSL certificate for the FQDN

An SSL certificate will encrypt all internet traffic to and from your server allowing Marble to use the HTTPS protocol.

You may be able to acquire an SSL certificate from the same place that you purchased your [domain name](fqdn).

Otherwise, you can acquire a certificate from organizations like [Let's Encrypt](https://letsencrypt.org).

We recommend using a tool like [certbot](https://certbot.eff.org/) to get and manage SSL certificates if you are
managing them yourself.

```{note}
If using [certbot](https://certbot.eff.org/), note that the Marble stack uses 
[nginx](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/) as a reverse proxy.

Certbot also requires that the website be already running and that ports 80 and 443 are open.
To deploy the stack and start the website see the instructions [here](deploy-marble).
```

### Git

The Marble source code is hosted on [GitHub](https://github.com) and a `git` client is highly recommended to download 
and update the source code.

Your server may already have `git` installed. To check run the following command from the command line:

```shell
git --version
```

The output should be some information about the version of `git` currently installed on your machine.

If you do not have `git` installed, it can be installed from https://git-scm.com/downloads. Select your operating system
for information on how to install `git`.

## Marble

Marble is deployed using software named [Birdhouse](https://github.com/bird-house/birdhouse-deploy/).

### Download the Birdhouse software

```shell
git clone https://github.com/bird-house/birdhouse-deploy.git
```

This will download the [Birdhouse](https://github.com/bird-house/birdhouse-deploy/) source code to the current 
directory.

The most up-to-date version of the source code is on the `master` branch. We recommend always using this branch.

### Create the local environment file

Your Marble deployment can be configured and customized by editing a local environment file. To create this file:

```shell
cd birdhouse-deploy/birdhouse
touch env.local
```

An (incomplete) example of this file named `env.local.example` can be used as a starting point. 

```{warning}
`env.local.example` contains a lot of default examples that *must* be updated. For this reason, we do not recommend 
just copying `env.local.example` to `env.local`
```

### Configure `env.local`

The `env.local` file contains environment variables that are used when deploying the Marble software.

Instructions on which variables should be set in this file can be found in `env.local.example`. Please refer to this
file which will instruct you:

- which variables *must* be set for all deployments
- which variables can be modified to customize your deployment
- how to enable additional components and which variables to set to customize these components

(deploy-marble)=
## Deploying Marble

The Marble stack can be started, stopped and inspected using the `pavics-compose.sh` script which takes the same 
arguments as the [`docker compose`](https://docs.docker.com/compose/) commands.

The `pavics-compose.sh` script will read the `env.local` configuration file, create a `docker compose` deployment file
based on this configuration and then execute any subcommands provided to the `pavics-compose.sh` file as subcommands to 
`docker compose` based on that file. 

For example, to start the Marble stack:

```shell
cd birdhouse-deploy/birdhouse
./pavics-compose.sh up --detach
```

This will call the [`docker compose up --detach`](https://docs.docker.com/engine/reference/commandline/compose_up/)
which will start up all the docker containers required to run the Marble stack.

Similarly, to stop and bring down the stack use:

```shell
cd birdhouse-deploy/birdhouse
./pavics-compose.sh down
```

which will call `docker compose down` internally.

## Check that everything is working

Once you have started the Marble stack with the `./pavics-compose.sh up --detach` command, check that everything is
working properly by opening your webpage in a browser:

- Navigate to the domain name [that you set up](fqdn)
- Ensure that the page loads as expected
  - Note that the page that loads should be the one set by the `PROXY_ROOT_LOCATION` variable in `env.local`
- Ensure that the connection is secure (uses the https protocol with a valid certificate)
  - If not: ensure that your SSL certificate is up-to-date and that `SSL_CERTIFICATE` variable in `env.local` is
    pointing to the correct file (see the birdhouse documentation for details)

## Next Steps

Now that you know the basics of how to configure and deploy the Marble stack you can select which optional components
you would like to add to your stack:

- [Monitoring and Logging components](../monitoring/monitoring.md)
- [User-facing Services](../services/services.md)

Once you've done that, you will likely want to add your new node to the Marble network:

- [Network](../network/network.md)

If you want to host data on your node:

- [Data hosting](../data/data.md)

And finally you'll want to start adding users to your node:

- [User management](../users/users.md)

(example-installation-steps)=
## Example installation steps

Here is an example of how to install Marble on a server running Ubuntu 20.04, using <span>mymarble</span>.com as a FQDN,
and where we get an SSL certificate using [certbot](https://certbot.eff.org/). We assume that 
[docker](https://www.docker.com/) and [git](https://git-scm.com/) are already installed:

```shell
# Download source code
git clone https://github.com/bird-house/birdhouse-deploy.git
cd birdhouse-deploy/birdhouse

# Configure env.local
echo "export PAVICS_FQDN=mymarble.com" > env.local
echo "export DOC_URL='https://marbleclimate.com'" >> env.local
echo "export MAGPIE_SECRET=$(openssl rand -hex 32)" >> env.local
echo "export MAGPIE_ADMIN_USERNAME=admin" >> env.local
echo "export MAGPIE_ADMIN_PASSWORD=$(openssl rand -base64 12)" >> env.local
echo "export SUPPORT_EMAIL=info@mymarble.com" >> env.local
echo "export POSTGRES_PAVICS_USERNAME=postgres-pavics" >> env.local
echo "export POSTGRES_PAVICS_PASSWORD=$(openssl rand -base64 12)" >> env.local
echo "export POSTGRES_MAGPIE_USERNAME=postgres-magpie" >> env.local
echo "export POSTGRES_MAGPIE_PASSWORD=$(openssl rand -base64 12)" >> env.local

echo "export EXTRA_CONF_DIRS='...'" >> env.local # fill in the ... with the additional components you want to add

# Get an SSL certificate with certbot
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot certonly --apache --domain mymarble.com # and follow any additional instructions

# Create a file that contains a combination of the fullchain.pem and the privkey.pem files
sudo cat /etc/letsencrypt/live/mymarble.com/fullchain.pem /etc/letsencrypt/live/mymarble.com/privkey.pem > cert.pem
echo "export SSL_CERTIFICATE=$(pwd)/cert.pem" >> env.local

# Start the server
./pavics-compose.sh up -d
```
