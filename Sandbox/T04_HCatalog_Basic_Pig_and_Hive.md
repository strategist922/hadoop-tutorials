## Tutorial 4: HCatalog, Basic Pig & Hive Commands

**This tutorial is from the [Hortonworks Sandbox](http://hortonworks.com/products/sandbox) - a single-node Hadoop cluster running in a virtual machine. Download to run this and other tutorials in the series.**

This tutorial was derived from one of the lab problems in the
Hortonworks Developer training class. The developer training class
covers uses of the tools in the Hortonworks Data Platform and how to
develop applications and projects using the Hortonworks Data Platform.
You can find more information about the course at [Hadoop Training for
Developers](http://hortonworks.com/hadoop-training/hadoop-training-for-developers/)

We value your feedback. When you’re done with this tutorial, please tell
us what you think by filling out this
[survey](https://www.surveymonkey.com/s/SandboxT4HcatPigHive) . We
really do pay attention and read your comments!

### Hortonworks Hadoop Essentials Video

[Apache HCatalog (running time: about 9
minutes)](http://www.youtube.com/watch?v=_dVlNu4lqpE)

### Downloading Example Data

For this tutorial, we will use a baseball statistics file. This file has
all the statistics for each American player by year from 1871-2011. The
data set is fairly large (over 95,000 records), but to learn Big Data
you don't need to use a massive dataset. You need only use tools that
scale to massive datasets.

The data files we are using in this tutorial come from Sean Lahman’s
extensive historical baseball database
([http://seanlahman.com/](http://seanlahman.com/)), and are being used
under a Creative Commons Attribution-ShareAlike license:
[http://creativecommons.org/licenses/by-sa/3.0/](http://creativecommons.org/licenses/by-sa/3.0/)

Download and unzip the data file from this URL:

[http://seanlahman.com/files/database/lahman591-csv.zip](http://seanlahman.com/files/database/lahman591-csv.zip)

The zip archive includes many statistics files. We will only use the
following two files:

-   Master.csv
-   Batting.csv

### Uploading the data files

Start by selecting the File Browser from the top tool bar. The File
Browser allows you to view the Hortonworks Data Platform (HDP) file
store. The HDP file system is separate from the local file system.

[![](./images/tutorial-4/Intro-1.jpg?raw=true)](./images/tutorial-4/Intro-1.jpg?raw=true)

Click **Upload** and select **Files** to upload files to HDFS.

[![](./images/tutorial-4/Intro-2.jpg?raw=true)](./images/tutorial-4/Intro-2.jpg?raw=true)

A dialog box appears.

[![](./images/tutorial-4/Intro-3.jpg?raw=true)](./images/tutorial-4/Intro-3.jpg?raw=true)

Click **Upload a file**, and you will get a dialog box. Navigate to
where you stored the data files on your local disk. Select 'Batting.csv'
and 'Master.csv' files and select **Choose**.

When you are done, you will see the two files in your directory.

[![](./images/tutorial-4/Intro-4.jpg?raw=true)](./images/tutorial-4/Intro-4.jpg?raw=true)

### Create tables for the Data Using HCatalog

Now that you've uploaded a file to HDFS, you will create an HCatalog
table so that the data can be accessible to both Pig and Hive.

Select the **HCat** icon in the icon bar at the top of the page:

[![](./images/tutorial-4/Intro-5.jpg?raw=true)](./images/tutorial-4/Intro-5.jpg?raw=true)

Select "Create a new table from file" from the ACTIONS menu on the left.

[![](./images/tutorial-4/Intro-6.jpg?raw=true)](./images/tutorial-4/Intro-6.jpg?raw=true)

This action takes you to **Step 1: Choose File**. On this page, you will
create a table for the batting.csv file, as follows:

-   Name the table "batting\_data"
-   Leave the optional description blank
-   Click 'Choose a file'**Next**

[![](./images/tutorial-4/Intro-7.jpg?raw=true)](./images/tutorial-4/Intro-7.jpg?raw=true)

This action takes you to **Step 2: Create a new table from a file**.

Complete these steps:

-   Scroll to the right and change column name R to "Runs" and also
    change its Column type to "int"
-   Click **Create Table**

[![](./images/tutorial-4/Intro-9.jpg?raw=true)](./images/tutorial-4/Intro-9.jpg?raw=true)

You will see a new table "batting\_data" has been created:

[![](./images/tutorial-4/Intro-10.jpg?raw=true)](./images/tutorial-4/Intro-10.jpg?raw=true)

Repeat above steps for the second data set (**master.csv**) and create a
new table named "master\_data". You do not need to make any changes in
Step 2 and Step 3 for this table.

[![](./images/tutorial-4/Intro-11.jpg?raw=true)](./images/tutorial-4/Intro-11.jpg?raw=true)

Now two tables have been created on input data, which Hive and Pig can
use for further processing.

### A Short Apache Hive Tutorial

In the previous sections you:

-   Uploaded your data file into HDFS
-   Used Apache HCatalog to create tables

In this tutorial, you will use Apache Hive to perform basic queries on
the data.

Apache Hive™ provides a data warehouse function to the Hadoop cluster.
Through the use of HiveQL you can view your data as a table and create
queries just as you would in a database.

To make it easy to interact with Hive, you can use a tool in the
Hortonworks Sandbox called **Beeswax**. Beeswax provides an interactive
interface to Hive where you can type in queries and Hive will evaluate
them using a series of MapReduce jobs.

Open Beeswax. Click on the bee icon on the top bar.

[![](./images/tutorial-4/Intro-12.jpg?raw=true)](./images/tutorial-4/Intro-12.jpg?raw=true)

Notice the query window and execute button. Type your queries in the
Query window. When you are done with a query, click the execute button.

Note: You can only type one query in the composition window at a given
time. You cannot type multiple queries separated by semicolons.

Since you loaded your data and created your table in HCatalog, Hive
automatically knows about the data.

To see tables that Hive knows about, in Query Editor type the query:

    show tables

and click on **Execute**.

[![](./images/tutorial-4/Intro-13.jpg?raw=true)](./images/tutorial-4/Intro-13.jpg?raw=true)

Notice the tables that you previously created are in the list
("batting\_data" and "master\_data").

[![](./images/tutorial-4/Intro-14.jpg?raw=true)](./images/tutorial-4/Intro-14.jpg?raw=true)

Hive inherits schema and location information from HCatalog. As a
result, you do not have to provide this information in the Hive queries.
If we did not have HCatalog, we would have to build the table using
HiveQL and provide location and schema information.

To see the records type:

    select * from batting_data

in Query Editor and click **Execute**.

[![](./images/tutorial-4/Intro-15.jpg?raw=true)](./images/tutorial-4/Intro-15.jpg?raw=true)
[![](./images/tutorial-4/Intro-16.jpg?raw=true)](./images/tutorial-4/Intro-16.jpg?raw=true)

You can see the columns in the table by executing:

    describe batting_data

[![](./images/tutorial-4/Intro-17.jpg?raw=true)](./images/tutorial-4/Intro-17.jpg?raw=true)
[![](./images/tutorial-4/Intro-18.jpg?raw=true)](./images/tutorial-4/Intro-18.jpg?raw=true)

You can make a join with other tables in Pig the same way you do with
other database queries.

Let's make a join between batting\_data and master\_data tables:

Enter the following into the query editor:

    select a.playerid, a.namefirst, a.namelast, b.yearid, b.runsfrom master_data ajoin batting_data b ON (b.playerid = a.playerid)
                  

[![](./images/tutorial-4/Intro-19.jpg?raw=true)](./images/tutorial-4/Intro-19.jpg?raw=true)

This job is more complex so takes longer than previous queries. You can
watch the job running in the log.

[![](./images/tutorial-4/Intro-20.jpg?raw=true)](./images/tutorial-4/Intro-20.jpg?raw=true)

When the job completes, you can see the results.

[![](./images/tutorial-4/Intro-21.jpg?raw=true)](./images/tutorial-4/Intro-21.jpg?raw=true)

## Pig Basics Tutorial

In this tutorial, you will create and execute a Pig script.

To access the Pig interface, click the Pig icon on the icon bar at the
top of your screen. This action brings up the Pig user interface. On the
left is a list of your scripts and on the right is a composition box for
your scripts.

A special feature of the interface is the Pig helper at the bottom. The
Pig helper provides templates for the statements, functions, I/O
statements, HCatLoader() and Python user defined functions.\
 At the bottom are status areas that show the results of script and log
files.

[![](./images/tutorial-4/Intro-22.jpg?raw=true)](./images/tutorial-4/Intro-22.jpg?raw=true)

In this section, you will load the data from the table that is stored in
HCatalog.  Then you will make a join between two data sets on the Player
ID field in the same way that you did in the Hive section.

### Step 1: Create and name the script

Open the Pig interface by clicking the Pig icon at the top of the
screen.

[![](./images/tutorial-4/Intro-23.jpg?raw=true)](./images/tutorial-4/Intro-23.jpg?raw=true)

Title your script by filling in the title box.

[![](./images/tutorial-4/Intro-24a.jpg?raw=true)](./images/tutorial-4/Intro-24a.jpg?raw=true)

### Step 2: Prepare to load the data

The data is already in HDFS through HCatalog. HCatalog stores schema and
location information, so we can use the HCatLoader() function within the
Pig script to read data from HCatalog-managed tables. In Pig, you now
only need to give the table a name or alias so that Pig can process the
table.

Follow this procedure to load the data using HCatLoader:

-   Use the right-hand pane to start adding your code at Line 1
-   Open the Pig helper drop-down menu at the bottom of the screen to
    give you a template for the line.

[![](./images/tutorial-4/Intro-25a.jpg?raw=true)](./images/tutorial-4/Intro-25a.jpg?raw=true)

Choose **PIG helper -\> HCatalog-\>LOAD…**template. This action pastes
the Load template into the script area.

[![](./images/tutorial-4/Intro-26.jpg?raw=true)](./images/tutorial-4/Intro-26.jpg?raw=true)

-   The entry **%TABLE%** is highlighted in red. Type the name of the
    table ('**batting\_data**') in place of **%TABLE%**(single quotes
    are required).
-   Remember to add the "a = " before the template. This saves the
    results into "a".
-   Make sure the statement ends with a semi-colon (;)

Repeat this sequence for "master\_data" and add " b = "

The completed lines of code will be:

    a = LOAD 'batting_data' using org.apache.hcatalog.pig.HCatLoader();
    b = LOAD 'master_data' using org.apache.hcatalog.pig.HCatLoader();

[![](./images/tutorial-4/Intro-27a.jpg?raw=true)](./images/tutorial-4/Intro-27a.jpg?raw=true)

It is important to note that at this point, we have merely defined the
aliases for our tables to hold the data (alias "a" for batting data and
alias "b" for master data). Data is not loaded or transformed until we
execute an operational command such as DUMP or STORE

### Step 3: Join both the tables on Player ID

Next, you will use the JOIN operator to join both tables on the Player
ID. Master.data has the player's first name and last name and player ID
(among other fields). Batting.data has the player's run record and
player ID (among other fields). You will create a new data set using the
Pig Join function that will match the player ID field and include all of
the data from both tables.

Complete these steps:

-   Choose **PIG helper-\>Data processing functions-\>JOIN template**
-   Replace %VAR% with "a". Repeat this step on the same line for "b".
-   Again, add the trailing semi-colon to the code.

So, the final code will be:

    a = LOAD 'batting_data' using org.apache.hcatalog.pig.HCatLoader();
    b = LOAD 'master_data' using org.apache.hcatalog.pig.HCatLoader(); 
    c = join a by playerid, b by playerid;

[![](./images/tutorial-4/Intro-28.jpg?raw=true)](./images/tutorial-4/Intro-28.jpg?raw=true)

Now you have joined all the records in both of the tables on Player ID.

### Step 4: Execute the script and generate output

To complete the Join operation, use the DUMP command to execute the
results. This will show all of the records that have a common PlayerID.
The data from both tables will be merged into one row. \
 Complete this steps:

-   Add the last line with **PIG helper-\>I/O-\>DUMP**template and
    replace %VAR% with "c".

The full script should be:

    a = LOAD 'batting_data' using org.apache.hcatalog.pig.HCatLoader();
    b = LOAD 'master_data' using org.apache.hcatalog.pig.HCatLoader();
    c = join a by playerid, b by playerid;dump c;

[![](./images/tutorial-4/Intro-29.jpg?raw=true)](./images/tutorial-4/Intro-29.jpg?raw=true)

### Step 5: Save the script and execute it

At the bottom of the screen, click **Save** and **Execute** to run the
script. This action creates one or more MapReduce jobs.

Below the Execute button is a progress bar that shows the job's status.
The progress bar can be blue (indicating job is in process), red (job
has a problem), or green (job is complete).

[![](./images/tutorial-4/Intro-30.jpg?raw=true)](./images/tutorial-4/Intro-30.jpg?raw=true)

When the job completes, check the results in the green box. You can also
download results to your system by clicking the download icon.  The
result is that each line that starts with an open parenthesis "(" has
data from both tables for each unique player ID.

[![](./images/tutorial-4/Intro-31.jpg?raw=true)](./images/tutorial-4/Intro-31.jpg?raw=true)

Click the **Logs** link if you want to see what happened when your
script ran, including any error messages. (You might need to scroll down
to view the entire log.)

[![](./images/tutorial-4/Intro-32.jpg?raw=true)](./images/tutorial-4/Intro-32.jpg?raw=true)

Congratulations! You have successfully completed HCatalog, Basic Pig & Hive Commands.