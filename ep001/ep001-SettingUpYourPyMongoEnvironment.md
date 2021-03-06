# Setting Up Your PyMongo Environment
Welcome to Quick Start:Python. This is the first in a series of regular blog 
posts that will introduce developers to programming MongoDB using the 
Python programming language. 

First thing we need to do is head over to the 
[the registration page](https://www.mongodb.com/cloud/atlas/register) for
MongoDB Atlas. There you can setup your free-tier and get started with 
MongoDB with the need for payment or credit card validation. Once you have
registered and set up your free-tier you are ready to get started with the rest
of this tutorial. 




Now that we have a server running we can confirm that it works by connecting via the 
[mongo shell](https://docs.mongodb.com/manual/mongo/).

<pre>
$ <b>mongo</b>
MongoDB shell version v4.0.0
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 4.0.0
Server has startup warnings:
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten]
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] ** WARNING: You are running this process as the root user, which is not recommended.
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten]
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] ** WARNING: This server is bound to localhost.
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] **          Remote systems will be unable to connect to this server.
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] **          Start the server with --bind_ip &lt address&gt to specify which IP
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] **          addresses it should serve responses from, or with --bind_ip_all to
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] **          bind to all interfaces. If this behavior is desired, start the
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten] **          server with --bind_ip 127.0.0.1 to disable this warning.
2018-07-06T10:56:50.973+0100 I CONTROL  [initandlisten]

---
Enable MongoDB's free cloud-based monitoring service to collect and display
metrics about your deployment (disk utilization, CPU, operation statistics,
etc).

The monitoring data will be available on a MongoDB website with a unique
URL created for you. Anyone you share the URL with will also be able to
view this page. MongoDB may use this information to make product
improvements and to suggest MongoDB products and deployment options to you.

To enable free monitoring, run the following command:
db.enableFreeMonitoring()
---

>
</pre>

These warnings are standard. They flag that this database has no access controls setup by default and, 
that it is only listening to connections coming from the machine it is running on (*localhost*). 
We will learn how to setup access control and listen on a broader range of ports in later episodes.

## Installing the PyMongo Driver

But this series is not about the MongoDB Shell, which uses JavaScript as its coin of the realm, 
it’s about Python. How do we connect to the database with Python?

First we need to install the MongoDB Python Driver, [PyMongo](https://docs.mongodb.com/ecosystem/drivers/). 
In MongoDB parlance a driver is a language-specific client library that allows developers to 
interact with the server in the idiom of their own programming language.

For Python that means installing the driver with `pip`. In node.js the driver is 
installed using `npm` and in Java you can use `maven`.

<pre>
$ <b>pip3 install pymongo</b>
Collecting pymongo
  Downloading https://files.pythonhosted.org/packages/a1/e0/51df08036e04c1ddc985a2dceb008f2f21fc1d6de711bb6cee85785c1d78/pymongo-3.7.1-cp27-cp27m-macosx_10_13_intel.whl (333kB)
    100% |████████████████████████████████| 337kB 4.1MB/s
Installing collected packages: pymongo
Successfully installed pymongo-3.7.1
$
</pre>

We recommend you use a [virtual environment](https://docs.python.org/3/library/venv.html) to isolate your 
PyMongo Monday code. This is not required but is very convenient for isolating different development streams.

Now we can connect to the database:

<pre>
$ <b>python</b>
Python 3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 03:03:55)
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> <b>import pymongo</b>                                                  <i>(1)</i>
>>> <b>client = pymongo.MongoClient(host="mongodb://localhost:8000")</b>   <i>(2)</i>
>>> <b>result = client.admin.command("isMaster")</b>                       <i>(3)</i>
>>> <b>import pprint</b>
>>> <b>pprint.pprint(result)</b>
{'ismaster': True,
 'localTime': datetime.datetime(2018, 6, 13, 21, 55, 2, 272000),
 'logicalSessionTimeoutMinutes': 30,
 'maxBsonObjectSize': 16777216,
 'maxMessageSizeBytes': 48000000,
 'maxWireVersion': 6,
 'maxWriteBatchSize': 100000,
 'minWireVersion': 0,
 'ok': 1.0,
 'readOnly': False}
>>>
</pre>

First we import the PyMongo library *(1)*. Then we create a local `client` object *(2)* that holds the connection 
pool and other status for this server. We generally don’t want more than one `MongoClient` object 
per program as it provides its own connection pool. 

Now we are ready to issue a command to the server. 
In this case it's the standard MongoDB server information command which is called rather 
anachronistically `isMaster` *(3)*. This is a hangover from the very early versions of MongoDB. 
It appears in pre 1.0 versions of MongoDB  (which is over ten years old at this stage). 
The `isMaster` command returns a `dict` which details a bunch of server information. In order to 
format this in a more readable way we import the `pprint` library.

# Conclusion
That’s the end of episode one. We have installed MongoDB, installed the Python client library (aka driver),
started a `mongod` server and established a connection between the client and server.

Next week we will introduce CRUD operations on MongoDB, starting with **Create**.

For direct feedback please pose your questions on [twitter/jdrumgoole](https://twitter.com/jdrumgoole). 
That way everyone can see the answers. 

The best way to try out MongoDB is via [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
 our fully managed Database as a Service available on AWS, Google Cloud Platform (CGP) and Azure. 
 
 
