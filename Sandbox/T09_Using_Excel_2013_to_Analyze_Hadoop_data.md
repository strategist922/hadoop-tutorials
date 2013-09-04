## Tutorial 9: Using Excel 2013 to Analyze Sandbox Data

**This tutorial is from the [Hortonworks Sandbox](http://hortonworks.com/products/sandbox) - a single-node Hadoop cluster running in a virtual machine. Download to run this and other tutorials in the series.**

### Summary

This tutorial describes how to use Excel 2013 to analyze data in the
Hortonworks sandbox on Windows 7.

In this procedure, we will use a Microsoft Query in Microsoft Excel 2013
to access sandbox data, and then analyze the data using the Excel Power
View feature.

The data we will load and analyze represents a fictitious web retail
store in what has become an established use case for Hadoop: deriving
insights from large data sources such as web logs. By combining web logs
with more traditional customer data, we can better understand our
customers, and also understand how to optimize future promotions and
advertising.

### Prerequisites:

-   Windows 7
-   Hortonworks ODBC driver (64-bit) installed and configured
-   Hortonworks Sandbox 1.2 or later (installed and running)
-   Hortonworks sample data files uploaded and refined as described in
    “Loading Data into the Hortonworks Sandbox”
-   Microsoft Excel 2013 Professional Plus 64-bit

### Overview

To analyze Hortonworks sandbox data with Excel 2013:

-   Use the Microsoft Query feature to access Hortonworks sandbox data.
-   Use the Excel Power View feature to analyze the data.

### Step 1: Use a Microsoft Query to Access Sandbox Data

-   In Windows, open a new Excel workbook, then select **Data \> From
    Other Sources \> From Microsoft Query**.

    [![](./images/tutorial-9/01_open_query.jpg?raw=true)](./images/tutorial-9/01_open_query.jpg?raw=true)
-   On the Choose Data Source pop-up, select the Hortonworks ODBC data
    source you installed previously, then click **OK**.

    [![](./images/tutorial-9/02_choose_data_source.jpg?raw=true)](./images/tutorial-9/02_choose_data_source.jpg?raw=true)
-   After the connection to the sandbox is established, the Query Wizard
    appears.  Select the webloganalytics table in the Available tables
    and columns box, then click the right arrow button to add the entire
    webloganalytics table to the query. Click **Next** to continue.

    [![](./images/tutorial-9/03_query_wizard1.jpg?raw=true)](./images/tutorial-9/03_query_wizard1.jpg?raw=true)
-   On the Filter Data screen, click **Next** to continue without
    filtering the data.

    [![](./images/tutorial-9/04_query_wizard2.jpg?raw=true)](./images/tutorial-9/04_query_wizard2.jpg?raw=true)
-   On the Sort Order screen, click **Next** to continue without setting
    a sort order.

    [![](./images/tutorial-9/05_query_wizard3.jpg?raw=true)](./images/tutorial-9/05_query_wizard3.jpg?raw=true)
-   Click **Finish** on the Query Wizard Finish screen to retrieve the
    query data from the sandbox and import it into Excel.

    [![](./images/tutorial-9/06_query_wizard4.jpg?raw=true)](./images/tutorial-9/06_query_wizard4.jpg?raw=true)
-   On the Import Data dialog box, click **OK** to accept the default
    settings and import the data as a table.

    [![](./images/tutorial-9/07_import_data.jpg?raw=true)](./images/tutorial-9/07_import_data.jpg?raw=true)
-   The imported query data appears in the Excel workbook.

    [![](./images/tutorial-9/08_data_imported.jpg?raw=true)](./images/tutorial-9/08_data_imported.jpg?raw=true)

Now that you have successfully imported sandbox data into Microsoft
Excel, you can use the Excel Power View feature to analyze the data.

### Step 2: Use a Microsoft Query to Access Sandbox Data

-   In the Excel workbook with the imported webloganalytics data, select
    **Insert \> Power View**.

    [![](./images/tutorial-9/09_open_powerview.jpg?raw=true)](./images/tutorial-9/09_open_powerview.jpg?raw=true)
-   The Power View Fields area appears on the right side of the window,
    with the data table displayed on the left. Drag the handles to
    maximize the size of the data table, and close the Filters area.

    [![](./images/tutorial-9/10_powerview_initial.jpg?raw=true)](./images/tutorial-9/10_powerview_initial.jpg?raw=true)
-   Let’s start by taking a look at a count of IP address by country. In
    the Power View area, select the **ip** and **country** checkboxes,
    and clear all of the other checkboxes. The data table will update to
    reflect the selections.

    [![](./images/tutorial-9/11_country_and_ip.jpg?raw=true)](./images/tutorial-9/11_country_and_ip.jpg?raw=true)
-   Under Fields, click the arrow next to **ip**, then select **Count
    (Not Blank)**.

    [![](./images/tutorial-9/12_ip_count_notblank.jpg?raw=true)](./images/tutorial-9/12_ip_count_notblank.jpg?raw=true)
-   On the Design tab in the top menu, click **Map**.

    [![](./images/tutorial-9/13_open_map.jpg?raw=true)](./images/tutorial-9/13_open_map.jpg?raw=true)
-   The map view displays a global view of the data. To view the data by
    state, drag and drop the **state** field into the Locations box just
    above **country**.

    [![](./images/tutorial-9/14_map_by_state.jpg?raw=true)](./images/tutorial-9/14_map_by_state.jpg?raw=true)
-   Use the map controls to zoom in on the United States.

    [![](./images/tutorial-9/15_ip_by_state.jpg?raw=true)](./images/tutorial-9/15_ip_by_state.jpg?raw=true)
-   To display categories in the map by color, drag and drop the
    **category** field into the Color box.

    [![](./images/tutorial-9/16_category_by_color.jpg?raw=true)](./images/tutorial-9/16_category_by_color.jpg?raw=true)
-   The map displays the categories by color for each state. Move the
    pointer over each state to display detailed category information. In
    the image below, we see that the largest category in Florida is
    clothing.

    [![](./images/tutorial-9/17_category_color_florida.jpg?raw=true)](./images/tutorial-9/17_category_color_florida.jpg?raw=true)
-   Now let’s look at a count of IP address by age. In the top menu,
    click **Power View**to open a new Power View Report. In the Power
    View area, select the **ip** and **age** checkboxes, and clear all
    of the other checkboxes. Under Fields, click the arrow next to
    **ip**, then select **Count (Not Blank)**.

    [![](./images/tutorial-9/18_ip_by_age.jpg?raw=true)](./images/tutorial-9/18_ip_by_age.jpg?raw=true)
-   Let’s display this data in a column chart. On the top menu, select
    **Column Chart \> Stacked Column**.

    [![](./images/tutorial-9/19_open_column_chart.jpg?raw=true)](./images/tutorial-9/19_open_column_chart.jpg?raw=true)
-   From the data in the column chart, we can see that our target
    demographic is people who are between 20 and 30 years old.

    [![](./images/tutorial-9/20_ip_by_age_chart.jpg?raw=true)](./images/tutorial-9/20_ip_by_age_chart.jpg?raw=true)

Now that you have successfully accessed and analyzed Hortonworks sandbox
data with Microsoft Excel, you can see how Excel and other BI tools can
be used with the Hortonworks platform to derive insights about customers
from various data sources.