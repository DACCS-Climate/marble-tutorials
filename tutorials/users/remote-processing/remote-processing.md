# Remote Processing

Remote processing services allow users to run workflows on different nodes across the Marble network.

Climate data is distributed across the Marble network to reduce the burden on any single node. The remote processing 
capability allows users to run their workflows on the same server where the data is located.

In other words, instead of downloading large amounts of data in order to run workflows on their own
computers, users can send their workflows to the computer that hosts the data to run there. This reduces lengthy
download/transfer times and eliminates the need to duplicate data unnecessarily.

The [Weaver](https://pavics-weaver.readthedocs.io) service provides remote processing capabilities across the Marble 
Network. Any node that enables the Weaver service will allow users to run workflows on that node from anywhere else in 
the network.

## How Weaver works

Weaver is an Execution Management Service (EMS) where users can send instructions in the form of workflows which are 
then sent to different Application Deployment and Execution Services (ADES) for execution. These ADES can either be
Weaver services running on different nodes on the Marble Network, or external servers outside the Marble Network that
provide an interface for one of the [atomic processes](atomic-processes) that Weaver supports.

A workflow can contain a single process step or multiple.

Processes can be run in either synchronous or asynchronous mode. 

- A synchronous process will block until it has finished and then return the result of the process. 

- An asynchronous process will immediately return a response containing a URL that can be used to check the status of 
  the process and to retrieve the result once the process has finished. A user running an asynchronous process is 
  responsible for checking back later to check if the process has finished.

```{note}
If a synchronous process takes too long (reaches a timeout threshold), the process will be converted to asynchronous
mode. This threshold is 20 seconds by default but may be different depending on the specific configuration of the Weaver
service running on your Marble node.
```

(atomic-processes)=
### Atomic Processes

Weaver supports several types of atomic processes. These processes receive inputs in the form of data and customization
arguments and return their results to the user.

Atomic processes include:

- [builtin](https://pavics-weaver.readthedocs.io/en/latest/processes.html#proc-builtin)
  - These processes come built into Weaver. No additional steps are required to deploy these processes.
- [Web Processing Service (WPS)](https://pavics-weaver.readthedocs.io/en/latest/processes.html#wps-1-2)
  - These processes are executed by a remote server through the [WPS 1/2](https://www.ogc.org/standard/wps/) interface.
- [OGC API - Processes](https://pavics-weaver.readthedocs.io/en/latest/processes.html#ogc-api-processes-wps-rest-wps-t-wps-3)
  - These processes are the core components of Weaver. 
    - Users can define these processes as [application 
      packages](https://pavics-weaver.readthedocs.io/en/latest/package.html#application-package) and deploy them for 
      later execution.
- [ESGF-CWT](https://pavics-weaver.readthedocs.io/en/latest/processes.html#esgf-cwt)
  - These processes are executed by a remote server through the [ESGF Compute API](https://github.com/ESGF/esgf-compute-api)
    interface.

```{note}
Weaver converts all process types to OGC API - Processes internally. This allows users to interact with all processes
using the same [REST](https://en.wikipedia.org/wiki/REST) interface that Weaver provides. 

This makes dealing with multiple different process types easier since the user can interact with all process types 
through the same interface.

For example, WPS 1/2 processes normally have a [SOAP](https://en.wikipedia.org/wiki/SOAP) interface. Weaver simplifies
the interaction for the user by translating the SOAP payloads to JSON as expected by Weaver's REST interface. In other
words, if a user can use Weaver, they don't have to learn the WPS protocol in order to execute WPS processes.
```

### Workflow Processes

By chaining atomic processes into multistep workflows, Weaver can be used to accomplish complex data processing tasks.

Weaver dispatches each step in the workflow to the appropriate node in the network for execution. It handles data
transfers if needed and tries to minimize data transfers by executing workflow steps on the same node where the data
needed for that step is hosted. Only the result from the last step in the process will be returned to the user.

Workflows are defined using the [common workflow language (CWL)](https://www.commonwl.org/) which describes which atomic
processes to execute in what order and how the data should be transferred between steps. Workflows can contain atomic
processes hosted on different nodes in the network if needed.

## The Weaver python client

The Weaver software comes with a command line interface (CLI) and a python client. In order to run either, you need the
weaver python package installed. 

This package may already be installed if you're working in a [Marble Jupyterlab](../ide/jupyterlab-howto.md) 
environment. To test whether the package is installed, run the following command in a JupyterLab console:

```
import weaver
```

If the package is not installed you can install it from the git repository with the `pip` command. Run the following
in a JupyterLab console:

```
import sys
import subprocess
subprocess.run([sys.executable, "-m", "pip", "install", "git+https://github.com/crim-ca/weaver.git"])
```

### Using the python client

The main component of Weaver is the process and so most of the interaction that you will have with the Weaver API will
involve inspecting, executing, and managing processes.

To interact with Weaver, first create a `weaver_client` object:

```
from weaver.cli import WeaverClient
weaver_client = WeaverClient("https://<your-node-url>/weaver")
```

```{tip}
If you are in a [Marble JupyterLab IDE](../ide/ide.html) and you have the 
[Marble python client](../python-client/python-client.html) installed, you can use this code snippet instead so you
don't have to explicitly write out the URL.

:::
from weaver.cli import WeaverClient
from marble_client import MarbleClient
marble_client = MarbleClient()

weaver_client = WeaverClient(marble_client.this_node.weaver.url)
:::
```

<!-- TODO: add in authentication info once https://github.com/crim-ca/weaver/pull/599 has been merged -->
<!-- TODO: add in information about discovering and executing providers as well as processes -->

(weaver-client-discover)=
#### Discover processes

To discover which processes are available on a Weaver service installed on a Marble node use the
[`capabilities` method](https://pavics-weaver.readthedocs.io/en/latest/cli.html#getcapabilities-example):

```
weaver_client.capabilities()
```

This will return an object containing a list of process names. To inspect the details of each process use the
[`describe` method](https://pavics-weaver.readthedocs.io/en/latest/cli.html#describeprocess-example)

```
weaver_client.describe("process_name_here")
```

The description should include a plain language description of what the process does as well as describing expected
inputs and outputs. Take note of the inputs especially as that will inform how you can execute this process.

#### Execute a process

To execute a process use the [`execute` method](https://pavics-weaver.readthedocs.io/en/latest/cli.html#execute-example):

```
weaver_client.execute("process_name_here", inputs={...})
```

where the value of the `inputs` argument are the expected inputs of this process. The format of these inputs can be
determined by the [`describe` method](weaver-client-discover).

For more details, see the [Weaver documentation on the execution of a 
process](https://pavics-weaver.readthedocs.io/en/latest/processes.html#execution-of-a-process-execute)

The `execute` command will either block until the process has finished (in synchronous mode) or will return a dictionary
containing a job id (in asynchronous mode). This job id can be used to get the status of the job with the [`status` 
method](https://pavics-weaver.readthedocs.io/en/latest/cli.html#getstatus-example):

```
weaver_client.status("job_id_here")
```

which will return a dictionary containing the job's status as well as lots of useful information about the job.

Once the job has completed successfully, the results of an asynchronous job can be inspected with the [`results` 
method](https://pavics-weaver.readthedocs.io/en/latest/cli.html#results-example)

```
weaver_client.results("job_id_here")
```

By default, this will return information containing a URL where the results can be downloaded from. If you want to
download the results directly you can specify the `download` argument:

```
weaver_client.results("job_id_here", download=True, out_dir="destination_dir")
```

where `destination_dir` is a path to a folder where you want the download to go.

#### Manage processes

Weaver also lets you create and manage your own processes. New processes can be added to a Weaver instance using the 
[`deploy` method](https://pavics-weaver.readthedocs.io/en/latest/cli.html#deploy-example):

```
weaver_client.deploy("new_process_id", ...)
```

where `...` corresponds to the definition of this new process. The definition is provided as an application 
package.

The details of the application package structure are beyond the scope of this tutorial. Please see the [Weaver 
documentation](https://pavics-weaver.readthedocs.io/en/latest/package.html#application-package) for details.
