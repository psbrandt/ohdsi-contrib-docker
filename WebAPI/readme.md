![OHDSI](https://www.ohdsi.org/wp-content/uploads/2015/02/h243-ohdsi-logo-with-text.png)

# WebAPI Dockerfiles

The [OHDSI WebAPI](https://github.com/OHDSI/WebAPI) contains all OHDSI services
that can be called from OHDSI applications.

## Quickstart

Use the following command to spin up the WebAPI. Make sure to change the values
of the environment variables as needed.

```
docker run \
  --name ohdsi-webapi \
  -p 8080:8080 \
  -e "DBHOST=docker.for.mac.host.internal" \
  -e "DBNAME=cdm" \
  -e "DBUSER=postgres" \
  -e "DBPASS=s3cret" \
  -e "DBADMINUSER=postgres" \
  -e "DBADMINPASS=s3cret" \
  -e "DBCDMSCHEMA=public" \
  -e "DBWEBAPISCHEMA=webapi" \
  uwcarg/ohdsi-webapi:2.3.0-postgres
```

:bulb: `docker.for.mac.host.internal` is a magic constant in Docker for macOS
that points to the IP address of the host machine.

### Test

Navigate to the following URLS to test:
* http://localhost:8080/WebAPI/source/sources
* http://localhost:8080/WebAPI/vocabulary/search/cardiomyopathy

## Details

The Docker image is built on [Docker
Hub](https://hub.docker.com/r/uwcarg/ohdsi-webapi/) and contains a build of the
[OHDSI WebAPI](https://github.com/OHDSI/WebAPI). It also installs a default
source that points to the CDM instance specified in the environment variables.
See [`settings.xml`] and [the Flyway
migration](V1.0.5.0.1__Install_default_source.sql) to see exactly how the
variables are used.

### Environment Variables

When creating the container, the configuration given
[here](http://www.ohdsi.org/web/wiki/doku.php?id=documentation:software:webapi:webapi_installation_guide)
is updated to contain the values specified in the following environment
variables. A default source is also configured that points to the CDM instance
specified.

> DBHOST [default: localhost]

The is the hostname of the server running Postgres. If you are running Postgres
on the Docker host machine, you will need the host machine's IP address or
hostname on the Docker network. On macOS this is `docker.for.mac.host.internal`
(see
[here](https://docs.docker.com/docker-for-mac/networking/#use-cases-and-workarounds)).

> **DBPORT** [default: 5432]

The port Postgres is listening on.

> **DBNAME** [default: OHDSI]

The name of the database containing the OMOP CDM schema.

> **DBUSER** [default: ohdsi_app_user]

A database user with read access to the CDM schema.

> **DBPASS** [default: app1]

Password for the above user.

> **DBCDMSCHEMA** [default: ohdsi]

The name of the OMOP CDM schema.

> **DBWEBAPISCHEMA** [default: webapi]

The name of the schema that the WebAPI tables will be created in. This should
be different from the CDM schema.

> **DBADMINUSER** [default: ohdsi_admin_user]

A database admin user.

> **DBADMINPASS** [default: !PASSWORD!]

Password for the database admin user.

> **WEBAPIHOST** [default: localhost]

The hostname where the WebAPI will be accessible.

> **WEBAPIPORT** [default: 8080]

The post the WebAPI will be using.

## License

[![CC BY-SA](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/)
