## Tutorial 10: Visualizing Website Clickstream Data

**This tutorial is from the [Hortonworks Sandbox](http://hortonworks.com/products/sandbox) - a single-node Hadoop cluster running in a virtual machine. Download to run this and other tutorials in the series.**

### Summary

This tutorial describes how to refine website clickstream data using the
Hortonworks Data Platform, and how to analyze and visualize this refined
data using the Power View feature in Microsoft Excel 2013.

**Demo:** Here is the [Clickstream
video](http://www.youtube.com/watch?v=weJI6Lp9Vw0)
as a demo of what you'll be doing in this tutorial.

### Clickstream Data

Clickstream data is an information trail a user leaves behind while
visiting a website. It is typically captured in semi-structured website
log files.

These website log files contain data elements such as a date and time
stamp, the visitor’s IP address, the destination URLs of the pages
visited, and a user ID that uniquely identifies the website visitor.

### Potential Uses of Clickstream Data

One of the original uses of Hadoop at Yahoo was to store and process
their massive volume of clickstream data. Now enterprises of all types
can use Hadoop and the Hortonworks Data Platform (HDP) to refine and
analyze clickstream data. They can then answer business questions such
as:

-   What is the most efficient path for a site visitor to research a
    product, and then buy it?
-   What products do visitors tend to buy together, and what are they
    most likely to buy in the future?
-   Where should I spend resources on fixing or enhancing the user
    experience on my website?

In this tutorial, we will focus on the “path optimization” use case.
Specifically: how can we improve our website to reduce bounce rates and
improve conversion?

### Prerequisites:

-   Windows 7
-   Hortonworks ODBC driver (64-bit) installed and configured
-   Hortonworks Sandbox 1.2 or later(installed and running)
-   Hortonworks sample data files uploaded and refined as described in
    “Loading Data into the Hortonworks Sandbox”
-   Microsoft Excel 2013 Professional Plus 64-bit

### Overview

To analyze and visualize website clickstream data, we will:

-   Use Hortonworks to view and refine website clickstream data.
-   Access the clickstream data with Excel.
-   Visualize the clickstream data using Excel Power View.

## Step 1: View and Refine the Website Clickstream Data in Hortonworks

In the “Loading Data into the Hortonworks Sandbox” tutorial, we loaded
website data files into Hortonworks, and then used Hive queries to
refine the data. Let’s take a closer look at that data.

Here’s a summary of the data we’re working with:

-   **Omniture logs*** – website log files containing information such as
    URL, timestamp, IP address, geocoded IP address, and user ID (SWID).
-   **users*** – CRM user data listing SWIDs (Software User IDs) along with
    date of birth and gender.
-   **products*** – CMS data that maps product categories to website URLs.   

Let’s start by looking at the raw Omniture website data. In the
    Hortonworks Sandbox, click the File Browser icon in the toolbar at
    the top of the page, then select the `Omniture.0.tsv.gz` file.

[![](./images/tutorial-10/01_file_browser.jpg?raw=true)](./images/tutorial-10/01_file_browser.jpg?raw=true)

- The raw data file appears in the File Browser, and you can see that
    it contains information such as URL, timestamp, IP address, geocoded
    IP address, and user ID (SWID).
     The Omniture log dataset contains about 4 million rows of data,
    which represents five days of clickstream data. Often, organizations
    will process weeks, months, or even years of data.

    [![](./images/tutorial-10/02_omniturelog_raw.jpg?raw=true)](./images/tutorial-10/02_omniturelog_raw.jpg?raw=true)
-   Now let’s look at the users table using HCatalog. Click the HCat
    icon in the toolbar at the top of the page, then click **Browse
    Data** in the users row.

    [![](./images/tutorial-10/03_select_users_table.jpg?raw=true)](./images/tutorial-10/03_select_users_table.jpg?raw=true)
-   The users table appears, and you can see the SWID, birth date, and
    gender columns.

    [![](./images/tutorial-10/04_users_table.jpg?raw=true)](./images/tutorial-10/04_users_table.jpg?raw=true)
-   You can also use HCatalog to view the data in the products table,
    which maps product categories to website URLs.

    [![](./images/tutorial-10/05_products_table.jpg?raw=true)](./images/tutorial-10/05_products_table.jpg?raw=true)
-   In the “Loading Data into the Hortonworks Sandbox” tutorial, we used
    Apache Hive to join the three data sets into one master set. This is
    easily accomplished in Hadoop, even when working with millions or
    billions of rows of data.
     First, we used a Hive script to generate an “omniture” view that
    contained a subset of the data in the Omniture log table.

    [![](./images/tutorial-10/06_omniture_script.jpg?raw=true)](./images/tutorial-10/06_omniture_script.jpg?raw=true)
-   To view the omniture data in Hive, click **Table**, then click
    **Browse Data**in the omniture row.

    [![](./images/tutorial-10/07_browse_omniture.jpg?raw=true)](./images/tutorial-10/07_browse_omniture.jpg?raw=true)
-   The query results will appear, and you can see that the results
    include the data from the Omniture log table that were specified in
    the query.

    [![](./images/tutorial-10/08_omniture_query_data.jpg?raw=true)](./images/tutorial-10/08_omniture_query_data.jpg?raw=true)
-   Next, we created a “webloganalytics” script to join the omniture
    website log data to the CRM data (registered users) and CMS data
    (products). This Hive query executed a join to create a unified
    dataset across our data sources.

    [![](./images/tutorial-10/09_webloganalytics_query.jpg?raw=true)](./images/tutorial-10/09_webloganalytics_query.jpg?raw=true)
-   You can view the data generated by the webloganalytics script in
    Hive as described in the preceding steps.

    [![](./images/tutorial-10/10_webloganalytics_table.jpg?raw=true)](./images/tutorial-10/10_webloganalytics_table.jpg?raw=true)

Now that we have reviewed the refined website data, we can access the
data with Excel.

## Step 2: Access the Website Clickstream Data with Excel

In this section, we will use Excel Professional Plus 2013 to access the
refined clickstream data.

-   In Windows, open a new Excel workbook, then select **Data \> From
    Other Sources \> From Microsoft Query**.

    [![](./images/tutorial-10/11_open_query.jpg?raw=true)](./images/tutorial-10/11_open_query.jpg?raw=true)
-   On the Choose Data Source pop-up, select the Hortonworks ODBC data
    source you installed previously, then click **OK**.
     The Hortonworks ODBC driver enables you to access Hortonworks data
    with Excel and other Business Intelligence (BI) applications that
    support ODBC.

    [![](./images/tutorial-10/12_choose_data_source.jpg?raw=true)](./images/tutorial-10/12_choose_data_source.jpg?raw=true)
-   After the connection to the sandbox is established, the Query Wizard
    appears.  Select the webloganalytics table in the Available tables
    and columns box, then click the right arrow button to add the entire
    webloganalytics table to the query. Click **Next** to continue.

    [![](./images/tutorial-10/13_query_wizard1.jpg?raw=true)](./images/tutorial-10/13_query_wizard1.jpg?raw=true)
-   On the Filter Data screen, click **Next** to continue without
    filtering the data.

    [![](./images/tutorial-10/14_query_wizard2.jpg?raw=true)](./images/tutorial-10/14_query_wizard2.jpg?raw=true)
-   On the Sort Order screen, click **Next** to continue without setting
    a sort order.

    [![](./images/tutorial-10/15_query_wizard3.jpg?raw=true)](./images/tutorial-10/15_query_wizard3.jpg?raw=true)
-   Click **Finish** on the Query Wizard Finish screen to retrieve the
    query data from the sandbox and import it into Excel.

    [![](./images/tutorial-10/16_query_wizard4.jpg?raw=true)](./images/tutorial-10/16_query_wizard4.jpg?raw=true)
-   On the Import Data dialog box, click **OK** to accept the default
    settings and import the data as a table.

    [![](./images/tutorial-10/17_import_data.jpg?raw=true)](./images/tutorial-10/17_import_data.jpg?raw=true)
-   The imported query data appears in the Excel workbook.

    [![](./images/tutorial-10/18_data_imported.jpg?raw=true)](./images/tutorial-10/18_data_imported.jpg?raw=true)

Now that we have successfully imported Hortonworks Sandbox data into
Microsoft Excel, we can use the Excel Power View feature to analyze and
visualize the data.

## Step 3: Visualize the Website Clickstream Data Using Excel Power View

Data visualization can help you optimize your website and convert more
visits into sales and revenue. In this section we will:

-   Analyze the clickstream data by location
-   Filter the data by product category
-   Graph the website user data by age and gender
-   Pick a target customer segment
-   Identify a few web pages with the highest bounce rates

In the Excel workbook with the imported webloganalytics data, select
    **Insert \> Power View** to open a new Power View report.

    [![](./images/tutorial-10/19_open_powerview.jpg?raw=true)](./images/tutorial-10/19_open_powerview.jpg?raw=true)
-   The Power View Fields area appears on the right side of the window,
    with the data table displayed on the left. Drag the handles or click
    the Pop Out icon to maximize the size of the data table.

    [![](./images/tutorial-10/20_powerview_initial_popout.jpg?raw=true)](./images/tutorial-10/20_powerview_initial_popout.jpg?raw=true)
-   Let’s start by taking a look at the countries of origin of our
    website visitors. In the Power View Fields area, leave the
    **country** checkbox selected, and clear all of the other
    checkboxes. The data table will update to reflect the selections.

    [![](./images/tutorial-10/21_country_selected.jpg?raw=true)](./images/tutorial-10/21_country_selected.jpg?raw=true)
-   On the Design tab in the top menu, click **Map**.

    [![](./images/tutorial-10/22_open_map.jpg?raw=true)](./images/tutorial-10/22_open_map.jpg?raw=true)
-   The map view displays a global view of the data. Now let’s take a
    look at a count of IP address by state. First, drag the **ip** field
    into the SIZE box.

    [![](./images/tutorial-10/23_add_ip_count.jpg?raw=true)](./images/tutorial-10/23_add_ip_count.jpg?raw=true)
-   Drag **country** from the Power View Fields area into the Filters
    area, then select the **usa** checkbox.

    [![](./images/tutorial-10/24_filter_by_usa.jpg?raw=true)](./images/tutorial-10/24_filter_by_usa.jpg?raw=true)
-   Next, drag **state** into the LOCATIONS box. Remove the **country**
    field from the LOCATIONS box by clicking the down-arrow and then
    **Remove Field**.

    [![](./images/tutorial-10/25_state_to_locations.jpg?raw=true)](./images/tutorial-10/25_state_to_locations.jpg?raw=true)
-   Use the map controls to zoom in on the United States. Move the
    pointer over each state to display the IP count for that state.

    [![](./images/tutorial-10/26_ip_count_by_state.jpg?raw=true)](./images/tutorial-10/26_ip_count_by_state.jpg?raw=true)
-   Our dataset includes product data, so we can display the product
    categories viewed by website visitors in each state. To display
    product categories in the map by color, drag the **category** field
    into the COLOR box.

    [![](./images/tutorial-10/27_category_by_color.jpg?raw=true)](./images/tutorial-10/27_category_by_color.jpg?raw=true)
-   The map displays the product categories by color for each state.
    Move the pointer over each state to display detailed category
    information.
     We can see that the largest number of page hits in Florida were for
    clothing, followed by shoes.

    [![](./images/tutorial-10/28_category_by_color_florida.jpg?raw=true)](./images/tutorial-10/28_category_by_color_florida.jpg?raw=true)
-   Now let’s look at the clothing data by age and gender so we can
    optimize our content for these customers. Select **Insert \> Power
    View** to open a new Power View report.

    [![](./images/tutorial-10/29_new_powerview1.jpg?raw=true)](./images/tutorial-10/29_new_powerview1.jpg?raw=true)

To set up the data, set the following fields and filters:

-   In the Power View Fields area, select **ip** and **age**. All of the
    other fields should be unselected.
-   Drag **category** from the Power View Fields area into the Filters
    area, then select the **clothing** checkbox.
-   Drag **gender** from the Power View Fields area into the Filters
    area, then select the **M** (male) checkbox.

After setting these fields and filters, select **Column Chart \>
Clustered Column**in the top menu.

[![](./images/tutorial-10/30_open_clustered_column1.jpg?raw=true)](./images/tutorial-10/30_open_clustered_column1.jpg?raw=true)

-   To finish setting up the chart, drag **age** into the AXIS box.
    Also, remove **ip** from the AXIS box by clicking the down-arrow and
    then **Remove Field**. The chart shows that the majority of men shopping for clothing on
    our website are between the ages of 22 and 30. With this
    information, we can optimize our content for this market segment.

    [![](./images/tutorial-10/31_clothing_by_age.jpg?raw=true)](./images/tutorial-10/31_clothing_by_age.jpg?raw=true)
-   Let’s assume that our data includes information about website pages
    (URLs) with high bounce rates. A page is considered to have a high
    bounce rate if it is the last page a user visited before leaving the
    website. By filtering this URL data by our target age group, we can
    find out exactly which website pages we should optimize for this
    market segment.
     Select **Insert \> Power View** to open a new Power View report.

    [![](./images/tutorial-10/32_new_powerview2.jpg?raw=true)](./images/tutorial-10/32_new_powerview2.jpg?raw=true)

To set up the data, set the following fields and filters:

-   Drag **age** from the Power View Fields area into the Filters area,
    then drag the sliders to set the age range from 22 to 30. 
-   Drag **gender** from the Power View Fields area into the Filters
    area, then select the **M** (male) checkbox.
-   Drag **country** from the Power View Fields area into the Filters
    area, then select the **usa** checkbox.
-   In the Power View Fields area, select **url**. All of the other
    fields should be unselected.
-   In the Power View Fields area, move the pointer over **url**, click
    the down-arrow, and then select **Add to Table as Count.  **

After setting these fields and filters, select **Column Chart \>
Clustered Column** in the top menu.

[![](./images/tutorial-10/33_open_clustered_column2.jpg?raw=true)](./images/tutorial-10/33_open_clustered_column2.jpg?raw=true)

-   The chart shows that we should focus on optimizing four of our
    website pages for the market segment of men between the ages of 22
    and 30. Now we can redesign these four pages and test the new
    designs based on our target demographic, thereby reducing the bounce
    rate and increasing customer retention and sales.

    [![](./images/tutorial-10/34_urls_for_age_group.jpg?raw=true)](./images/tutorial-10/34_urls_for_age_group.jpg?raw=true)
-   You can use the controls in the upper left corner of the map to sort
    by Count of URL in ascending order.

    [![](./images/tutorial-10/35_urls_for_age_group_sorted.jpg?raw=true)](./images/tutorial-10/35_urls_for_age_group_sorted.jpg?raw=true)

Now that you have successfully analyzed and visualized Hortonworks
Sandbox data with Microsoft Excel, you can see how Excel and other BI
tools can be used with the Hortonworks platform to derive insights about
customers from various data sources.

The data in the Hortonworks platform can be refreshed frequently and
used for basket analysis, A/B testing, personalized product
recommendations, and other sales optimization activities.