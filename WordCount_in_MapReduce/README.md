# How to Execute WordCount Program in MapReduce using Cloudera Distribution Hadoop(CDH)

# 1. Introduction

This project implements the WordCount program using Hadoop MapReduce on the Cloudera Distribution of Hadoop (CDH). The WordCount program reads a text file, tokenizes it into words, and counts the occurrences of each word using the MapReduce framework. The program is executed on Cloudera Hadoop and developed using Eclipse for Java coding.

# 2. Prerequisites

Before running the program, ensure you have the following installed:

Cloudera Hadoop (CDH 5.x or later)

Java JDK 8+

Eclipse IDE with Hadoop Libraries

HDFS (Hadoop Distributed File System) configured

Git (Optional, for version control)

# 3. Steps to Execute WordCount in Cloudera Hadoop

Step 1: Start Cloudera Hadoop Services

Open Cloudera Manager.

Start HDFS and YARN ResourceManager.

Open a terminal in Cloudera and verify services using:

hdfs dfsadmin -report
yarn node -list

Step 2: Set Up Eclipse for Hadoop Development

Open Eclipse IDE.

Create a new Java Project.

Add the Hadoop libraries to the project by configuring the Build Path.

Create a package (e.g., wordcount.hadoop).

Step 3: Implement WordCount in Java

Create three Java files inside the package:

WordCountMapper.java (Mapper function)

WordCountReducer.java (Reducer function)

WordCount.java (Driver program)
