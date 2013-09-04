## Tutorial 7: Installing and Configuring the Hortonworks ODBC driver on Windows 7

**This tutorial is from the [Hortonworks Sandbox](http://hortonworks.com/products/sandbox) - a single-node Hadoop cluster running in a virtual machine. Download to run this and other tutorials in the series.**

### Summary

This tutorial describes how to install and configure the Hortonworks
ODBC driver on Windows 7.

The Hortonworks ODBC driver enables you to access data in the
Hortonworks Data Platform from Business Intelligence (BI) applications
such as Microsoft Excel, Tableau, Click View, Micro Strategy, Cognos,
and Business Objects.

### Prerequisites:

-   Windows 7
-   Hortonworks Sandbox 1.2 (installed and running)

### Overview

The Hortonworks ODBC driver installation consists of the following
steps:

-   Download and install the Hortonworks ODBC driver.
-   Configure the ODBC connection in Windows 7.

### Step 1: Download and Install the Hortonworks ODBC Driver

-   In Windows 7, open a web browser and navigate to
    [http://hortonworks.com/download/](http://hortonworks.com/download/).
    Click the **Add-Ons** link at the bottom of the Hortonworks Data
    Platform 1.2 box.

    [![](./images/tutorial-7/01_download_page.jpg?raw=true)](./images/tutorial-7/01_download_page.jpg?raw=true)
-   On the Add-Ons page, scroll down to Hortonworks Hive ODBC Driver
    (Windows + Mac) and select the driver that matches the version of
    Excel installed on your system (32-bit or 64-bit). For this
    tutorial, we will configure for Excel 2013 64-bit, so we’ll select
    **Windows 64-bit (msi)**.

    [![](./images/tutorial-7/02_addons_page.jpg?raw=true)](./images/tutorial-7/02_addons_page.jpg?raw=true)
-   Review the Hortonworks license, then click **Accept Agreement**.

    [![](./images/tutorial-7/03_license_agreement.jpg?raw=true)](./images/tutorial-7/03_license_agreement.jpg?raw=true)
-   To start the download, click **Save File** on the pop-up message.

    [![](./images/tutorial-7/04_save_file.jpg?raw=true)](./images/tutorial-7/04_save_file.jpg?raw=true)
-   After the download is complete, double-click to open the downloaded
    HortonworksHiveODBC64.msi file, then click **Run** on the pop-up
    security message to open the setup wizard.

    [![](./images/tutorial-7/05_run_install.jpg?raw=true)](./images/tutorial-7/05_run_install.jpg?raw=true)
-   To start the installation, click **Next** on the Hortonworks Hive
    ODBC Driver Setup Wizard Welcome screen.

    [![](./images/tutorial-7/06_install_wizard1.jpg?raw=true)](./images/tutorial-7/06_install_wizard1.jpg?raw=true)
-   Review the license agreement, then select the checkbox to accept the
    license terms. Click **Next** to continue.

    [![](./images/tutorial-7/07_install_wizard2.jpg?raw=true)](./images/tutorial-7/07_install_wizard2.jpg?raw=true)
-   Click **Next** to accept the default installation folder.

    You can also type in a different location, or click **Change** to
    select a different installation folder using a file browser.

    [![](./images/tutorial-7/08_install_wizard3.jpg?raw=true)](./images/tutorial-7/08_install_wizard3.jpg?raw=true)

-   To begin the installation, click **Install**.

    [![](./images/tutorial-7/09_install_wizard4.jpg?raw=true)](./images/tutorial-7/09_install_wizard4.jpg?raw=true)
-   If a reboot is required, a pop-up message will appear. Click **OK**
    to continue.

    [![](./images/tutorial-7/10_install_wizard5.jpg?raw=true)](./images/tutorial-7/10_install_wizard5.jpg?raw=true)
-   When the installation is complete, the setup wizard displays a
    confirmation message. Click **Finish** to close the setup wizard.

    [![](./images/tutorial-7/11_install_wizard6.jpg?raw=true)](./images/tutorial-7/11_install_wizard6.jpg?raw=true)
-   A pop-up message will appear. Close any open applications, then
    click **Yes** to restart your system.

    [![](./images/tutorial-7/12_confirm_reboot.jpg?raw=true)](./images/tutorial-7/12_confirm_reboot.jpg?raw=true)

Now that you have successfully installed the Hortonworks ODBC driver,
the next step is to configure the driver. 

### Step 2: Configure the Hortonworks ODBC Driver

-   In the Windows Control Panel, select **Administrative Tools**, then
    double-click **Data Sources (ODBC)** to open the ODBC Data Source
    Administrator.

    [![](./images/tutorial-7/14_system_dsn.jpg?raw=true)](./images/tutorial-7/14_system_dsn.jpg?raw=true)
-   Select the **System DSN** tab. The Sample Hortonworks Hive DSN
    should be selected by default; if not, select it. Click
    **Configure** to continue.

    [![](./images/tutorial-7/13_data_source_admin.jpg?raw=true)](./images/tutorial-7/13_data_source_admin.jpg?raw=true)
-   On the Hortonworks Hive ODBC Driver DSN Setup window, type in the
    settings as shown in the image below. Type the IP address of the
    Hortonworks sandbox in the Host box. The Authentication mechanism
    should be set to User Name, and the sandbox user name should be
    entered in the User Name box (in this case the default user name,
    “sandbox”).

**Notes**

-   The sandbox IP address is displayed in the command prompt window
    after the sandbox VM (Virtual Machine) starts, and also appears in
    the browser address box when you open the sandbox.
-   If you are running more than one VM, the last number of the IP
    address may vary depending on the order in which the sandbox VM was
    started relative to the other VMs. In this example, the sandbox VM
    was started first, and its IP address is 198.168.56.101. If the
    sandbox VM had been started second (after another VM), its IP
    address would then be 198.168.56.102.
-   The IP address provided in this tutorial is an example – your IP
    address may be different. Be sure to check the sandbox command
    prompt window after starting the VM for the IP address used for your
    sandbox installation.

    [![](./images/tutorial-7/15_driver_setup.jpg?raw=true)](./images/tutorial-7/15_driver_setup.jpg?raw=true)
-   Click **Test** to test the configuration settings. If the test is
    successful, a confirmation message appears. Click **OK** to close
    the message box.

    [![](./images/tutorial-7/16_driver_test.jpg?raw=true)](./images/tutorial-7/16_driver_test.jpg?raw=true)
-   On the Hortonworks Hive ODBC Driver DSN Setup window, click **OK**
    to save the driver configuration settings.

    [![](./images/tutorial-7/17_close_setup.jpg?raw=true)](./images/tutorial-7/17_close_setup.jpg?raw=true)
-   Click **OK** to close the ODBC Data Source Administrator window.

    [![](./images/tutorial-7/18_close_dsn.jpg?raw=true)](./images/tutorial-7/18_close_dsn.jpg?raw=true)

Now that you have configured the Hortonworks ODBC driver, you can enable
ODBC connections in BI tools such as Microsoft Excel, then use those
applications to access data in the Hortonworks Platform.
