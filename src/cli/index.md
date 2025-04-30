# Basalt CLI

The Basalt CLI is a tool for packet designers and competition administrators
for provisioning servers, generating packet PDF documents, and verifying
server configurations.

The Basalt CLI is [Open Source](https://github.com/basalt-rs/basalt-cli).

## Provisioning a Server

To build a server, you first must have a valid server configuration. By
default this is a `basalt.toml` file in the current working directory, but
any other valid file can be supplied.
To get started with an example configuration, you can run the `basalt init` command.

*NOTE: The Basalt Server leverages docker for security and portability*

```
basalt build
```

With no arguments provided, the Basalt CLI will attempt to build a docker
image using `basalt.toml` as the configuration. This docker image will be
tagged with "bslt" prepended to the hash of the configuration.

*NOTE: Not all changes have any affect on the hash [More Info](../config/hashing.md)*

You can now run your container:

```
docker run -p <outer port>:9090 <conatiner name>
```

Soon, you will be able to simply run `basalt run` to run your server.
