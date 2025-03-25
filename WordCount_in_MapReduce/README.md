# How to Execute WordCount Program in MapReduce using Cloudera Distribution Hadoop(CDH)

# 1. Introduction

This project implements the WordCount program using Hadoop MapReduce on the Cloudera Distribution of Hadoop (CDH). The WordCount program reads a text file, tokenizes it into words, and counts the occurrences of each word using the MapReduce framework. The program is executed on Cloudera Hadoop and developed using Eclipse for Java coding.

# 2. Prerequisites

Before running the program, ensure you have the following installed:

1) Cloudera Hadoop (CDH 5.x or later)
2) Java JDK 8+
3) Eclipse IDE with Hadoop Libraries
4) HDFS (Hadoop Distributed File System) configured
5) Git (Optional, for version control)

# 3. Steps to Execute WordCount in Cloudera Hadoop

Step 1: Start Cloudera Hadoop Services

1. Open Cloudera Manager.
2. Start HDFS and YARN ResourceManager.
3. Open a terminal in Cloudera and verify services using:

hdfs dfsadmin -report
yarn node -list

Step 2: Set Up Eclipse for Hadoop Development

1. Open Eclipse IDE.
2. Create a new Java Project.
3. Add the Hadoop libraries to the project by configuring the Build Path.
4. Create a package (e.g., wordcount.hadoop).

Step 3: Implement WordCount in Java

Create three Java files inside the package:

1. WordCountMapper.java (Mapper function)
2. WordCountReducer.java (Reducer function)
3. WordCount.java (Driver program)

Steps: 

1. First Open Eclipse -> then select File -> New -> Java Project ->Name it WordCount -> then Finish.

![image](https://github.com/user-attachments/assets/84aaa6f4-9dcb-40ba-a4a6-8aa0d3103148)
 
2. Create Three Java Classes into the project. Name them WCDriver(having the main function), WCMapper, WCReducer.
3. You have to include two Reference Libraries for that:
   Right Click on Project -> then select Build Path-> Click on Configure Build Path

![image](https://github.com/user-attachments/assets/f6301fc2-0845-454f-b5d6-2b790d221315)

4. In the above figure, you can see the Add External JARs option on the Right Hand Side. Click on it and add the below mention files. You can find these files in /usr/lib/
   1. /usr/lib/hadoop-0.20-mapreduce/hadoop-core-2.6.0-mr1-cdh5.13.0.jar 
   2. /usr/lib/hadoop/hadoop-common-2.6.0-cdh5.13.0.jar
  
![image](https://github.com/user-attachments/assets/f0f859ac-e1b9-456f-acc2-a7f719e8e484)

5. Mapper Code: You have to copy paste this program into the WCMapper Java Class file.

6. Reducer Code: You have to copy paste this program into the WCReducer Java Class file.
   
7. Driver Code: You have to copy paste this program into the WCDriver Java Class file.
 
8. Now you have to make a jar file. Right Click on Project-> Click on Export-> Select export destination as Jar File-> Name the jar File(WordCount.jar) -> Click on next -> at last Click on Finish. Now copy this file into the Workspace directory of Cloudera

![image](https://github.com/user-attachments/assets/38652200-1872-4b1c-bd78-ec0dd7eca30a)

![image](https://github.com/user-attachments/assets/94ae5404-4337-410c-a142-78253ea899d6)

![image](https://github.com/user-attachments/assets/b0ce594a-13e2-4b98-9b4e-4cdd66f5ba3d)

9. Open the terminal on CDH and change the directory to the workspace. You can do this by using “cd workspace/” command. Now, Create a text file(WCFile.txt) and move it to HDFS. For that open terminal and write this code(remember you should be in the same directory as jar file you have created just now).
 
![image](https://github.com/user-attachments/assets/850f9500-dff1-44a7-9d88-02af2bafa30a)

10. Now, run this command to copy the file input file into the HDFS.
 
      hadoop fs -put WCFile.txt WCFile.txt

![image](https://github.com/user-attachments/assets/a81c9de7-b832-4e3a-bfcc-37cca485f074)

11. Now to run the jar file by writing the code as shown in the screenshot.

![image](https://github.com/user-attachments/assets/09a6515d-de5b-4abe-92f2-b9c6e5437faf)

12. After Executing the code, you can see the result in WCOutput file or by writing following command on terminal.
 
      hadoop fs -cat WCOutput/part-00000

![image](https://github.com/user-attachments/assets/bbfcb60d-a225-415d-9714-3d340b1d976a)

 



