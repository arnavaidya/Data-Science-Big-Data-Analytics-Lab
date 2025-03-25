# HiveQL Demo Problem Statement

Write an application using HiveQL for flight information system which will include a. Creating, Dropping, and altering Database tables. b. Creating an external Hive table. c. Load table with data, insert new values and field in the table, Join tables with Hive d. Create index on Flight Information Table e. Find the average departure delay per day in 2008.

# Step 1: Start HBase
    hbase
This command starts HBase and provides various options.

# Step 2: Enter HBase Shell
    hbase shell
This launches the HBase shell.

# Step 3: Create an HBase Table
Create a table named flight with column families finfo and fsch.
    create 'flight','finfo','fsch'
Check if the table is created:
    list
    
# Step 4: Insert Data into HBase
Insert flight records with different source, destination, arrival time, and departure time.

put 'flight',1,'finfo:src','Pune'
put 'flight',1,'finfo:dest','Mumbai'
put 'flight',1,'fsch:at','10.25a.m.'
put 'flight',1,'fsch:dt','11.25a.m.'
put 'flight',1,'fsch:delay','5min'

put 'flight',2,'finfo:src','Pune'
put 'flight',2,'finfo:dest','Kolkata'
put 'flight',2,'fsch:at','07.00a.m.'
put 'flight',2,'fsch:dt','07.30a.m.'
put 'flight',2,'fsch:delay','2min'

# Step 5: Scan the HBase Table
    scan 'flight'
This retrieves all records in the flight table.

# Step 6: Modify the HBase Table
Add a new column family named revenue.
    alter 'flight', NAME=>'revenue'
Insert revenue data for a flight:
    put 'flight',4,'revenue:rs','45000'
Scan the table again:
    scan 'flight'
Delete the revenue column:
    alter 'flight', NAME=>'revenue', METHOD=>'delete'

# Step 7: Create and Drop Tables in HBase
Create a new table tb1:
    create 'tb1','cf'
    list
Disable and drop tb1:
    disable 'tb1'
    drop 'tb1'
    list

# Step 8: Retrieve Specific Data
Get all data for row 1:
    get 'flight',1
Get only specific columns:
    get 'flight','1',COLUMN=>['finfo:src','finfo:dest']
Scan only the finfo:src column:
    scan 'flight',COLUMNS=>'finfo:src'

# Step 9: Create Another Table emphivee and Insert Employee Data
create 'emphivee','cf'
put 'emphivee',1,'cf:name','Arnav'
put 'emphivee',1,'cf:sal',45000
put 'emphivee',2,'cf:name','Pranav'
put 'emphivee',2,'cf:sal',40000
put 'emphivee',3,'cf:name','Sampada'
put 'emphivee',3,'cf:sal',42000

Scan the table:
    scan 'emphivee'

# Step 10: Alter Table to Add Delay Data
alter 'flight',NAME=>'delay'
put 'flight',1,'delay:dl',10
put 'flight',2,'delay:dl',5
put 'flight',3,'delay:dl',4
put 'flight',4,'delay:dl',16
scan 'flight'

# Step 11: Start Hive
    hive

# Step 12: Create an External Hive Table
CREATE EXTERNAL TABLE empdata123(ename STRING, esal INT)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ' '
STORED AS TEXTFILE
LOCATION '/home/cloudera/Desktop/33280/Workspace/Assignment_3/empdata123';

Load data into Hive table:

LOAD DATA LOCAL INPATH '/home/cloudera/Desktop/33280/Workspace/Assignment_3/empdata123'
INTO TABLE empdata123;

Query the table:

SELECT * FROM empdata123;

# Step 13: Create a Hive Table Linked to HBase

CREATE EXTERNAL TABLE hivee_table_emp(id INT, name STRING, esal INT)
STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
WITH SERDEPROPERTIES ("hbase.columns.mapping"=":key,cf:name,cf:sal")
TBLPROPERTIES ("hbase.table.name"="emphivee");

Query the table:

SELECT * FROM hivee_table_emp;

# Step 14: Create Another Hive Table and Insert Data

CREATE TABLE empdbnew(eno INT, ename STRING, esal INT)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ' '
STORED AS TEXTFILE;

Load data:

LOAD DATA LOCAL INPATH '/home/cloudera/Desktop/33280/Workspace/Assignment_3/empdata321'
INTO TABLE empdbnew;

Check the data:

SELECT * FROM empdbnew;

Insert Hive table data into HBase table:

INSERT INTO hivee_table_emp SELECT * FROM empdbnew;

Verify insertion:

SELECT * FROM hivee_table_emp;

# Step 15: Create a Hive Table for Flights Data in HBase

CREATE EXTERNAL TABLE hbase_flight_new(
    fno INT, 
    fsource STRING,
    fdest STRING,
    fsh_at STRING,
    fsh_dt STRING,
    fsch_delay STRING,
    delay INT
)
STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
WITH SERDEPROPERTIES (
    "hbase.columns.mapping"=":key,finfo:src,finfo:dest,fsch:at,fsch:dt,fsch:delay,delay:dl"
)
TBLPROPERTIES ("hbase.table.name"="flight");
