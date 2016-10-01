PostgreSQL 9
============
Hoon H.

Desribes how to use PostgreSQL 9 on macOS.

**Pitfall**: Remove "Server.app" before proceed. Because the Server.app
contains a PostgreSQL command, and it confuses procedures below.



Install. (vis Homebrew)

    brew install postgresql

Make a new empty database files.

    mkdir sample1
    cd sample1
    pg_ctl init -D .
    cd ..

Run server single time.

    cd sample1
    postgres -D .
    cd ..

Connect to the server which run with fresh new database.

    psql -d postgres

`-d` designate the name of database to connect to.
Newrly created PostgreSQL datafiles should have at least `postgres` database
which is a metadata database. You need to connect to this database at first,
and create another database for your needs.

Quit `psql`.

    \q

Or, press `Control+D`.

Help in `psql`.

    \?

Listing available databases.

    \l

Listing available tables, views and etc..

    \d


















