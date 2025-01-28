# Language Config

Configuration for languages that may be used by competitors.  We have a
number of [built-in languages](#built-in-languages), but also offer support for adding [custom
languages](#custom-languages).

```toml
[languages]
# Enable python3 default
python3 = "*"
# Enable built-in Java 21
java = "21"
# Add custom `ocaml` language type
[languges.ocaml]
build = "ocamlc -o out {{SOURCEFILE}}"
run = "./out"
```

## Built-in Languages

- `python3`
- `java`
    - versions: `8`, `11`, `21`
- `javascript`
- `rust`

## Custom Languages

Custom languages may be specified by using a table instead of the
version.

| Key     | Optional | Description                                                                                                                                                                      |
| ------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `build` | true     | The command that will be used to build the solution.  This is run in a temporary directory that gets deleted after all tests have run, so extra generated files will be removed. |
| `run`   | false    | The command that will be used to run the solution.  This is run in a temporary directory that gets deleted after all tests have run, so extra generated files will be removed.   |
| `name`  | true     | Optional name for this language profile.  This will be used in the UI.                                                                                                           |
