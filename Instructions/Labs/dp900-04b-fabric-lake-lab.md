# Module 04b: Explore data analytics in Microsoft Fabric

## Lab scenario
In this lab, you'll explore data ingestion and analytics in a Microsoft Fabric Lakehouse.

## Lab Objectives

In this lab, you will perform:

+ Task 1: Create the workspace
+ Task 2: Create a lakehouse
+ Task 3: Ingest data
+ Task 4: Query data in a lakehouse
+ Task 5: Visualize data in a lakehouse

## Estimated Timing: 25 minutes

## Architecture diagram

 ![](images/4b.png)  

## Task 1: Create the workspace

Before working with data in Fabric, create a workspace with the Fabric trial enabled.

1. In the menu bar, at the bottom left, switch to the **Data Engineering** experience.

     ![Screenshot of the experience switcher menu.](./images/DP-900-dataengineering.png)

1. In the menu bar on the left, select Workspaces (the icon looks similar to 🗇). Select +New Workspace.
   
1. Create a new workspace **Fabricworkspace<inject key="DeploymentID" enableCopy="false"/>**.

1. When your new workspace opens, it should be empty.

   ![](images//workspace.png)

   >**Note:** The first time you use any Microsoft Fabric features, prompts with tips may appear. Dismiss these.

## Create a lakehouse

Now that you have a workspace, it's time to create a data lakehouse for your data files.

1. In the **Data engineering** home page, select **Lakehouse(Preview)**. On the **New Lakehouse** page, enter the name of your choice, and select **Create**.

   ![Screenshot of a new lakehouse.](./images/DP-900-lakehouse.png)

3. View the new lakehouse, and note that the **Lakehouse explorer** pane on the left enables you to browse tables and files in the lakehouse:
    
    - The **Tables** folder contains tables that you can query using SQL. Tables in a Microsoft Fabric lakehouse are based on the open source *Delta Lake* file format, commonly used in Apache Spark.
    
    - The **Files** folder contains data files in the OneLake storage for the lakehouse that aren't associated with managed delta tables. You can also create *shortcuts* in this folder to reference data that is stored externally.
    
      >**Note:** Currently, there are no tables or files in the lakehouse.

  >**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

   <validation step="edbc75e2-8634-4dbb-9a62-f9c74b4a9849" />

## Task 3: Ingest data

A simple way to ingest data is to use a **Copy Data** activity in a pipeline to extract the data from a source and copy it to a file in the lakehouse.

1. On the **Home** page for your lakehouse, select **Get data** drop-down, select **New data pipeline**, and create a new data pipeline named **Ingest Data**.

1. In the **Copy Data into Lakehouse** wizard, on the **Choose a data source** page, select the **Sample data** and then select the **NYC Taxi - Green**.
   
   ![Screenshot of a new lakehouse.](./images/choose-data-source.png)

1. On the **Connect to data source** page, view the tables in the data source. There should be one table that contains details of taxi trips in New York City. Then select **Next** to progress to the **Choose data destination** page.

1. On the **Choose data destination** page, select your existing lakehouse. Then select **Next**.

1. Set the following data destination options, and then select **Next**:
    - **Root folder**: Tables
    - **Load settings**: Load to new table
    - **Destination table name**: taxi_rides *(You may need to wait for the column mappings preview to be displayed before you can change this)*
    - **Column mappings**: *Leave the default mappings as-it-is*
    - **Enable partition**: *Unselected*

1. On the **Review + save** page, ensure that the **Start data transfer immediately** option is selected, and then select **Save + Run**.

    A new pipeline containing a **Copy Data** activity is created, as shown here:

    ![Screenshot of a pipeline with a Copy Data activity.](./images/DP-900-copy.png)

    >**Note:** When the pipeline starts to run, you can monitor its status in the **Output** pane under the pipeline designer. Use the **&#8635;** (*Refresh*) icon to refresh the status, and wait until it has succeeded (which may take 10 minutes or more).

1. In the hub menu bar on the left, select your lakehouse.

1. On the **Home** page, in the **Lakehouse explorer** pane, in the **...** menu for the **Tables** node, select **Refresh** and then expand **Tables** to verify that the **taxi_rides** table has been created.

    >**Note**:If the new table is listed as *unidentified*, use its **Refresh** menu option to refresh the view.
    
1. Select the **taxi_rides** table to view its contents.

## Task 4: Query data in a lakehouse

Now that you have ingested data into a table in the lakehouse, you can use SQL to query it.

1. At the top right of the Lakehouse page, switch from **Lakehouse** view to the **SQL analytics endpoint** for your lakehouse.

1. In the toolbar, select **New SQL query**. Then enter the following SQL code into the query editor:

    ```sql
    SELECT  DATENAME(dw,lpepPickupDatetime) AS Day,
            AVG(tripDistance) As AvgDistance
    FROM taxi_rides
    GROUP BY DATENAME(dw,lpepPickupDatetime)
    ```

1. Select the **&#9655; Run** button to run the query and review the results, which should include the average trip distance for each day of the week.

    ![Screenshot of a SQL query.](./images/sql-query.png)

## Task 5: Visualize data in a lakehouse

Microsoft Fabric lakehouses organize all tables in a semantic data model, which you can use to create visualizations and reports.

1. At the bottom left of the page, under the **Explorer** pane, select the **Model** tab to see the data model for the tables in the lakehouse (this includes system tables as well as the **taxi_rides** table).
1. In the toolbar, select **New report** to create a new report based on the **taxi_rides**.
   
1. In the report designer:
    1. In the **Data** pane, expand the **taxi_rides** table and select the **lpepPickupDatetime** and **passengerCount** fields.
    1. In the **Visualizations** pane, select the **Line chart** visualization. Then ensure that the **X-axis** contains the **lpepPickupDatetime** field and the **Y** axis contains **Sum of passengerCount**.
       
        ![Screenshot of a Power BI report.](./images/fabric-report.png)

    **Tip**: You can use the **>>** icons to hide the report designer panes in order to see the report more clearly.

1. On the **File** menu, select **Save** to save the report as **Taxi Rides Report** in your Fabric workspace.

    You can now close the browser tab containing the report to return to your lakehouse.  You can find the report in the page for your workspace in the Microsoft Fabric portal.

  >**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

   <validation step="b016c5bb-cccd-4821-9464-697aa7036d09" />

## Review
In this lab, you have completed:
- Create the workspace
- Created a lakehouse
- Ingested data
- Queried data in a lakehouse
- Visualized data in a lakehouse
  
## You have successfully completed this lab
