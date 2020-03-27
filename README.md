# olric-docker

This repository contains Dockerfiles for the official [Olric](https://github.com/buraksezer/olric) Docker images.

## Table of Contents

* [Quick Start](#quick-start)
  * [Olricd](#olricd)
  * [Hello World](#hello-world)
  * [Using Custom Configuration File](#using-custom-configuration-file)
  * [Extending Olricd Base Image](#extending-olricd-base-image)
* [Plugins](#plugins)
  * [olric-consul-plugin](#olric-consul-plugin)
  * [olric-cloud-plugin](#olric-cloud-plugin)
   
## Quick Start

### Olricd

You can launch Olricd Docker container by running the following command. 

```
docker run olricio/olricd:latest
``` 

This command will pull Olricd Docker image and run a new Olric Instance. You should know that the container 
exposes `3320` and `3322` ports. 

### Hello World

```
docker run -p 3320:3320 olricio/olricd:latest
``` 

`3320` is the client port. So you can run commands on this Olric instance. In order to do this, you need to install 
`olric-cli`:

```
go get -u github.com/buraksezer/olric/cmd/olric-cli
```

If `olric-cli` installed successfully, you can access the instance:

```
olric-cli
[127.0.0.1:3320] » use my-dmap
use my-dmap
[127.0.0.1:3320] » put my-key my-value
[127.0.0.1:3320] » get my-key
my-value
[127.0.0.1:3320] »
```

There is another tool to test the instance. It's called `olric-load`. You can install it by using the following command:

```
go get -u github.com/buraksezer/olric/cmd/olric-load
```

Call `Put` for 1000 keys on the instance:

```
olric-load -a 127.0.0.1:3320 -s msgpack -k 1000 -c put
```

Then call `Get` on the instance:

```
olric-load -a 127.0.0.1:3320 -s msgpack -k 1000 -c get
```

### Using Custom Configuration File

If you need to configure Olric with your own `olricd.yaml`, you need to mount the folder that has `olricd.yaml`. You also need to pass the 
`olricd.yaml` file path to `OLRICD_CONFIG` environment variable. Please see the following example:

```
$ docker run -e OLRICD_CONFIG=/etc/olricd/config_ext/olricd.yaml  -v PATH_TO_LOCAL_CONFIG_FOLDER:/etc/olricd/config_ext olricio/olricd:latest
```

### Extending Olricd Base Image

You can use Olricd Docker Image to start a new Olric member with default configuration. If you'd like to customize your Olric member, 
you can extend the Olricd base image, provide your own configuration file and customize your initialization process. In order to do that, 
you need to create a new `Dockerfile` and build it with `docker build` command. 

In the `Dockerfile` example below, we are creating a new image based on the Olricd image and adding our own configuration file from our host 
to the container, which is going to be used with Olric when the container runs.

```
FROM olricio/olricd:latest

# Adding custom olricd.yaml
ADD olricd.yaml /etc/olricd.yaml
```

After creating the `Dockerfile` you need to build it by running the command below:

```
$ docker build .
```

Now you can run your own container with its ID or tag (if you provided `-t` option while building the image) using the `docker run` command.

## Plugins

### olric-consul-plugin

### olric-cloud-plugin

## Contributions

Please don't hesitate to fork the project and send a pull request or just e-mail me to ask questions and share ideas.

## License

The Apache License, Version 2.0 - see LICENSE for more details.