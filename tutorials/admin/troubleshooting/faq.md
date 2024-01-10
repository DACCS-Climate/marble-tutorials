# Frequently Asked Questions

## I cannot run docker as a non-root user

Docker requires root permissions to run. If you do not want to manage Marble as the root user then you can configure
Docker to permit access to users in the `docker` group. 

To set this up, see the instructions here: 
https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user

## The webpage says my SSL certificate has expired, what do I do?

First, you should update your SSL certificate. 

If your SSL certificate is provided to you by your domain name service or through a cloud provider, check their
documentation on how to update your certificate. 

If you got your SSL certificate through a service like [Let's Encrypt](https://letsencrypt.org/) then you 
