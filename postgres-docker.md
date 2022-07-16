## Configuration steps

#### Creates a **docker volume** to persist data named as *postgres-data*
    $ docker volume create postgres-data

**Obs, docker volumes are held into */var/snap/docker/common/var-lib-docker/volumes* directory**

#### Creates a **docker image** named as *postgresql* from Postgresql-DBMS version 14

+ Sets POSTGRES_PASSWORD environment variable value
+ Maps the container port into host OS port
+ Mounts the containers directory /var/lib/postgresql/data into the docker volume created above

###

    $ docker run --name postgresql -d \
        -e "POSTGRES_PASSWORD=1234" \
        -p 5432:5432 \
        -v postgres-data:/var/lib/postgresql/data \
        postgres:14-alpine

#### Checks if the container is running
    $ docker container list

#### Runs psql command inside postgresql container
    $ docker exec -it \
        postgresql \
        psql -U postgres
