# Lab 5c: Explore real-time analytics in Microsoft Fabric

## Lab scenario

In this lab, you will explore the process of working with event-driven data in Microsoft Fabric. You will start by setting up a workspace and then progress through the creation and management of eventstreams and eventhouses, which are central to capturing and storing event data. As you move through the lab, you will query the data captured in the eventhouse for insights. Finally, you will clean up your environment by removing the workspace, ensuring that all resources are properly decommissioned.

## Lab Objective

In this lab, you will perform:

+ Task 1: Create the workspace
+ Task 2: Create an eventstream
+ Task 3: Create an eventhouse
+ Task 4: Query the captured data
+ Task 5: Remove the workspace


## Estimated timing: 30 minutes

## Architecture diagram

![](images/5c.png)

### Task 1: Create the workspace

In this task, you will create a workspace in Microsoft Fabric with the Fabric trial enabled. This workspace will serve as the central environment for managing your eventstreams, eventhouses, and other resources required for event-driven data processing.

1. Navigate to [Microsft fabric](https://app.powerbi.com/) in the LabVM browser.

1. If prompted, in the Power BI tab, provide the **Email/Username: <inject key="AzureAdUserEmail"></inject>(1)** and select **Submit (2)**.

    ![The Power BI Desktop start screen](images/dp6-1.png)

1. Complete the sign in process by clicking on **Continue**.

    ![The Power BI Desktop start screen](images/dp6-2.png)

1. If prompted, provide the **Job title** as **xxxx (1)**, **Business phone number** as some random 10 digits **(2)** and then **Get Started (3)**.

    ![The Power BI Desktop start screen](images/dp6-3.png)

1. Click on **Get Started**.

    ![The Power BI Desktop start screen](images/dp6-4.png)

1. Select **Account manager (1)**, and click on **Free trial (2)**.

    ![The Power BI Desktop start screen](images/dp4b-1.png)    

1. Upgrade to a free Microsoft Fabric trial dialog opens. Select **Activate**.

    ![The Power BI Desktop start screen](images/dp4b-2.png)       

1. Select **Fabric Home Page**.

    ![The Power BI Desktop start screen](images/dp4b-3.png)    

1. In the menu bar on the left, select **Workspaces (1)** (the icon looks similar to **🗇**). Select **+ New Workspace (2)**.

    ![The Power BI Desktop start screen](images/dp4b-4.png)    
   
1. Create a new workspace **Fabricworkspace<inject key="DeploymentID" enableCopy="false"/> (1)**. Expand **Advanced** then select **Trail (2)** Licence mode and then click on **Apply (3)**.

    ![The Power BI Desktop start screen](images/dp4b-5.png)   

    ![The Power BI Desktop start screen](images/dp4b-6.png)         

1. When your new workspace opens, it should be empty.

### Task 2: Create an eventstream

In this task, you will create an eventstream in Microsoft Fabric to ingest real-time data from a streaming source. 

> **Tip**: The first time you use the Real-Time Hub, some *getting started* tips may be displayed. You can close these.

1. In the menu bar on the left, select the **Real-Time (1)** hub. In the real-time hub, in the **Connect to** section, select **Data sources (2)**. Find the **Yellow taxi (3)** sample data source and select **Connect (4)**. 

    ![Screenshot of a new eventstream.](./images/dp5bc-2.png)

1. Then in the **Connect** wizard, name the source `taxi` **(1)** and **edit** the default eventstream name to change it to `taxi-data` **(2)**. The default stream associated with this data will automatically be named *taxi-data-stream* **(3)** and then select **Next (4)**.

    ![Screenshot of a new eventstream.](./images/dp5c-3.png)

1. Wait for the source and eventstream to be created, click on **Connect**.

    ![Screenshot of a new eventstream.](./images/dp5c-4.png)

1. Then select **Open eventstream**.

   ![Screenshot of the eventstream canvas.](./images/dp5c-5.png)

1. The eventstream will show the **taxi** source and the **taxi-data-stream** on the design canvas:

   ![Screenshot of the eventstream canvas.](./images/dp5bc-5.png)


### Task 3: Create an eventhouse

In this task, you will create an eventhouse to store the real-time stock data captured by the eventstream. 

1. On the menu bar on the left, click on **elipsis(...)(1)** select **Create (2)**.

    ![Screenshot of the eventstream canvas.](./images/dp5c-6.png)

1. In the *New* page, scroll down under the *Real-Time Inteligence* section, select **Eventhouse**. 

    ![Screenshot of the eventstream canvas.](./images/dp5c-7.png)

1. Give it a unique name as **Eventhouse<inject key="DeploymentID" enableCopy="false"/> (1)** and the click **Create (2)**.

    ![Screenshot of the eventstream canvas.](./images/dp5c-8.png)

1. Click on **Get started** pop up.

    ![Screenshot of a new eventhouse](./images/dp5c-9.png)

1. In the pane on the left, note that your eventhouse contains a **KQL database** with the same name as the eventhouse. You can create tables for your real-time data in this database, or create additional databases as necessary.

    ![Screenshot of a new eventhouse](./images/dp5c-10.png)

1. Select the database, and note that there is an associated **queryset**. This file contains some sample KQL queries that you can use to get started querying the tables in your database.

    ![Screenshot of a new eventhouse](./images/dp5c-11.png)

    However, currently there are no tables to query. Let's resolve that problem by getting data from the eventstream into a new table.

1. In the main page of your KQL database, select **Get data**.

    ![Screenshot of a new eventhouse](./images/dp5bc-12.png)

1. For the data source, select **Eventstream (1)** > **Existing eventstream (2)**.

    ![Screenshot of a new eventhouse](./images/dp5c-13.png)

1. In the **Select or create a destination table** pane, click on **+ New table** then create a new table named `taxi`**(1)** and then click on right mark **(2)**.

    ![Screenshot of a new eventhouse](./images/dp5c-16.png)

1. Then in the **Configure the data source** pane, 

    - Workspace: **Fabricworkspace<inject key="DeploymentID" enableCopy="false"/>(1)**
    
    - Evenstream Name:  Select **taxi-data (2)** 
    
    - Data connection name: Enter **taxi-table** **(3)**.

    - Click on **Next (4)**

      ![Screenshot of configuration for loading a table from an eventstream.](./images/dp5c-15.png)

1. Click on **Finish**.

    ![Screenshot of a new eventhouse](./images/dp5c-17.png)

1. Then close the configuration window to see your eventhouse with the stock table.

    ![Screenshot of and eventhouse with a table.](./images/dp5c-18.png)

    >**Note**: The connection between the stream and the table has been created. Let's verify that in the eventstream.

1. In the menu bar on the left, select the **Real-Time (1)** hub and then view the **My data streams (2)** page. In the **... (3)** menu for the **taxi-data-stream** stream, select **Open eventstream (4)**.

    ![Screenshot an eventstream with a destination.](./images/dp5c-19.png)

1. The eventstream now shows a destination for the stream:

    ![Screenshot an eventstream with a destination.](./images/dp5c-20.png)

     > **Tip**: Select the destination on the design canvas, and if no data preview is shown beneath it, select **Refresh**.

### Task 4: Query the captured data

In this task, you will query the real-time taxi fare data that has been captured by the eventstream and stored in the KQL database within your eventhouse. 

1. In the menu bar on the left, select your eventhouse database **Eventhouse<inject key="DeploymentID" enableCopy="false"/> (1)**, select the **Eventhouse<inject key="DeploymentID" enableCopy="false"/>** database, then select the **Eventhouse<inject key="DeploymentID" enableCopy="false"/>_ queryset (2)** queryset for your database **Eventhouse<inject key="DeploymentID" enableCopy="false"/>**. In the query pane, modify the first example query as shown here: **(3)**

    ```kql
    taxi
    | take 100
    ```

1. Select the query code and **Run (4)** it to see 100 rows of data from the table and review the results **(5)**.

    ![Screenshot of a KQL query.](./images/dp5c-21.png)

1. Then modify the query to show the number of taxi pickups for each hour: **(1)** 

    ```kql
    taxi
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
   ```

1. Highlight the modified query then **Run** **(2)** it to see the results. **(3)**

     ![Screenshot of a KQL query.](./images/dp5c-22.png)  

1. Wait a few seconds and run it again, noting that the number of pickups change as new data is added to the table from the real-time stream.

### Task 5: Remove the workspace

In this task, you will remove the workspace you created in Microsoft Fabric for this exercise. Deleting the workspace ensures that all resources associated with it, such as eventstreams, eventhouses, and any data stored, are cleaned up properly, preventing unnecessary usage and costs.

1. In the bar on the left, select the icon for your workspace **Fabricworkspace<inject key="DeploymentID" enableCopy="false"/> (1)**, then click on **Workspace settings (2)**.

     ![Screenshot of a KQL query.](./images/dp5c-23.png)  

1. In the **General** section, select **Remove this workspace**.

     ![Screenshot of a KQL query.](./images/dp5c-24.png)  

1. Click on **Delete** do delete the workspace.

     ![Screenshot of a KQL query.](./images/dp5c-25.png)  


## Review

In this lab, you have completed:
- Created the workspace
- Created a eventstream
- Created a eventhouse
- Queried real-time data in a KQL database
- Removed the workspace


## You have successfully completed this lab
