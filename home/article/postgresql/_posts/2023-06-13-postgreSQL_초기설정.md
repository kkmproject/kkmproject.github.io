---
layout: article
---

# {{ page.title }}

```
$ brew search postgresql
$ brew install postgresql@15
$ brew search libpq
$ echo 'export PATH="/opt/homebrew/opt/postgresql@15/bin:$PATH"' >> ~/.zshrc
$ source ~/.zshrc
$ postgres --version
$ brew services start postgresql@15
$ brew services list
$ brew services info postgresql@15
$ psql postgres

postgres=# CREATE ROLE ADMIN WITH LOGIN PASSWORD 'ADMIN';
postgres=# SELECT ROLENAME FROM PG_ROLES;
postgres=# ALTER ROLE ADMIN SUPERUSER;
postgres=# \du
postgres=# psql postgres -U admin
postgres=# CREATE DATABASE kkmproject;
postgres=# \list
postgres=# GRANT ALL PRIVILEGES ON DATABASE kkmproject TO admin;
postgres=# \connect kkmproject
postgres=# CREATE SCHEMA blog;
postgres=# \dn
postgres=# exit

...

$ brew services stop postgresql@15
```