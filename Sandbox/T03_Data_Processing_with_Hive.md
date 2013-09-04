## Tutorial 3: Data Processing With Hive - Processing Baseball Stats With Hive

**This tutorial is from the [Hortonworks Sandbox](http://hortonworks.com/products/sandbox) - a single-node Hadoop cluster running in a virtual machine. Download to run this and other tutorials in the series.**

This tutorial was derived from one of the lab problems in the
Hortonworks Developer training class. The developer training class
covers uses of the tools in the Hortonworks Data Platform and how to
develop applications and projects using the Hortonworks Data Platform.
You can find more information about the course at [Hadoop Training for
Developers](http://hortonworks.com/hadoop-training/hadoop-training-for-developers/)

### Hortonworks Hadoop Essentials Video

[Apache Hive (running time: about 16
minutes)](http://www.youtube.com/watch?v=Pn7Sp2-hUXE)

### Data processing with Hive

Hive is a component of Hortonworks Data Platform(HDP). Hive provides a SQL-like interface to data stored in HDP. In the previous tutorial we used Pig which is a scripting language with a focus on dataflows. Hive provides a database query interface to Apache Hadoop.

People often ask why do Pig and Hive exist when they seem to do much of the same thing. Hive because of its SQL like query language is often used as the interface to an Apache Hadoop based data warehouse. Hive is considered friendlier and more familiar to users who are used to using SQL for querying data. Pig fits in through its data flow strengths where it takes on the tasks of bringing data into Apache Hadoop and working with it to get it into the form for querying. A good overview of how this works is in Alan Gates posting on the Yahoo Developer blog titled
[Pig and Hive at
Yahoo!](http://developer.yahoo.com/blogs/hadoop/posts/2010/08/pig_and_hive_at_yahoo/)
From a technical point of view both Pig and Hive are feature complete so
you can do tasks in either tool. However you will find one tool or the
other will be preferred by the different groups that have to use Apache
Hadoop. The good part is they have a choice and both tools work
together.

### Our data processing task

We are going to do the same data processing task as we just did with Pig
in the previous tutorial. We have several files of baseball statistics
and we are going to bring them into Hive and do some simple computing
with them. We are going to find the player with the highest runs for
each year. This file has all the statistics from 1871-2011 and contains
more that 90,000 rows. Once we have the highest runs we will extend the
script to translate a player id field into the first and last names of
the players.

### Downloading the data

The data files we are using comes from the site www.seanlahman.com. You
can download the data file from:

[http://seanlahman.com/files/database/lahman591-csv.zip](http://seanlahman.com/files/database/lahman591-csv.zip)

Once you have the file you will need to unzip it into a directory. We
will be uploading just the Master.csv and Batting.csv files from the
dataset.

### Uploading the data files

We start by selecting the File Browser from the top tool bar. The File
Browser shows you the files in the HDP file store. In this case the file
store resides in the Hortonworks Sandbox VM.

[![File
Browser](./images/tutorial-3/1FileBrowser.jpg?raw=true)](./images/tutorial-3/1FileBrowser.jpg?raw=true)

Click on the Upload button

[![Upload
Button](./images/tutorial-3/2UploadButton.jpg?raw=true)](./images/tutorial-3/2UploadButton.jpg?raw=true)

You want to select Files. Then you will get a dialog box.

[![Upload
Box](./images/tutorial-3/3UploadBox.jpg?raw=true)](./images/tutorial-3/3UploadBox.jpg?raw=true)

When you click on the Upload a file button you will get a dialog box.
Navigate to where you stored the Batting.csv file on your local disk and
select Batting.csv. Do the same thing for Master.csv. When you are done
you will see there are two files in your directory.

[![Loaded
Files](./images/tutorial-3/4LoadedFiles.jpg?raw=true)](./images/tutorial-3/4LoadedFiles.jpg?raw=true)

### Starting Beeswax, the Hive UI

Lets start Beeswax by clicking on the bee icon in the top bar. Beeswax
is a user interface to the Hive data warehouse system for Hadoop.

[![Start
Beeswax](./images/tutorial-3/5StartBeeswax.jpg?raw=true)](./images/tutorial-3/5StartBeeswax.jpg?raw=true)

Beeswax provides a GUI to Hive. On right is a query editor. There is a
limit of one query per execute cycle. A query may span multiple lines.
At the bottom there are buttons to Execute the query, Save the query
with a name, Explain the query and to start a new query.

[![Query
Editor](./images/tutorial-3/5_1QueryEditor.jpg?raw=true)](./images/tutorial-3/5_1QueryEditor.jpg?raw=true)

Before we get started let's take a look at how Pig and Hive data models
differ. In the case of Pig all data objects exist and are operated on in
the script. Once the script is complete all data objects are deleted
unless you stored them. In the case of Hive we are operating on the
Apache Hadoop data store. Any query you make, table that you create,
data that you copy persists from query to query. You can think of Hive
as providing a data workbench where you can examine, modify and
manipulate the data in Apache Hadoop. So when we perform our data
processing task we will execute it one query or line at a time. Once a
line successfully executes you can look at the data objects to verify if
the last operation did what you expected. All your data is live,
compared to Pig, where data objects only exist inside the script unless
they are copied out to storage. This kind of flexibility is Hive's
strength. You can solve problems bit by bit and change your mind on what
to do next depending on what you find.

The first task we will do is create a table to hold the data. We will
type the query into the composition area on the right like this. Once
you have typed in the query hit the Execute button at the bottom.

    create table temp_batting (col_value STRING);
                  
[![Create
Table](./images/tutorial-3/7CreateTable.jpg?raw=true)](./images/tutorial-3/7CreateTable.jpg?raw=true)

The query returns "No data available in the table" because at this point
we just created an empty table and we have not copied any data in it.

Once the query has executed we can click on Tables at the top of the
composition area and we will see we have a new table called
temp\_batting.

[![Tables](./images/tutorial-3/8Tables.jpg?raw=true)](./images/tutorial-3/8Tables.jpg?raw=true)

Clicking on the Browse Data button will let us see the data and right
now the table is empty. This is a good example of the interactive feel
you get with using Hive.

[![Empty
Table](./images/tutorial-3/9EmptyTable.jpg?raw=true)](./images/tutorial-3/9EmptyTable.jpg?raw=true)

The next line of code will load the data file Batting.csv into the table
temp\_batting. We can start typing the code and we will notice there is
a helper feature that helps us fill in the correct path to our file.

[![Helper](./images/tutorial-3/10Helper.jpg?raw=true)](./images/tutorial-3/10Helper.jpg?raw=true)

The complete query looks like this.

    LOAD DATA INPATH '/user/sandbox/Batting.csv' OVERWRITE INTO TABLE temp_batting;

[![Load](./images/tutorial-3/11Load.jpg?raw=true)](./images/tutorial-3/11Load.jpg?raw=true)

After executing the query we can look at the Tables again and when we
browse the data for temp\_batting we see that the data has been read in.
Note Hive consumed the data file Batting.csv during this step. If you
look in the File Browser you will see Batting.csv is no longer there.

[![Data](./images/tutorial-3/12Data.jpg?raw=true)](./images/tutorial-3/12Data.jpg?raw=true)

Now that we have read the data in we can start working with it. The next
thing we want to do extract the data. So first we will type in a query
to create a new table called batting to hold the data. That table will
have three columns for player\_id, year and the number of runs.

    create table batting (player_id STRING, year INT, runs INT);
                  
[![Create
Batting](./images/tutorial-3/13Createbatting.jpg?raw=true)](./images/tutorial-3/13Createbatting.jpg?raw=true)

Then we extract the data we want from temp\_batting and copy it into
batting. We will do this with a regexp pattern. To do this we are going
to build up a multi-line query. The first line of the query create the
table batting. The three regexp\_extract calls are going to extract the
player\_id, year and run fields from the table temp\_batting. When you
are done typing the query it will look like this. Be careful as there
are no spaces in the regular expression pattern.

    insert overwrite table batting
    SELECT
      regexp_extract(col_value, '^(?:([^,]*)\,?){1}', 1) player_id,
      regexp_extract(col_value, '^(?:([^,]*)\,?){2}', 1) year,
      regexp_extract(col_value, '^(?:([^,]*)\,?){9}', 1) run
    from temp_batting;
                  
[![Extract](./images/tutorial-3/14Extract.jpg?raw=true)](./images/tutorial-3/14Extract.jpg?raw=true)

Execute the query and look at the batting table. You should see data
that looks like this.

[![Batting
Data](./images/tutorial-3/15battingData.jpg?raw=true)](./images/tutorial-3/15battingData.jpg?raw=true)

Now we have the data fields we want. The next step is to group the data
by year so we can find the highest score for each year. This query first
groups all the records by year and then selects the player with the
highest runs from each year.

    SELECT year, max(runs) FROM batting GROUP BY year;
                  
[![Select Max
Year](./images/tutorial-3/17SelectMaxYr.jpg?raw=true)](./images/tutorial-3/17SelectMaxYr.jpg?raw=true)

The results of the query look like this.

[![Results Max
Year](./images/tutorial-3/18ResultsMaxYr.jpg?raw=true)](./images/tutorial-3/18ResultsMaxYr.jpg?raw=true)

Now we need to go back and get the player\_id(s) so we know who the
player(s) was. We know that for a given year we can use the runs to find
the player(s) for that year. So we can take the previous query and join
it with the batting records to get the final table.

    SELECT a.year, a.player_id, a.runs from batting a
    JOIN (SELECT year, max(runs) runs FROM batting GROUP BY year ) b
    ON (a.year = b.year AND a.runs = b.runs) ;

[![Join](./images/tutorial-3/19SelectJoin.jpg?raw=true)](./images/tutorial-3/19SelectJoin.jpg?raw=true)

The resulting data looks like:

[![Select Join
Results](./images/tutorial-3/20SelectJoinResults.jpg?raw=true)](./images/tutorial-3/20SelectJoinResults.jpg?raw=true)

This query may take a couple of minutes. While you’re waiting, if you
have internet access, take a look at this video from Alan Gates to hear
about the future of HCatalog: \
[Future of HCatalog](http://www.youtube.com/watch?v=gTwhSAEEe1I)

So now we have our results. As described earlier we solved this problem
using Hive step by step. At any time we were free to look around at the
data, decide we needed to do another task and come back. At all times
the data is live and accessible to us.