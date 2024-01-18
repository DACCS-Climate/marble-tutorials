# Updating the Software

Occasionally Marble will release updates to its software. These updates may include bugfixes, feature updates, and
security patches. 

It is important to keep your Marble node up to date. This is especially important if your node is part of the Marble
network so that we can ensure that all nodes in the network are secure and provide predictably similar features.

### Updating to the latest version

Before you start have a look at the [CHANGES.md](https://github.com/bird-house/birdhouse-deploy/blob/master/CHANGES.md) 
file in the [Birdhouse repository](https://github.com/bird-house/birdhouse-deploy) to see what changes have been made in
the most recent versions.

Most version updates won't require any additional manual actions from you but if there are any, they will be explained
in this file. Please take note of any manual actions or additional instructions for later.

For example, the [CHANGES.md](https://github.com/bird-house/birdhouse-deploy/blob/master/CHANGES.md) file might tell you
that new environment variables need to be added to the `env.local` file, or that certain components are deprecated.

First navigate to the directory that contains the `birdhouse-deploy` source code:

```shell
cd birdhouse-deploy
```

Then use the `pavics-compose.sh` script to stop the stack momentarily while you update the code:

```shell
cd birdhouse
./pavics-compose.sh down
```

Update the source code to the latest version using git:

```shell
git pull
```

There should not be any merge conflicts but if there are, resolve them now and allow git to finish the pull.

```{note}
There should be no merge conflicts because you should *NOT* be manually editing the source code directly.
If you would like to customize existing components or add additional ones, please see the instructions in the [custom
overrides](../services/custom-overrides.md) tutorial.
```

Now perform any of the manual actions that you noted in a previous step. This will often only require you to update the
`env.local` file.

Now start the stack up again:

```shell
./pavics-compose.sh up --detach
```

Navigate to your node's URL in a browser and ensure that everything is running as expected.

```{warning}
You must stop and restart the Marble software for the changes to take affect. This means that your Marble node will 
be offline for up to several minutes. 

To avoid disruption to your users as much as possible we recommend warning your users before performing this update.
Or at the very least, do the update at off-peak times when you expect minimal usage of the software.
```
