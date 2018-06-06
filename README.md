# SCDF Recipe JDBC

## What Is SCDF?

Spring Cloud Data Flow (SCDF) is a framework for creating, deploying and operating scalable data pipelines onto modern runtimes such as Cloud Foundry, Kubernetes, Apache Mesos or Apache YARN.

To learn more about SCDF, please refer to the following Blog:

http://lukeshannon.com/blog/2018/scdf-setup.html

The following is a recipes for an data oriented outcome we can achieve once SCDF is set up. As usual the work will be done on Pivotal Web Services (PWS) (https://run.pivotal.io/).

## JDBC Recipe

### Outcome

We have a stream of data, we want to write this data into a DB.

### Source Of Data

We will use an application that produces JSON and posts it to a HTTP endpoint (which is the start of the pipeline). Streams can be over whelming so we will explore filtering to ensure only what we want go to the DB.

### Running The Producer

### Creating the DB on PWS

### Creating the Stream

### Running the Stream
