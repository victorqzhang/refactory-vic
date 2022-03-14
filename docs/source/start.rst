Getting Started
================

Before You Start
-----------------

If you haven't already, please start a terminal and clone the repository:

::
    git clone https://github.com/Accenture/mercury.git
    cd mercury

To get the system up and running, you should compile and build the foundation libraries from sources. This will install the libraries into your ".m2/repository/org/platformlambda" folder.

``Important`` \- please close all Java applications and web servers in your PC if any. The build process will invoke unit tests that simulate HTTP and websocket servers.

::
    # start a terminal and go to the mercury sandbox folder
    mvn clean install

The platform-core, rest-spring, hazelcast-connector and kafka-connector are libraries and you can rebuild each one individually using ``mvn clean install``

The rest of the subprojects are executables that you can rebuild each one with ``mvn clean package``.

Getting Started
----------------
You can compile the rest-example as a microservices executable like this:

::
    cd mercury/examples
    cd rest-example
    mvn clean package
    java -jar target/rest-example-2.3.2.jar
    # this will run the rest-example without a cloud connector

Try http://127.0.0.1:8083/api/hello/world with a browser.

It will respond with some sample output like this:

::
 {
  "body" : {
    "body" : {
      "accept" : "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8",
      "accept-encoding" : "gzip, deflate, br",
      "accept-language" : "en-US,en;q=0.9",
      "cache-control" : "max-age=0",
      "connection" : "keep-alive",
      "host" : "127.0.0.1:8083",
      "time" : "2018-12-21T16:39:33.546Z",
      "upgrade-insecure-requests" : "1",
      "user-agent" : "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) ..."
    },
    "headers" : {
      "seq" : "4"
    },
    "instance" : 4,
    "origin" : "2018122170c4d0e80ef94b459763636da74d6b5f"
  },
  "execution_time" : 0.298,
  "headers" : { },
  "round_trip" : 0.862,
  "status" : 200
}

The REST endpoint makes a request to the "hello.world" service that echoes back the headers of the HTTP request. The underlying Spring Boot HTTP server has been pre-configured with HTML, JSON and XML message serializers and exception handlers.

If you change the "accept" header to "application/xml", the output will be shown in XML.

To demonstrate concurrent processing, you may visit http://127.0.0.1:8083/api/hello/concurrent

Now try http://127.0.0.1:8083/api/hello/pojo/1

This will return a HTTP-500 "Route hello.pojo not found" error. This is expected behavior because the "hello.pojo" service is not available in the rest-example container. Let's walk thru distributed and scalable application in the next section.