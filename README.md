# Fedora 4/GraphDB Docker Repo

This is a fork of the Git repo of the Docker image for [Fedora 5 docker](https://hub.docker.com/r/yinlinchen/fcrepo4-docker/). It uses the latest Fedora 4.7.z release in order support development for (ActiveFedora)[https://github.com/samvera/active_fedora] (which, current is only tested against (Fedora 4.y releases)[https://github.com/samvera-labs/samvera-circleci-orb/blob/master/src/executors/ruby_fcrepo_solr.yml#L17]).  Please see the [Hub page](https://hub.docker.com/r/yinlinchen/fcrepo4-docker/) for the full readme on how to use the Docker image and for information regarding contributing and issues. It is also configured for synchronization with GraphDB.

## Requirements

* [Docker](https://www.docker.com/)

## Usage

### With GraphDB
By default Fedora is configured to synchronize with GraphDB with its resource 
index. The GraphDB installation is assumed to be hosted at URL ``http://localhost:7200/repositories/fcrepo/statements`. Please edit this in `config/org.fcrepo.camel.indexing.triplestore.cfg` in order to update this URL.

Run Fedora with a file-based objects database:
```
FEDORA_TAG=4.7.5 docker-compose up -d

# Shutdown server
docker-compose down
```

Run Fedora(e.g. 4.7.5) with a MySQL database:
```
# Start server
FEDORA_TAG=4.7.5 docker-compose -f fcrepo-mysql.yml up -d

# Shutdown server
docker-compose -f fcrepo-mysql.yml down
```

Run Fedora(e.g. 4.7.5) with a PostgreSQL database:
```
# Start server
FEDORA_TAG=4.7.5 docker-compose -f fcrepo-postgres.yml up -d

# Shutdown server
docker-compose -f fcrepo-postgres.yml down
```

Run Fedora(e.g. 4.7.5) with Camel Toolbox customizations:
```
# Start server
FEDORA_TAG=4.7.5 docker-compose -f fcrepo-camel.yml up -d

# Shutdown server
docker-compose -f fcrepo-camel.yml down
```
 * See [Camel](docker/services/fcrepo-camel) section for details.

# Rebuild the docker image and start the Fedora (e.g. 4.7.5) server
```
FEDORA_TAG=4.7.5 docker-compose up -d --force-recreate --build
```
Fedora [Dockerfile](docker/services/fcrepo/Dockerfile)

You can shell into the machine with `docker exec -i -t "CONTAINER ID" /bin/bash`

## In this Docker image, see detail in [Dockerfile](docker/services/fcrepo/Dockerfile)

  * [Tomcat 8.0.53](https://tomcat.apache.org) at [http://localhost:8080](http://localhost:8080)
    * Manager username = "fedora4", password = "fedora4"
  * [Fedora 4.7.5](https://wiki.duraspace.org/display/FF/Downloads) at [http://localhost:8080/fcrepo](http://localhost:8080/fcrepo)
    * username = "fedoraAdmin", password = "secret3"

  ps. MacOS: docker is configured to use the default machine with IP e.g. 192.168.99.100 or 127.0.0.1, the Fedora 4 URL is either [http://192.168.99.100:8080/fcrepo](http://192.168.99.100:8080/fcrepo) or [http://127.0.0.1/fcrepo](http://127.0.0.1/fcrepo). You can use "docker-machine ip" to see your docker machine IP.

## Maintainers

Current maintainers (for this fork):

* [James Griffin](https://github.com/jrgriffiniii)

Current maintainers (for the original project):
* [Yinlin Chen](https://github.com/yinlinchen)

