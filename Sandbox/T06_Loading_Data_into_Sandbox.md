## Tutorial 6: Loading Data into the Hortonworks Sandbox

**This tutorial is from the [Hortonworks Sandbox](http://hortonworks.com/products/sandbox) - a single-node Hadoop cluster running in a virtual machine. Download to run this and other tutorials in the series.**

### Summary

This tutorial describes how to load data into the Hortonworks sandbox.

The Hortonworks sandbox is a fully contained Hortonworks Data Platform
(HDP) environment. The sandbox includes the core Hadoop components (HDFS
and MapReduce), as well as all the tools needed for data ingestion and
processing. You can access and analyze sandbox data with many Business
Intelligence (BI) applications.

In this tutorial, we will load and review data for a fictitious web
retail store in what has become an established use case for Hadoop:
deriving insights from large data sources such as web logs. By combining
web logs with more traditional customer data, we can better understand
our customers, and also understand how to optimize future promotions and
advertising.

### Prerequisites:

-   Hortonworks ODBC driver installed and configured
-   Hortonworks Sandbox 1.3 (installed and running)

### Overview

To load data into the Hortonworks sandbox, you will:

-   Download sample data to your computer.
-   Upload the data files into the sandbox
-   View and refine the data in the sandbox.

### Step 1: Download the Sample Data

-   You can download a set of sample data contained in a compressed
    (.zip) folder here:

    [RefineDemoData.zip](https://s3.amazonaws.com/hw-sandbox/tutorial8/RefineDemoData.zip)

-   Save the sample data .zip file to your computer, then extract the
    files.

**Note:** The extracted data files should have a .tsv.gz file extension.
If you download the files using a browser, the file extension may change
to .tsv.gz.tsv. If this happens, change the file extensions back to
.tsv.gz before uploading the files into the sandbox.

### Step 2: Upload the Data Files into the Sandbox

-   In the Hortonworks Sandbox, click the HCat icon to open the HCatalog
    page, then click **Create a new table from a file**.

    [![](./images/tutorial-6/01_HCatalog.jpg?raw=true)](./images/tutorial-6/01_HCatalog.jpg?raw=true)
-   On the “Create a new table from a file” page, type “omniturelogs” in
    the Table Name box, then click **Choose a file**.

    [![](./images/tutorial-6/02_choose_file1.jpg?raw=true)](./images/tutorial-6/02_choose_file1.jpg?raw=true)
-   On the "Choose a file" pop-up, click **Upload a file** to display a
    file browser.

    [![](./images/tutorial-6/03_choose_file2.jpg?raw=true)](./images/tutorial-6/03_choose_file2.jpg?raw=true)
-   Use the file browser to select the Omniture.0.tsv.gz file, then
    click **Open**.

    [![](./images/tutorial-6/04_choose_file3.jpg?raw=true)](./images/tutorial-6/04_choose_file3.jpg?raw=true)
-   After you select the select the Omniture.0.tsv.gz file, it appears
    in the list on the "Choose a file" pop-up. Click the file name to
    select the Omniture.0.tsv.gz file.

    [![](./images/tutorial-6/05_choose_file4.jpg?raw=true)](./images/tutorial-6/05_choose_file4.jpg?raw=true)
-   The "Create a new table from a file" page is redisplayed with the
    Omniture.0.tsv.gz in the Input File box.

    [![](./images/tutorial-6/06_choose_file5.jpg?raw=true)](./images/tutorial-6/06_choose_file5.jpg?raw=true)
-   Clear the check box next to “Read column headers” to create the
    table using default column names (col\_1, col\_2, etc.).

    [![](./images/tutorial-6/07_choose_delimiter.jpg?raw=true)](./images/tutorial-6/07_choose_delimiter.jpg?raw=true)
-   Scroll down to the bottom of the page and click **Create Table**. A
    progress indicator will appear at the top of the page while the
    table is being created.

    [![](./images/tutorial-6/08_define_columns.jpg?raw=true)](./images/tutorial-6/08_define_columns.jpg?raw=true)
-   After the table is created, the "omniturelogs" table appears in the
    list on the HCatalog page.

    [![](./images/tutorial-6/09_HCatalog_newtable.jpg?raw=true)](./images/tutorial-6/09_HCatalog_newtable.jpg?raw=true)
-   Repeat this procedure for the users.tsv.gz file using the table name
    “users,” and for the products.tsv.gz using the table name
    “products.” When creating these tables, leave the “Read column
    headers” check box selected to create the tables using the first row
    as the column names.

### Step 3: View and Refine the Data in the Sandbox

In the previous section, we created sandbox tables from uploaded data
files. Now let’s take a closer look at that data.

Here’s a summary of the data we’re working with:

-   `omniturelogs` – website logs containing information such as URL,
    timestamp, IP address, geocoded IP, and session ID.
-   `users` – CRM user data listing SWIDs (Software User IDs) along with date of birth and gender.
-   `products` – CMS data that maps product categories to website URLs.
-   Let’s start by looking at the raw omniture data. Click the File Browser icon in the toolbar at the top of the page, then select the `Omniture.0.tsv.gz` file. 

    [![](./images/tutorial-6/10_file_browser.jpg?raw=true)](./images/tutorial-6/10_file_browser.jpg?raw=true)
-   The raw data file appears in the File Browser, and you can see that
    it contains information such as URL, timestamp, IP address, geocoded
    IP, and session ID.

    [![](./images/tutorial-6/11_omniturelog_raw.jpg?raw=true)](./images/tutorial-6/11_omniturelog_raw.jpg?raw=true)
-   Now let’s look at the "users" table using HCatalog. Click the HCat
    icon in the toolbar at the top of the page, then click **Browse
    Data** in the "users" row.

    [![](./images/tutorial-6/12_select_users_table.jpg?raw=true)](./images/tutorial-6/12_select_users_table.jpg?raw=true)
-   The "users" table appears, and you can see the SWID, birth date, and
    gender columns.

    [![](./images/tutorial-6/13_users_table.jpg?raw=true)](./images/tutorial-6/13_users_table.jpg?raw=true)
-   You can also use HCatalog to view the data in the "products" table,
    which maps product categories to website URLs.

    [![](./images/tutorial-6/14_products_table.jpg?raw=true)](./images/tutorial-6/14_products_table.jpg?raw=true)

Now let’s use a Hive script to generate an “omniture” view that contains a subset of the data in the Omniture log table. Click the Beeswax (Hive UI) icon in the toolbar at the top of the page to display the Query Editor, then paste the following text in the Query box:

	CREATE VIEW omniture AS 
	SELECT 
	  col_2 ts,
      col_8 ip,
      col_13 url,
      col_14 swid,
      col_50 city,
      col_51 country,
      col_53 state
    from omniturelogs


[![](./images/tutorial-6/15_save_script.jpg?raw=true)](./images/tutorial-6/15_save_script.jpg?raw=true)

-   Click **Save as**. On the "Choose a Name" pop-up, type “omniture” in
    the Name box, then click **Save**.

    [![](./images/tutorial-6/16_omniture_view.jpg?raw=true)](./images/tutorial-6/16_omniture_view.jpg?raw=true)
-   Click **Execute** to run the script.

    [![](./images/tutorial-6/17_execute_script.jpg?raw=true)](./images/tutorial-6/17_execute_script.jpg?raw=true)
-   To view the data generated by the saved script, click **Tables** in
    the menu at the top of the page, select the checkbox next to
    “omniture,” then click **Browse Data**.

[![](./images/tutorial-6/18_browse_omniture.jpg?raw=true)](./images/tutorial-6/18_browse_omniture.jpg?raw=true)
-   The query results will appear, and you can see that the results
    include the data from the omniturelogs table that were specified in
    the query.

[![](./images/tutorial-6/18_omniture_query_data.jpg?raw=true)](./images/tutorial-6/18_omniture_query_data.jpg?raw=true)

Finally, we’ll create a script that joins the omniture website log
    data to the CRM data (registered users) and CMS data (products).
    Click **Query Editor**, then paste the following text in the Query
    box:

    create table webloganalytics as
    
            select 
                to_date(o.ts) logdate,
                o.url,
                o.ip,
                o.city,
                upper(o.state) state,
                o.country,
                p.category,
                CAST(datediff(
                from_unixtime( unix_timestamp() ),
                from_unixtime( unix_timestamp(u.birth_dt, 'dd-MMM-yy'))) / 365  AS INT) age,
                  u.gender_cd gender
                  from 
                  omniture o 
                  inner join products p on o.url = p.url 
                  left outer join users u on o.swid = concat('{', u.swid , '}')

-   Save this script as “webloganalytics” and execute the script. You
    can view the data generated by the script as described in the
    preceding steps.

Now that you have loaded data into the Hortonworks Platform, you can use
Business Intelligence (BI) applications such as Microsoft Excel to
access and analyze the data.
