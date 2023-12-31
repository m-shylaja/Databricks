Delta Lake Logo
Test License PyPI PyPI - Downloads

Delta Lake is an open-source storage framework that enables building a Lakehouse architecture with compute engines including Spark, PrestoDB, Flink, Trino, and Hive and APIs for Scala, Java, Rust, Ruby, and Python.

See the Delta Lake Documentation for details.
See the Quick Start Guide to get started with Scala, Java and Python.
Note, this repo is one of many Delta Lake repositories in the delta.io organizations including delta, delta-rs, delta-sharing, kafka-delta-ingest, and website.
The following are some of the more popular Delta Lake integrations, refer to delta.io/integrations for the complete list:

Apache Spark™: This connector allows Apache Spark™ to read from and write to Delta Lake.
Apache Flink (Preview): This connector allows Apache Flink to write to Delta Lake.
PrestoDB: This connector allows PrestoDB to read from Delta Lake.
Trino: This connector allows Trino to read from and write to Delta Lake.
Delta Standalone: This library allows Scala and Java-based projects (including Apache Flink, Apache Hive, Apache Beam, and PrestoDB) to read from and write to Delta Lake.
Apache Hive: This connector allows Apache Hive to read from Delta Lake.
Delta Rust API: This library allows Rust (with Python and Ruby bindings) low level access to Delta tables and is intended to be used with data processing frameworks like datafusion, ballista, rust-dataframe, vega, etc.

Table of Contents
Latest Binaries
See the online documentation for the latest release.

API Documentation
Scala API docs
Java API docs
Python API docs
Compatibility
Delta Standalone library is a single-node Java library that can be used to read from and write to Delta tables. Specifically, this library provides APIs to interact with a table’s metadata in the transaction log, implementing the Delta Transaction Log Protocol to achieve the transactional guarantees of the Delta Lake format.

API Compatibility
There are two types of APIs provided by the Delta Lake project.

Direct Java/Scala/Python APIs - The classes and methods documented in the API docs are considered as stable public APIs. All other classes, interfaces, methods that may be directly accessible in code are considered internal, and they are subject to change across releases.
Spark-based APIs - You can read Delta tables through the DataFrameReader/Writer (i.e. spark.read, df.write, spark.readStream and df.writeStream). Options to these APIs will remain stable within a major release of Delta Lake (e.g., 1.x.x).
See the online documentation for the releases and their compatibility with Apache Spark versions.
Data Storage Compatibility
Delta Lake guarantees backward compatibility for all Delta Lake tables (i.e., newer versions of Delta Lake will always be able to read tables written by older versions of Delta Lake). However, we reserve the right to break forward compatibility as new features are introduced to the transaction protocol (i.e., an older version of Delta Lake may not be able to read a table produced by a newer version).

Breaking changes in the protocol are indicated by incrementing the minimum reader/writer version in the Protocol action.

Roadmap
For the high-level Delta Lake roadmap, see Delta Lake 2022H1 roadmap.
For the detailed timeline, see the project roadmap.
Transaction Protocol
Delta Transaction Log Protocol document provides a specification of the transaction protocol.

Requirements for Underlying Storage Systems
Delta Lake ACID guarantees are predicated on the atomicity and durability guarantees of the storage system. Specifically, we require the storage system to provide the following.

Atomic visibility: There must be a way for a file to be visible in its entirety or not visible at all.
Mutual exclusion: Only one writer must be able to create (or rename) a file at the final destination.
Consistent listing: Once a file has been written in a directory, all future listings for that directory must return that file.
See the online documentation on Storage Configuration for details.

Concurrency Control
Delta Lake ensures serializability for concurrent reads and writes. Please see Delta Lake Concurrency Control for more details.

Reporting issues
We use GitHub Issues to track community reported issues. You can also contact the community for getting answers.

Contributing
We welcome contributions to Delta Lake. See our CONTRIBUTING.md for more details.

We also adhere to the Delta Lake Code of Conduct.

Building
Delta Lake is compiled using SBT.

To compile, run

build/sbt compile
To generate artifacts, run

build/sbt package
To execute tests, run

build/sbt test
To execute a single test suite, run

build/sbt 'testOnly org.apache.spark.sql.delta.optimize.OptimizeCompactionSuite'
To execute a single test within and a single test suite, run

build/sbt 'testOnly *.OptimizeCompactionSuite -- -z "optimize command: on partitioned table - all partitions"'
Refer to SBT docs for more commands.

IntelliJ Setup
IntelliJ is the recommended IDE to use when developing Delta Lake. To import Delta Lake as a new project:

Clone Delta Lake into, for example, ~/delta.
In IntelliJ, select File > New Project > Project from Existing Sources... and select ~/delta.
Under Import project from external model select sbt. Click Next.
Under Project JDK specify a valid Java 1.8 JDK and opt to use SBT shell for project reload and builds.
Click Finish.
Setup Verification
After waiting for IntelliJ to index, verify your setup by running a test suite in IntelliJ.

Search for and open DeltaLogSuite
Next to the class declaration, right click on the two green arrows and select Run 'DeltaLogSuite'
Troubleshooting
If you see errors of the form

Error:(46, 28) object DeltaSqlBaseParser is not a member of package io.delta.sql.parser
import io.delta.sql.parser.DeltaSqlBaseParser._
...
Error:(91, 22) not found: type DeltaSqlBaseParser
    val parser = new DeltaSqlBaseParser(tokenStream)
then follow these steps:

Compile using the SBT CLI: build/sbt compile.
Go to File > Project Structure... > Modules > delta-spark.
In the right panel under Source Folders remove any target folders, e.g. target/scala-2.12/src_managed/main [generated]
Click Apply and then re-run your test.
License
Apache License 2.0, see LICENSE.

Community
There are two mediums of communication within the Delta Lake community.

Public Slack Channel
Register here
Login here
Linkedin page
Youtube channel
Public Mailing list
