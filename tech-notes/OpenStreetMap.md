OpenStreetMap
=============

Describes how to use OSM tools.



`osmosis`
---------

- This is basically Java app.
- I don't want to have Java installed on my local machine. Because it spams.
- Let's go VM.

So I setup a Docker container based on Ubuntu 16.
Installed these packages.

- `curl`
- basic development tools
- `postgresql-client`
- `default-jdk`
- `git`

When you install this thing, make sure that you are running everything with non-root user.
Prepare a Docker container and log into there.

    docker run -it --rm <image-name>

Clone Osmosis, and checkout stable releaes.

    git clone https://github.com/openstreetmap/osmosis
    cd osmosis
    git checkout 0.45
    
Build.

    ./gradlew assemble
    
Move into the package.

    cd package
    
    
    
    
Initializing Database Schema
-------------------
First, you must make a new database with PostGID and HStore support.
Just make a new database and execute these SQL commands.

    CREATE EXTENSION postgis;
    CREATE EXTENSION hstore;

First, you must initialize database schema. Osmosis does not do this for you.
There's an SQL script for you. Do something like this. Command may different
by your PostgreSQL server configuration.

    cd script
    psql -d <your-db-name> -f osmosis_dir/script/pgsnapshot_schema_0.6.sql
    cd ..

[Reference](http://wiki.openstreetmap.org/wiki/Osmosis/PostGIS_Setup#Create_and_Initialise_Database)
    
    
    
    

Processing Data
---------------
Now we can use the importer. Move to directory that contains osmosis binary.

    cd bin

Prepare some `.pbf` files to import.

    curl -O http://download.bbbike.org/osm/bbbike/Seoul/Seoul.osm.pbf
    ./osmosis --read-pbf file=Seoul.osm.pbf --write-pgsql host="<your-db-server-addr>" database="<your-db-name>" user="<your-user-name>"
    
Notice that it uses `--write-pgsql` writer. It's not `--write-apidb`.



