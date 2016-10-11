# PostgreSQL

Installs PostgreSQL from the official repository and configures it

## Requirements

`apt` must be installed and the `buildenv` role.

## Role variables

Depends on `site_secrets.yml`

- `database_user`: postgres
- `database_group`: postgres
- `database_password`: postgres
