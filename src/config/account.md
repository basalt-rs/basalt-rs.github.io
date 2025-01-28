# Account Configuration

The two types of accounts, [admin](#admin-accounts) and
[competitor](#competitor-accounts) can be specified using the toml array
syntax.

Competitor accounts and admin accounts must not have the same names.

```toml
[[accounts.admins]]
name = "Host"
password = "HostP@ssword1"

[[accounts.competitors]]
name = "Team1"
password = "Team1P@ssword"

[[accounts.competitors]]
name = "Team2"
password = "Team2P@ssword"
```

## Admin Accounts

Admin accounts have access to the host view when using the basalt app
and can manage the competition at run time.

## Competitor Accounts

Competitor accounts have access to the competitor view when using the
basalt app and will test and submit their solutions.

## Imports

Account configuration may be imported from another toml file.

```toml
# In config.toml
accounts = { import = "./accounts.toml" }
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
