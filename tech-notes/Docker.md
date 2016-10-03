Docker
======
Hoon H.

I am still not sure what's the best way to install Docker on macOS. For now, I just used Docker for macOS app.



Basics
----
- Docker has images and containers. Images are snapshot, and containers are running process.
- All the container configuration must be done at `docker run`. You cannot modify any after it once
  been executed.

Networking
----------
- Docker containers have no networking to host by default.
- Docker containers have their own segregated internal network. They are all connected to each other by default.
  
You may have toruble to find out IP addresses of each docker containers. Use this.

    docker inspect <container-name>
    
To inspect IP address of the container. And even more.






PostgreSQL 9 Container
----------------------
Install.

    docker pull postgres
    
Run naively.

    docker run postgres

Run cleverly.

- Nameless.
- `--rm`: Remove automatically after exit.
- `-p 5432:5432`: Map port `5432` to host to allow host to connect to server.
- `-e POSTGRES_PASSWORD=your_password`: Setup `postgres` database user password.
- `-v \`pwd\`:/var/lib/postgresql/data`: Mount current directory as server's data storage.

Here's the command.

    docker run -p 5432:5432 --rm -v `pwd`:/var/lib/postgresql/data: -e POSTGRES_PASSWORD=your_password postgres
    
Connect to the server using `psql`.

    psql -h localhost -U postgres




    


