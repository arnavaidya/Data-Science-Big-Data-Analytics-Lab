# Log file processing distributed application using MapReduce
Design a distributed application using MapReduce which processes a log file of a system. List out the users who have logged for maximum period on the system. Use simple log file from the Internet and process it using a pseudo distribution mode on Hadoop platform.

# 1. Introduction

This project implements a Log Processing program using Hadoop MapReduce on the Cloudera Distribution of Hadoop (CDH). The program reads a log file, extracts and counts occurrences of specific patterns (e.g., IP addresses, error codes), and processes them using HDFS and MapReduce. The program is developed in Java using Eclipse IDE and executed on Cloudera Hadoop.

# 2. Prerequisites

Before running the program, ensure you have the following installed:

1. Cloudera Hadoop (CDH 5.x or later)
2. Java JDK 8+
3. Eclipse IDE with Hadoop Libraries
4. HDFS (Hadoop Distributed File System) configured
5. Git (Optional, for version control)

# 3.Steps to Execute Log Processing in Cloudera Hadoop
Step 1: Start Cloudera Hadoop Services

1. Open Cloudera Manager.
2. Start HDFS and YARN ResourceManager.
3. Open a terminal in Cloudera and verify services using:

        hdfs dfsadmin -report
        yarn node -list

Step 2: Set Up Eclipse for Hadoop Development
1. Open Eclipse IDE.
2. Create a new Java Project (e.g., LogProcessor).
3. Add Hadoop Libraries:
    1. Right-click on the project → Build Path → Configure Build Path.
    2. Click Add External JARs and select:
                   /usr/lib/hadoop-0.20-mapreduce/hadoop-core-2.6.0-mr1-cdh5.13.0.jar
                   /usr/lib/hadoop/hadoop-common-2.6.0-cdh5.13.0.jar

Step 3: Implement WordCount in Java

Create three Java classes inside the project:

1. LogMapper.java (Mapper function)
2. LogReducer.java (Reducer function)
3. LogDriver.java (Driver program)

Step 4: Compile and Create a JAR File
Right-click on the project → Export → Select JAR File.

Name the JAR file as LogProcessor.jar and save it.

Move the JAR file to the Cloudera workspace directory.

Step 5: Upload Log File to HDFS
Open Cloudera terminal and change the directory to the workspace:
    
    cd workspace/
    
Create a log file access_log.txt with sample data.

Move it to HDFS:

    hadoop fs -put access_log.txt access_log.txt

Step 6: Run the Log Processing Program
Execute the JAR file in Hadoop:

    hadoop jar LogProcessor.jar LogDriver access_log.txt LogOutput

Step 7: View the Output
Check the results using:

    hadoop fs -cat LogOutput/part-00000

this will display processed log data (e.g., IP counts, error counts).
 



