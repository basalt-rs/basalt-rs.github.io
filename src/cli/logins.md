# Logins PDF Generation

A PDF with logins can be generated using the basalt CLI.  To do so, you must
first have a valid basalt server configuration.  By default, the CLI
uses `basalt.toml` in the current directory, but a different path may be
specified, if necessary.

## Generating the Packet

To generate the logins packet, run the following command.

```sh
basalt render-logins [config.toml]
```

This command will create a PDF with the same name as your config (with
`-logins`) that looks like the one shown [below](#example).

The output file may be changed using the `-o` or `--output` flag.

## Customising the Template

The PDF is generated using [Typst](https://typst.app/) with a default
template found [here](https://github.com/basalt-rs/bedrock/blob/main/data/login-template.typ).
This template may be changed by passing the path to a template file using `-t` or `--template`.

Templates are provided with the following values:

| Name          | Type                | Description                                                                           |
| ----------    | ------------------- | ------------------------------------------------------------------------------------- |
| `title`       | `str`               | The title of the competition, as specified in the config                              |
| `preamble`    | `content` or `none` | The rendered markdown from the preamble, if specified in the config, otherwise `none` |
| `competitors` | `Login[]`           | The competitors' logins                                                               |
| `hosts`       | `Login[]`           | The hosts' logins                                                                     |

### Login

A `Login` consists of the following fields:

| Name       | Type  | Description                |
| ---------- | ----- | -------------------------- |
| `username` | `str` | The username of this login |
| `password` | `str` | The password of this login |

## Example

<object data="./uil-logins.pdf" type="application/pdf" width="100%" height="600px">
    <p>Unable to display PDF file. <a href="./uil-logins.pdf">Download</a> instead.</p>
</object>
