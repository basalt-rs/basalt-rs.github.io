# Configuration

The configuration of basalt is written using [toml].
This configuration is used by the [`basalt-cli`] and the [`basalt-server`]
to host a competition.

[toml]: https://toml.io/en/v1.0.0
[`basalt-cli`]: https://github.com/basalt-rs/basalt-cli
[`basalt-server`]: https://github.com/basalt-rs/basalt-server

The configuration is broken up into four main sections:

- [Runtime Config](./runtime.md)
- [Setup Config](./setup.md)
- [Language Config](./languages.md)
- [Account Config](./account.md)
- [Packet Config](./packet.md)

## Example

An example configuration is shown below.

```toml
# Host competition on port 1234
port = 1234

# Setup configuration
[setup]
# Install `opam` package
install = '''
apt-get install opam
'''

# Initialise opam so we can run ocaml
init = '''
opam init -y
eval $(opam env)
'''

# Language configuration
[languages]
# Enable python3 default
python3 = "*"
# Enable built-in Java 21
java = "21"
# Add custom `ocaml` language type
[languges.ocaml]
build = "ocamlc -o out {{SOURCEFILE}}"
run = "./out"


# Account configurations
[[accounts.admins]]
name = "Host"
password = "HostP@ssword1"

[[accounts.competitors]]
name = "Team1"
password = "Team1P@ssword"

[[accounts.competitors]]
name = "Team2"
password = "Team2P@ssword"


# packet configuration
[packet]
title = "Example Packet"
preamble = '''
This packet includes problems of a difficulty *vastly*
surpassing the capabilities of the average computer
science student. Be wary as these problems will
certainly give you great intellectual trouble. There
is little hope for anyone without a Ph.D in computer
science.

If you decide to attempt these problems anyways, good
luck. You will be rewarded for swiftness in your answers.
'''

# Add a problem to this packet that requires the competitor to reverse a
# string
[[packet.problems]]
title = "Reversing a string"
description = '''
Reversing a string is one of the most _basic_ algorithmic
problems for a beginner computer science student to solve.

Solve it.
'''

# Simple "hello" -> "olleh" test
# Since this is the first test that is visible, it will be shown as the
# example to the user.
[[packet.problems.tests]]
input = "hello"
output = "olleh"
visible = true

[[packet.problems.tests]]
input = "world"
output = "dlrow"
visible = true

# Test that is not visible, and thus will not show the input or expected
# output to the competitor.
# This test is still used for scoring the competitor's solution.
[[packet.problems.tests]]
input = ""
output = ""

[[packet.problems.tests]]
input = "aa"
output = "aa"

[[packet.problems.tests]]
input = "racecar"
output = "racecar"
```

## Imports

Because these configuration files can easily become out of hand, we
offer the ability to import sections of the file using `import`.

This example shows many sections broken into their own files.  Of
course, if only want to take certain sections out, you may.

```toml
# In config.toml

port = 1234 # Host competition on port 1234

setup = { import = "./setup.toml" }
languages = { import = "./languages.toml" }
accounts = { import = "./accounts.toml" }
packet = { import = "./packet.toml" }
```

```toml
# In setup.toml

# Install `opam` package
install = '''
apt-get install opam
'''

# Initialise opam so we can run ocaml
init = '''
opam init -y
eval $(opam env)
'''
```

```toml
# In languages.toml

python3 = "*" # Enable python3 default
java = "21"   # Enable built-in Java 21

[ocaml]       # Add custom `ocaml` language type
build = "ocamlc -o out {{SOURCEFILE}}"
run = "./out"
```

```toml
# In accounts.toml
[[admins]]
name = "Host"
password = "HostP@ssword1"

[[competitors]]
name = "Team1"
password = "Team1P@ssword"

[[competitors]]
name = "Team2"
password = "Team2P@ssword"
```

```toml
# In packet.toml
title = "Example Packet"
preamble = '''
This packet includes problems of a difficulty *vastly*
surpassing the capabilities of the average computer
science student. Be wary as these problems will
certainly give you great intellectual trouble. There
is little hope for anyone without a Ph.D in computer
science.

If you decide to attempt these problems anyways, good
luck. You will be rewarded for swiftness in your answers.
'''

problems = [{ import = "./problem1.toml" }]
```

```toml
# In problem1.toml
title = "Reversing a string"
description = '''
Reversing a string is one of the most _basic_ algorithmic
problems for a beginner computer science student to solve.

Solve it.
'''

# Simple "hello" -> "olleh" test
# Since this is the first test that is visible, it will be shown as the
# example to the user.
[[tests]]
input = "hello"
output = "olleh"
visible = true

[[tests]]
input = "world"
output = "dlrow"
visible = true

# Test that is not visible, and thus will not show the input or expected
# output to the competitor.
# This test is still used for scoring the competitor's solution.
[[tests]]
input = ""
output = ""

[[tests]]
input = "aa"
output = "aa"

[[tests]]
input = "racecar"
output = "racecar"
```
