# Packet Generation

A packet can be generated using the basalt CLI.  To do so, you must
first have a valid basalt server configuration.  By default, the CLI
uses `basalt.toml` in the current directory, but a different path may be
specified, if necessary.

## Generating the Packet

To generate the packet, run the following command.

```sh
basalt render [config.toml]
```

This command will create a PDF with the same name as your config that
looks like the one shown [below](#example).

The output file may be changed using the `-o` or `--output` flag.

## Customising the Template

The PDF is generated using [Typst](https://typst.app/) with a default
template found [here](https://github.com/basalt-rs/bedrock/blob/main/data/template.typ).
This template may be changed by passing the path to a template file using `-t` or `--template`.

Templates are provided with the following values:

| Name       | Type                | Description                                                                           |
| ---------- | ------------------- | ------------------------------------------------------------------------------------- |
| `title`    | `str`               | The title of the competition, as specified in the config                              |
| `preamble` | `content` or `none` | The rendered markdown from the preamble, if specified in the config, otherwise `none` |
| `problems` | `Problem[]`         | List of problems from the config                                                      |

### Problem

A `Problem` consists of the following fields:

| Name          | Type                | Description                                                                              |
| ------------- | ------------------- | ---------------------------------------------------------------------------------------- |
| `title`       | `str`               | The title of the problem, as specified in the config                                     |
| `description` | `content` or `none` | The rendered markdown from the description, if specified in the config, otherwise `none` |
| `languages`   | `str[]`             | Languages allowed for this problem                                                       |
| `tests`       | `Test[]`            | Tests for this problem                                                                   |

### Tests

A `Test` consists of the following fields:

| Name      | Type   | Description                                                 |
| --------- | ------ | ----------------------------------------------------------- |
| `input`   | `str`  | The input to the test, as specified in the config           |
| `output`  | `str`  | The expected output of the test, as specified in the config |
| `visible` | `bool` | Whether this test case is marked as visible                 |

## Example

<object data="./uil.pdf" type="application/pdf" width="100%" height="600px">
    <p>Unable to display PDF file. <a href="./uil.pdf">Download</a> instead.</p>
</object>
