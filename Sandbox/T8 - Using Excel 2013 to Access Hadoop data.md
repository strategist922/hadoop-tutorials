## Tutorial 8: Using Excel 2013 to Access Sandbox Data

**This tutorial is from the [Hortonworks Sandbox](http://hortonworks.com/products/sandbox) - a single-node Hadoop cluster running in a virtual machine. Download to run this and other tutorials in the series.**

### Summary

This tutorial describes how to use Excel 2013 to access data in the
Hortonworks sandbox on Windows 7.

In this procedure, we will use a Microsoft Query in Microsoft Excel 2013
to access sandbox data. This procedure should also apply to other
versions of Excel. The process may not be identical in other versions of
Excel, but it should be similar.

### Prerequisites:

-   Windows 7
-   Hortonworks ODBC driver (64-bit) installed and configured
-   Hortonworks Sandbox 1.2 or later (installed and running)
-   Microsoft Excel 2013 Professional Plus 64-bit

### Overview

To access Hortonworks sandbox data with Excel 2013:

-   Use the Microsoft Query feature to access the sandbox repository.
-   Specify sandbox data to import into Excel.
-   Import the data as a spreadsheet or pivot chart.

### Using Excel 2013 to Access Sandbox Data

-   In Windows, open a new Excel workbook, then select **Data \> From
    Other Sources \> From Microsoft Query**.

    [![](./images/tutorial-8/01_open_query.jpg?raw=true)](./images/tutorial-8/01_open_query.jpg?raw=true)
-   On the Choose Data Source pop-up, select the Hortonworks ODBC data
    source you installed previously, then click **OK**.

    [![](./images/tutorial-8/02_choose_data_source.jpg?raw=true)](./images/tutorial-8/02_choose_data_source.jpg?raw=true)
-   After the connection to the sandbox is established, the Query Wizard
    appears.  Select the omniture table in the Available tables and
    columns box, then click the right arrow button to add the entire
    omniture table to the query. Click **Next** to continue.

     **Note:** You can select multiple tables and columns to add to a
    query. Use the **+** symbols to expand tables. Use the right arrow
    button to add tables and columns to a query. Use the left arrow
    buttons to remove tables and columns. The double left arrow button
    removes all tables and columns from a query.

-   On the Filter Data screen, click **Next** to continue without
    filtering the data.

     **Note:** You can use Filter Data to include column rows based on
    filtering criteria. Select a column to filter, then use the
    drop-down boxes and radio buttons to specify which rows to include.

    [![](./images/tutorial-8/04_query_wizard2.jpg?raw=true)](./images/tutorial-8/04_query_wizard2.jpg?raw=true)
-   On the Sort Order screen, click **Next** to continue without setting
    a sort order.

     **Note:** You can use Sort Order to sort the query based on column
    data in ascending or descending order.

    [![](./images/tutorial-8/05_query_wizard3.jpg?raw=true)](./images/tutorial-8/05_query_wizard3.jpg?raw=true)
-   Click **Finish** on the Query Wizard Finish screen to retrieve the
    query data from the sandbox and import it into Excel.

    [![](./images/tutorial-8/06_query_wizard4.jpg?raw=true)](./images/tutorial-8/06_query_wizard4.jpg?raw=true)
-   On the Import Data dialog box, click **OK** to accept the default
    settings and import the data as a table.

     **Note:** You can use the Import Data dialog box to import the
    query data as a pivot chart, or to specify an insertion point.

    [![](./images/tutorial-8/07_import_data.jpg?raw=true)](./images/tutorial-8/07_import_data.jpg?raw=true)
-   The imported query data appears in the Excel workbook.

    [![](./images/tutorial-8/08_data_imported.jpg?raw=true)](./images/tutorial-8/08_data_imported.jpg?raw=true)

Now that you have successfully imported sandbox data into Microsoft
Excel, you can use the features in Excel to analyze the data.