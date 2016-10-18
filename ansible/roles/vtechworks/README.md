# vtechworks

Installs dspace from VTUL's github repository

## Requirements

Needs `ant`, `maven`, `postgres`, `tomcat7` and our `webserver` roles to run.

## Role Variables

- `source_dir`: directory which holds cloned vtechworks repo
- `project_db_password`: database password for vtechworks application
- `project_db_user`: database user for vtechworks application
- `project_db_name`: database name for vtechworks application
- `version`: vtechworks branch to clone
- `repo_version`: vtechworks git branch to clone
- `apache_server_aliases`: apache alias
- `dspace_home`: dspace application home
- `ant_source_dir`: directory ant builds from
