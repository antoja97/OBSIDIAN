
# Chapter 1

Four characteristics about Spark's design:
- Speed
- Ease of use
- Modularity
- Extensibility


### Apache Spark's Distributed Execution

*Spark Driver*: Responsible for instantiating a SparkSession, communicates with the cluster manager and it taransforms all the Spark operations into DAG computations.

*SparkSession*: Became a unified conduit to all Spark operations and data.
Provides a single unified entry point to all of Spark's functionality.

*Cluster manager*: Responsible for managing and allocating resources for the cluster of nodes on wich your Spark app runs. Currently, Spark supporst 4 cluster managers: Hadoop, YARN, Mesos and Kubernetes.

*Spark executor*: Runs on each worker node in the cluster and he communicates with the driver program and are responsible for executing tasks on the workers.

*Deployment modes*: Its support for myriad deployment modes, enabling Spark to run in different configurations and environments. and it could be possible in different environments such as Hadoop, Yarn or Kubernetes.


# Chapter 2


## Concepts

*Application*: A user program built on Spark using its APIs. It consists of a driver program and executors on the cluster.

*SparkSession*: Objet that provides a point of entry to interact with underlying Spark functionality and allows programming Spark with its APIs.

*Job*: A parallel computation consisting of multiple tasks that gets spawned in response to a Spark action (e.g., save(), collect())

*Stage*: Each job gets divided into smaller sets of tasks called stages that depend on each other.

*Task*: A single unit of work or execution that will be sent to a Spark executor.

*Transformations, Actions and Lazy evaluation*:  Transformations are evaluated lazily.
Let's see the differences between both.

![[Pasted image 20230721164339.png]]

