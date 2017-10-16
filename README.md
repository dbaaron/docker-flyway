# Docker Flyway
Docker container for running flyway migrations.

# How to use this image

## Configuration
This image requires a flyway configuration file that that needs to be mounted as a volume.
```console
$ docker run --rm --net --host --volume "/path/to/config/flyway.conf":"/flyway/conf/flyway.conf" meatspace/flyway info
```

### Sample Configuration
```shell
flyway.driver=org.hsqldb.jdbcDriver
flyway.url=jdbc:hsqldb:file:/db/flyway_sample
flyway.user=SA
flyway.password=mySecretPwd
flyway.schemas=schema1,schema2,schema3
flyway.table=schema_history
flyway.locations=classpath:com.mycomp.migration,database/migrations,filesystem:/sql-migrations
flyway.sqlMigrationPrefix=Migration-
flyway.repeatableSqlMigrationPrefix=RRR
flyway.sqlMigrationSeparator=__
flyway.sqlMigrationSuffix=-OK.sql
flyway.encoding=ISO-8859-1
flyway.placeholderReplacement=true
flyway.placeholders.aplaceholder=value
flyway.placeholders.otherplaceholder=value123
flyway.placeholderPrefix=#[
flyway.placeholderSuffix=]
flyway.resolvers=com.mycomp.project.CustomResolver,com.mycomp.project.AnotherResolver
flyway.skipDefaultCallResolvers=false
flyway.callbacks=com.mycomp.project.CustomCallback,com.mycomp.project.AnotherCallback
flyway.skipDefaultCallbacks=false
flyway.target=5.1
flyway.outOfOrder=false
flyway.validateOnMigrate=true
flyway.cleanOnValidationError=false
flyway.mixed=false
flyway.group=false
flyway.ignoreMissingMigrations=false
flyway.ignoreFutureMigrations=false
flyway.cleanDisabled=false
flyway.baselineOnMigrate=false
flyway.installedBy=my-user
```

## Migrations
This image supports the use of sql migrations only at this time.
```console
$ docker run --rm --net host --volume "/path/to/migration/sql":"/flyway/sql" meatspace/flyway info
```

## Execute Migration
Execute migration 
```console
$ docker run \
    --rm --net host \
    --volume "/path/to/migration/sql":"/flyway/sql" \
    --volume "/path/to/config/flyway.conf":"/flyway/conf/flyway.conf" \
    meatspace/flyway:test migrate
```