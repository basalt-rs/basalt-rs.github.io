# Packet Configuration

Configuration for the packet of questions that is used for prompts and
testing of problems.

```toml
[packet]
title = "Example Packet"
preamble = '''
This is an optional preamble that has markdown support.  This preamble
will be shown on the first page of the packet.
'''

[[packet.problems]]
title = "Reversing a string"
description = '''
Accept a single string as input.  You must reverse the order of this
string and print it back out.
'''

[[packet.problems.tests]]
input = "hello"
output = "olleh"
visible = true
trim_output = true

[[packet.problems.tests]]
input = "world"
output = "dlrow"
visible = true
trim_output = true

[[packet.problems.tests]]
input = ""
output = ""
trim_output = true

[[packet.problems.tests]]
input = "aa"
output = "aa"
trim_output = true

[[packet.problems.tests]]
input = "racecar"
output = "racecar"
trim_output = true
```

## Problems

The `problems` array contains all of the problems that will be presented
to the user in packet.

- `title` - the title of this problem, this will also be used as a preview
  in the UI.
- `description` - Detailed description of this problem, supports Markdown
- `supported_languages` - Optional list of languages that are allowed
  for this problem.  All languages must appear in the [Languages
  configuration](./languages.md).

### Tests

Each problem contains a suite of tests that will be used to validate the
code that the competitor has submitted.

- `input` - Input that will be provided to the competitor's program
  through standard input
- `output` - Expected output that the competitor's code should produce
  out to standard output
- `trim_output` - Whether the output should be have starting and trailing
  whitespace removed before comparing.  i.e., `" hello "` would match
  `"hello"`
- `visible` - Whether this test should be visible to the user.  The
  first visible test listed will be shown as an example in the problem
  description.

## Imports

Many items in the packet spec may be imported from neighbouring files.

`packet`:

```toml
packet = { import = "./packet.toml" }
```

`packet.preamble`:

```toml
[packet]
preamble = { import = "./preamble.md" }
```

`packet.problems`:

```toml
[[packet.problems]]
import = "./problem1.toml"

[[packet.problems]]
import = "./problem2.toml"

# OR

[packet]
problems = [{ import = "./problem1.toml" },
            { import = "./problem2.toml" }]
```
