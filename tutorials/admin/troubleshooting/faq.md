# Frequently Asked Questions

```{contents}
:local:
```

### I cannot run docker as a non-root user

Docker requires root permissions to run. If you do not want to manage Marble as the root user then you can configure
Docker to permit access to users in the `docker` group. 

To set this up, see the instructions here: 
https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user

### The webpage says my SSL certificate has expired, what do I do?

Before you do anything else, you should update your SSL certificate.

If your SSL certificate is provided to you by your domain name service or through a cloud provider, check their
documentation on how to update your certificate. 

If you got your SSL certificate through a service like [Let's Encrypt](https://letsencrypt.org/) then you can use a tool like 
[certbot](https://certbot.eff.org/) to update it.

Once your certificate has been updated, make sure that you've created a file that combines the 
`privkey.pem` and `fullchain.pem` files and ensure that that file is set as the value of the `SSL_CERTIFICATE` variable
in the `env.local` file. See the [installation example](example-installation-steps) for an example of this step.
