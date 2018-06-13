# SCDF Recipe JDBC

## What Is SCDF?

Spring Cloud Data Flow (SCDF) is a framework for creating, deploying and operating scalable data pipelines onto modern runtimes such as Cloud Foundry, Kubernetes, Apache Mesos or Apache YARN.

To learn more about SCDF, please refer to the following Blog:

http://lukeshannon.com/blog/2018/scdf-setup.html

The following is a recipes for an data oriented outcome we can achieve once SCDF is set up. As usual the work will be done on Pivotal Web Services (PWS) (https://run.pivotal.io/).

## JDBC Writer Recipe

### Outcome

We have a stream of data, we want to write this data into a DB. The stream is continuous and not all the records are interesting to us, so we only want certain ones writen to the DB.

### Source Of Data

We will use an application that produces JSON and posts it to a HTTP endpoint (which is the start of the pipeline). Streams can be over whelming so we will explore filtering to ensure only what we want go to the DB.

### Running The Producer

The HTTP Producer app can be found here:

It's a simple application that produces JSON with the target to the POST the message as a command line arguement.

### Creating the DB on PWS

Using the CF command line (connected and authenticated to PWS), run the following commands:

```shell

cf create-service elephantsql turtle message-db

```
This will create out target DB. We can get a link to the Admin dashboard by running the service command.

```shell

cf service message-db

```

### Creating the Stream

```shell
stream create --name s1 --definition "http |  jdbc --driver-class-name=org.postgresql.Driver --username=txcqdjrm --password=yugppwbVy77PmULgidTqC0lfc0qpwDVK  --url=jdbc:postgresql://pellefant.db.elephantsql.com:5432/txcqdjrm --jdbc.initialize=true --spring.datasource.maxActive=2 --spring.datasource.tomcat.max-active=2" --deploy

```

### Testing the Stream

```shell

curl 'https://cndescdf-dataflow-server-rhlqe0u-s1-http.cfapps.io/' -i -X POST -H 'Content-Type: application/json;charset=UTF-8' -H 'Accept: application/json' -d '{"greeting" : "hello world" }'

```

### Filtering The Data


