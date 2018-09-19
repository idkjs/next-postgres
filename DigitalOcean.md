Access the droplet docker environment we run, `eval $(docker-machine env mytestdb)`

Access the container on d-ocean server. We will create a database inside our PostgreSQL container.
Run `docker exec -it my-postgres bash`. This gets us inside of the pg container.

Then run `psql -U postgres` to get into psql

```s
root@04d6e500ec59:/# psql -U postgres
psql (10.5 (Debian 10.5-1.pgdg90+1))
Type "help" for help.

postgres=#
```

Then create a user: test with password: test:

```s
postgres=# CREATE ROLE test WITH LOGIN PASSWORD 'test';
CREATE ROLE
postgres=#

# Allow yourself to create databases
ALTER ROLE test CREATEDB;

# Exit Postgres console
\q

# Log in as your new user.
psql postgres -U test

# root@04d6e500ec59:/# psql postgres -U test
# psql (10.5 (Debian 10.5-1.pgdg90+1))
# Type "help" for help.

# postgres=>

# Create a database named: nextdb.
# If you change this, update config.js
CREATE DATABASE nextdb;

# Give your self privileges
GRANT ALL PRIVILEGES ON DATABASE nextdb TO test;

# List all of your databases
\list

# Connect to your newly created DB as a test
\connect nextdb

# Exit Postgres console
\q
```
