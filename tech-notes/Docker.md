Docker
======
Hoon H.

I am still not sure what's the best way to install Docker on macOS. For now, I just used Docker for macOS app.



Tips
----
- Docker has images and containers. Images are snapshot, and containers are running process.
- All the container configuration must be done at `docker run`. You cannot modify any after it once
  been executed.
- Docker container has no networking to host by default.
- But, you can map a port from a container to host.

For example, you can expose PostgreSQL server container to expose its port to host.



PostgreSQL 9 Container
----------------------
Install.

    docker pull postgres
    
Run naively.

    docker run postgres

Run cleverly.
- Nameless.
- Remove automatically after exit.
- Map port `5432` to host to allow host to connect to server.
- Setup `postgres` database user password.

    docker run -p 5432:5432 --rm -e POSTGRES_PASSWORD=your_password postgres
    
Connect to the server using `psql`.

    psql -h localhost -U postgres




    


