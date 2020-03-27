# olric-docker

This repository contains Dockerfiles for the official Olric Docker images.

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
[127.0.0.1:3320] » use my-first-olric-instance
use my-first-olric-instance
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

## Contributions

Please don't hesitate to fork the project and send a pull request or just e-mail me to ask questions and share ideas.

## License

The Apache License, Version 2.0 - see LICENSE for more details.