# Setup Configuration

The setup configuration is used to declare how the docker container
should be built.

```toml
[setup]
install = '''
apt-get install opam
'''

init = '''
opam init -y
eval $(opam env)
'''
```

## Imports

The value of both `install` and `init` may be replaced with an import to
read from another file:

```toml
[setup]
install = { import = "./install.sh" }
init = { import = "./init.sh" }
```

## Fields

| name      | type          | range       | default | description                                                                                                                                                   |
| ------    | -------       | ----------- | ------- | -----------------------------------------------------------                                                                                                   |
| `install` | string/import | N/A         | None    | A shell script that will be run while building the docker container.  Used for installing programs for language support                                       |
| `init`    | string/import | N/A         | None    | A shell script that will be run before the basalt server is started.  Used for initialising environment variables that may be necessary for language support. |
