# ClamAV Role

Installs ClamAV

## Requirements

The target system should have apt and the buildenv role

## Role variables

Role variables are listed below

- `clamav_private_mirror_enabled`: enables a private mirror (true/false)
- `clamav_private_mirror_host`: FQDN of your private mirror

## Dependencies

The buildenv role
