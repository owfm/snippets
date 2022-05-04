This is a base setup script for new PG databases for the _least priviledge_ model.

[Link to related AWS blog post](https://aws.amazon.com/blogs/database/managing-postgresql-users-and-roles/)

```SQL
REVOKE CREATE ON SCHEMA public FROM PUBLIC;
REVOKE ALL ON DATABASE "database_name" FROM PUBLIC;
CREATE ROLE readwrite;
GRANT CONNECT ON DATABASE "database_name" TO readwrite;
GRANT USAGE, CREATE ON SCHEMA public TO readwrite;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO readwrite;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT USAGE ON SEQUENCES TO readwrite;
CREATE USER read_write_app_user WITH PASSWORD 'xxx';
ALTER USER read_write_app_user VALID UNTIL 'infinity';
GRANT readwrite to read_write_app_user;
```
