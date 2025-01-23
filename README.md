# Basalt Manual

This is the repo which hosts the source for the Basalt Manual.

To build, you must have both [mdBook](https://github.com/rust-lang/mdBook) and
[mdBook-pagetoc](https://github.com/slowsage/mdbook-pagetoc) installed.

To build, you can run

```sh
mdbook build
```

To build the book into `book/`

For development, use 

```sh
mdbook serve [-p <port>]
```

to build and serve (with hot reload) on a given port.