*Narrow and Wide Transformations*: Narrow is any transformation where a single output partition can be computed from a single input partition (e.g., filter() and contains() they don't produce any exchange of data).
Wide is where data from other aprtitions is read in, combined, and written on disk (e.g. groupBy() and orderBy()).


# Chapter 3

The RDD is the most basic abstraction in Spark, where there are three vital characteristics such as:
- Dependencies: Intructs Spark how an RDD is constructed with its inputs is required.
- Partitions (with some locality information): Provides Spark the ability to split the work to paralleliza computation on partitions across executors. In some cases-fro example, reading from HDFS-Spark.
- Compute function: Partition => Iterator[T] where data will be stored in the RDD.

##### Basic Data Types

![[Pasted image 20230721172015.png]]

##### Complex Data Types

![[Pasted image 20230721172046.png]]


***Defining a Schema***

![[Pasted image 20230721172134.png]]


##### Columns and Expressions

![[Pasted image 20230721172248.png]]
![[Pasted image 20230721172316.png]]


##### Rows

A row in Spark is a generic Row object, containing one or more columns, because is an object in Spark and an ordered collection of fields.

![[Pasted image 20230721172504.png]]

***Saving DataFrame as a Parquet file or SQL table***

![[Pasted image 20230721173253.png]]

***Projections and filters***

![[Pasted image 20230721173331.png]]
![[Pasted image 20230721173423.png]]

***Renaming, adding, and dropping columns***

![[Pasted image 20230721173445.png]]
![[Pasted image 20230721173517.png]]
![[Pasted image 20230721173544.png]]
![[Pasted image 20230721173613.png]]

***Other common DataFrame operations***

*F*

![[Pasted image 20230721173702.png]]


## DataFrames vs Datasets

- If u want to tell Spark what to do, not how to do it, use both
- If u want rich semantics, high-level abstractions, and DSL operatos, use both
- If u want strict compile-time type safete, use Dataset
- Processing demands high-level expressions filters,map, agg... use both
- If u want SQL queries, use DataFrames
- Serialization with Encoders, use Datasets
- Unification, optimization and simplification, use DataFrames.
- If u re an R user, use DataFrame
- If u re an Python user, use DataFrame and drop down to RDDs if you need more control
- If u want space and speed efficiency, use DataFrames

### Catalyst Optimizer

It goes through four transformational phases:
- Analysis
- Logical optimization
- Physical planning
- Code generation

![[Pasted image 20230721174341.png]]

# Chapter 4

Spark SQL provides the engine upon which the high-level Structured APIs.
Can red and wirte data in a variety of structured formats (JSON, Hive, Parquet, Avro, ORC, CSV)

![[Pasted image 20230723123035.png]]

#### Managed vs Unmanaged Tables

For a managed table, Spark manages  both of metadata and the data in the file store. This could be a local filesystem, HDFS, or an object store such as Amazon S3 or Azure Blob.

An unmanaged table, Spark only manages the metada, while you manage the data yourself in an external data source such as Cassandra.

![[Pasted image 20230723123933.png]]
![[Pasted image 20230723123958.png]]

#### Views

Views can be global (visible across all SparkSessions on a given cluster) or session-scoped (visible only to a single SparkSession).

![[Pasted image 20230723124217.png]]
![[Pasted image 20230723124252.png]]

##### Temporary views vs Global Temporary views

Temporary View: A temporary view is local to the current session and is accessible only within that session. It is dropped automatically at the end of the session or when the user explicitly drops it.

Global Temporary View: A global temporary view is accessible across multiple sessions but is local to the current database. It is dropped automatically at the end of the session that created it, or when all sessions referencing it are closed or when the user explicitly drops it.

![[Pasted image 20230723124733.png]]

#### DataFrameReader

![[Pasted image 20230723124910.png]]

*IMPORTANTE*
![[Pasted image 20230723124952.png]]


![[Pasted image 20230723125432.png]]
![[Pasted image 20230723125451.png]]

***IMAGES***

![[Pasted image 20230723125606.png]]


##### Binary Files

![[Pasted image 20230723130149.png]]


# Chapter 5


## Spark SQL and Apache Hive

The current Spark SQL engine no longer uses the Hive code in its implementation.
Shark was originally built on the Hive codebase on Hadoop systems.
It demonstrated that it was possible to have the best of both worlds; as fast as an enterprise data warehouse, and scaling as well as Hive/MapReduce.


##### User-Defined Functions 

The benefit of creating your own PySpark or Scala UDFs is that you  (and others) will be able to make use of them within Spark SQL itself.

Example:

![[Pasted image 20230723194807.png]]
![[Pasted image 20230723210127.png]]


***Pandas UDFs***

Pandas UDF (User-Defined Function) is a feature in Apache Spark that enables applying custom functions, written with the Pandas library, to distributed data in a cluster. This improves performance and usability when working with large datasets in Spark by leveraging the power and flexibility of Pandas for row-level processing.

![[Pasted image 20230723210304.png]]


## Querying with the Spark SQL Shell, Beeline, and Tableau.

![[Pasted image 20230723210535.png]]

![[Pasted image 20230723210711.png]]

***Iniciar: beeline -u jdbc:hive2://nombre_del_host:10000***


![[Pasted image 20230723210903.png]]
![[Pasted image 20230723210913.png]]
![[Pasted image 20230723210924.png]]
![[Pasted image 20230723210936.png]]
![[Pasted image 20230723210946.png]]


For more information on using Tableau to connect to a Spark SQL database, refer to Tableau’s Spark SQL documentation and the Databricks Tableau documentation
[Connect to Tableau | Databricks on AWS](https://docs.databricks.com/partners/bi/tableau.html)
[Spark SQL - Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_sparksql.htm)

![[Pasted image 20230723211133.png]]
![[Pasted image 20230723211144.png]]


***JDBC AND SQL DATABASES***

JDBC stands for Java Database Connectivity, and it is a Java API (Application Programming Interface) that provides a set of classes and interfaces to allow Java applications to connect to and access a database. This API enables Java applications to send queries and update data in the database using the Structured Query Language (SQL).

By using JDBC, developers can write Java code to establish connections with databases, send queries, retrieve results, and manage transactions efficiently and securely. It is an essential part of most Java applications that require access to data stored in databases.

![[Pasted image 20230723211422.png]]
![[Pasted image 20230723211436.png]]
![[Pasted image 20230723211502.png]]

***PostgreSQL***

![[Pasted image 20230723211735.png]]
![[Pasted image 20230723211747.png]]

***MySQL***

![[Pasted image 20230723211828.png]]
![[Pasted image 20230723211839.png]]


***Azure Cosmos DB***

![[Pasted image 20230723212533.png]]
![[Pasted image 20230723212557.png]]


***MS SQL Server***

![[Pasted image 20230723212650.png]]


***Other External Sources***

[datastax/spark-cassandra-connector: DataStax Spark Cassandra Connector (github.com)](https://github.com/datastax/spark-cassandra-connector)
[Snowflake Connector for Spark | Snowflake Documentation](https://docs.snowflake.com/en/user-guide/spark-connector)
[MongoDB Connector for Spark — MongoDB Spark Connector](https://www.mongodb.com/docs/spark-connector/upcoming/)


### High-Order Functions in DataFrames and Spark SQL

Exploding the nested structure into individual rows, applying some function, and then re-creating the nested structure.

EXPLODE: In the provided SQL code, the EXPLODE function is used to transform an array or an array-type column into multiple rows. The main purpose of EXPLODE is to "explode" or unfold the elements of an array into separate rows, making it easier to process and analyze data in relational tables.

![[Pasted image 20230723213229.png]]
![[Pasted image 20230723213253.png]]
![[Pasted image 20230723213305.png]]

![[Pasted image 20230723213342.png]]
![[Pasted image 20230723213402.png]]
![[Pasted image 20230723213413.png]]
![[Pasted image 20230723213431.png]]

***Unions***

![[Pasted image 20230724095304.png]]

***Joins***

![[Pasted image 20230724095454.png]]

***Windowing***

![[Pasted image 20230724095606.png]]
![[Pasted image 20230724095638.png]]

***Modifications in columns***

![[Pasted image 20230724095729.png]]
![[Pasted image 20230724095738.png]]
![[Pasted image 20230724095801.png]]
![[Pasted image 20230724095857.png]]
![[Pasted image 20230724095956.png]]

# Chapter 6

***Scala Case Classes and JavaBeans for Datasets***

In order to create Dataset[T], where T is your typed object in Scala, you need a case class that defines the object. Let's see the next example where we create a class and process a data.

Json file has the following format:
![[Pasted image 20230724132523.png]]

![[Pasted image 20230724132648.png]]

![[Pasted image 20230724132931.png]]

###### Creating sample data

![[Pasted image 20230724133024.png]]

***Transformations***

Some examples of transformations could be map, reduce, filter, select and aggregate.
Scala is functional programming language and more recently lambdas, functional arguments, and closures have been added to Java too.

![[Pasted image 20230724133232.png]]
![[Pasted image 20230724133252.png]]
![[Pasted image 20230724133310.png]]

***Converting DataFrames to Datasets***

For strong type cecking of queries and constructs, we can convert DF to DS.

![[Pasted image 20230724133434.png]]

![[Pasted image 20230724133534.png]]

***Strategie to Mitigate Costs***

In short, serialization converts data or an object into a sequence of bytes for storage or transmission, while deserialization takes the byte sequence and converts it back into data or an object in memory for use in the application. These processes are essential for sharing data between different systems or for efficiently storing and retrieving data in persistent media.

![[Pasted image 20230724133927.png]]
![[Pasted image 20230724134003.png]]


# Chapter 7


We want to consider how to optimize and tune Spark and in this chapter, we will discuss a set of Spark configuration that enable optimizations.


## Optimizing and Tuning Spark for Efficiency

#### Viewing and Setting Apache Spark configurations

There are three ways:
- The first one is a set of configuration files, where we have $SPARK_HOME directory. There are several config files, what we can change default values and shaving them without .template suffix instructs Spark to use these new values.

- The second way is to specify Spark configuration directly in our Spark app or on the command line when submitting the app with spark-submit, using the --conf flag:

![[Pasted image 20230724134900.png]]

Now is how we would do this in the Spark app:

![[Pasted image 20230724135551.png]]


- The third way is through a programmatic interface via the Spark shell, as with everything else in Spark, APIs are the primary method of interaction.

![[Pasted image 20230724140100.png]]
![[Pasted image 20230724140111.png]]
![[Pasted image 20230724140144.png]]

[Hive Bucketing in Apache Spark - Tejas Patil - YouTube](https://www.youtube.com/watch?v=6BD-Vv-ViBw&=645s)
[Tuning Apache Spark for Large Scale Workloads - Sital Kedia & Gaoxiang Liu - YouTube](https://www.youtube.com/watch?v=5dga0UT4RI8)


##### Configuring Spark Executor's memory and the shuffle service

![[Pasted image 20230724140628.png]]

*IMPORTANT*

![[Pasted image 20230724140719.png]]


***How partitions are created***

Spark's task process data as partitions read from disk into memory. Data on disk is laid out in chunks or contiguous file blocks, depending on the store. By default, file blocks on data stores range in size from 64 mb to 128 mb.

The size of a partition in Spark is dictated by spark.sql.files.maxPartitionBytes, where default size is 128 mb. We can decrease the size, but that may result in whats known as the "small file problem" - many small partition files, introducing an inordinate amount of disk I/0 and performance degradation thanks to filesystem operations such as opnening, closing, and listing diretories, which on da distributed filesystem can be slow.

![[Pasted image 20230724161342.png]]

[Tuning Apache Spark for Large Scale Workloads - Sital Kedia & Gaoxiang Liu - YouTube](https://www.youtube.com/watch?v=5dga0UT4RI8)

https://oreil.ly/RmiTd


### Caching and Persistance of Data

We can find two API calls, cache() and persist(). The latter provides more control over how and where your data is stored-in memory and on disk, serialized and unserialized.

In short and concise terms:

- `cache()`: It is a transient in-memory transformation that lazily stores the DataFrame or Dataset in memory. If the DataFrame or Dataset is used in multiple operations, it is re-evaluated each time it is needed. It is suitable for temporary data or when the DataFrame or Dataset will be used multiple times in the workflow.

- `persist()`: It is a persistent in-memory transformation that stores the DataFrame or Dataset in memory or on disk, depending on the specified storage level. Persistence is more durable and prevents re-evaluation of the DataFrame or Dataset each time it is used in subsequent operations. It is useful when you need to keep the DataFrame or Dataset in memory across multiple operations or want to avoid costly re-evaluation of the data.

##### DataFrame.chache()

It will store as many  of the aprtitions read in memory across Spark executors as memory allows.
While a DF may be fractionally cached, partitions cannot be fractionally cached.
(e.g. We have 8 partitions but onlye 4.5 partitions can fit in memory, only 4 will be cached)

![[Pasted image 20230724162508.png]]

Example Cache distributed across 12 partitions in executor memory

![[Pasted image 20230724162543.png]]


###### DataFrame.persist()

persist(StorageLevel.LEVEL) is nuance, providing control over how your data is cached vida StorageLevel.
Data on disk is always serialized using either Java or Kryo serialization.

![[Pasted image 20230724162820.png]]

![[Pasted image 20230724163052.png]]

We can cache the tables or views derived from DF.
Example:
![[Pasted image 20230724163236.png]]


***When to Cache and Persist***

Scenarios where we would want to access a larga dataset repteadly for queries or transformations.
- DF commonly used during iterative ML training
- DF accessed commonly for doing frequent transformations during ETL or building data pipelines

***When Not to Cache and Persist***

Some scenarios that may not warrant caching your DF include:
- DF are too big to fit in memory
- An inexpensive transformation on a DF not requiring frequent use, regardless of size

## Family of Spark Joins


Spark has five distinct join strategies by which it exchanges, moves, sorts, groups, and merges data across executors:

### Broadcast Hash Join

Also known as *map-side-only-join*, the broadcast hash join employed when two data sets, one small and another large enough to ideally be spared from movement, need to be joined over certain conditions or columns, Using a Spark broadcast variable, the smaller data set is broadcasted ny the driver to all Spark executors and subsequently joined with the larger data set on each executor.
![[Pasted image 20230724164204.png]]

By default Spark will use a broadcast join if the smaller data set is less than 10 MB.

**Common Case** -> When we have a commn set of keys between two DF, one holding less information than the other and we need to merge both.
(example)
![[Pasted image 20230724164407.png]]
*In this code we are forcing Spark to do a broadcast join, but it will resort to this type of join by default if the size of the smaller data is bellow othe spark.sql.autobroadcastJoinThreshHold*

***When to use broadcast hash join***

![[Pasted image 20230724164624.png]]


### Shuffle Sort Merge Join

It's an efficient way to merge two large datasets over a common key that is sortable, unique, and can be assigned to or stored in the same partition.

This join scheme has two phases: a sort phase fllowed by a merge phase. The sort phase sorts each data set by its desired join key; this phase iterates over each key in the row from each data set and merges the riws if the two keys amtch.

By default, the SortMergeJoin is enabled via spark.sql.join.oerferSortMergeJoin.

![[Pasted image 20230724165012.png]]

![[Pasted image 20230724170511.png]]
![[Pasted image 20230724170528.png]]

***Optimizing the shuffle sort merge join***

![[Pasted image 20230724171217.png]]

***When to use a shuffle sort merge join***

![[Pasted image 20230724172040.png]]


## Inspecting the Spark UI

Spark provides an elaborate web UI that allows us to inspect various components of our application.
A spark-submit job will launch the Spark UI, and you can connect to it on the local host (in local mode) or through the Spark driver at the default port 4040.

##### Journey through the Spark UI Tabs

![[Pasted image 20230725091515.png]]

***Jobs and Stages***

The Jobs and Stages tabs allow you to navigate through these and drill down to a granular level to examine the details of individual tasks.

The next figure shows when executors were added to or removed from the cluster.
It also provides a tabular list of all completed jobs in the cluster.
The Duration column indicates the time it took for each job to finish (If this time is high, it's a good indication that you  might want to investigate the stages in that job to see what tasks might be causing delays)

![[Pasted image 20230725091852.png]]

Stages provides a summary of the current state of all stages of all jobs in the app. 
We can see the average duration of each task, time spent in garbage collection (GC), and number of shuffle bytes/records read.
*If shuffle data is being read from remote executors, a high Shuffle Read Blocked Time can signal I/O issues.*

**In summary, GC is an automatic process of freeing up memory, preventing the program from running out of memory due to unused objects. "Shuffle Read Blocked Time" is a metric that indicates the time threads of the executor spend waiting for shuffle data, and it can be helpful in identifying I/O issues on remote nodes during a shuffle operation in Apache Spark.**

![[Pasted image 20230725092259.png]]

***Executors***

It provides information on the executors created for the app.
In addition, we can view how memory is used by each individual executor, and for what purpose.
This also helps to examine resource usage when you have used the cache() or persist() method on a DF or managed table.

![[Pasted image 20230725092513.png]]


***Storage***

In the Spark code in Shuffle Sort Merge Join we cached to managed tables after bucketing.

![[Pasted image 20230725092717.png]]

![[Pasted image 20230725092741.png]]


***SQL***

The effects of Spark SQL queries that are executed as part of your Spark app are traceable and viewable through the SQL tab.
We can see when the queries were executed and by which jobs, and their duration

![[Pasted image 20230725092905.png]]


***Environment***

Knowing about the environment in which your Spark app is running reveals many cues that are useful for troubleshooting. In fact, it's imperative to know what environment variables are set, what jars are included, what Spark properties are set, what system properties are set....

![[Pasted image 20230725093047.png]]


***Debugging Spark aplications***

We can also debug a Spark application in an IDE such IntelliJ.
Initially, this plethora of information can be overwhelming to a novice.