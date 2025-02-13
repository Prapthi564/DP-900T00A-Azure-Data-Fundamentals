# Lab 04: Explore data analytics in Azure with Azure Synapse Analytics

## Lab scenario

In this lab, you'll use the already provisioned Azure Synapse Analytics workspace in your Azure subscription, to ingest and query data.

## Lab objectives

In this lab, you will perform the following tasks:

+ Task 1: Explore an Azure Synapse Analytics workspace
+ Task 2: Ingest data
+ Task 3: Use a SQL pool to analyze data
+ Task 4: Use a Spark pool to analyze data
  
## Estimated timing: 30 minutes

## Architecture diagram

![](images/dp900lab4.png)  

## Exercise 1: Provision an Azure Synapse Analytics workspace

In this exercise, you'll use the Azure Synapse Analytics workspace to ingest and analyze some data.

The exercise is designed to familiarize you with some key elements of a modern data warehousing solution, not as a comprehensive guide to performing advanced data analysis with Azure Synapse Analytics. 

### Task 1: Explore an Azure Synapse Analytics workspace

1. In the Azure portal, on the **Home** page, use the **&#65291; Create a resource** icon to create a new resource.

    ![](images/dp1.png)

1. Search for **Azure Synapse Analytics (1)** and select **Azure Synapse Analytics (2)**.

    ![](images/dp4-1.png)

1. Create a new **Azure Synapse Analytics** resource with the following settings and click  **Create**.
    
    - Subscription: **Leave default Sybscription (1)**
    - Resource group: Select **DP-900-Module-4-<inject key="DeploymentID" enableCopy="false"/> (2)**
    - Managed resource group: Leave Blank **(3)**
    - Workspace name: Enter **synapse-<inject key="DeploymentID" enableCopy="false"/> (4)**
    - Region: **Central US (5)**
    - Select Data Lake Storage Gen 2: **From subscription (6)**
    - Account name: Click on **Create new**, then enter **datalake<inject key="DeploymentID" enableCopy="false"/> (7)**
    - File system name: Click on **Create new**, then enter **fs<inject key="DeploymentID" enableCopy="false"/> (8)**
    - Select **Review+Create (9)**

      ![](images/dp4-3.png)    

       > **Note**: A Synapse Analytics workspace requires two resource groups in your Azure subscription; one for resources you explicitly create, and another for managed resources used by the service. It also requires a Data Lake storage account in which to store data, scripts, and other artifacts.
    
1. Then select **Create** to create the workspace.

1. Wait for the workspace to be created - this may take five minutes or so.

1. When deployment is complete, click on **Go to resource group** to go to the resource group that was created.

1. Notice that it contains your **Synapse Analytics workspace** and a **Data Lake storage account**.

    ![](images/dp4-4.png)

1. Select your Synapse workspace **synapse-<inject key="DeploymentID" enableCopy="false"/>**.

    ![](images/dp4-6.png)

1. On the **Overview (1)**  page, in  **Open Synapse Studio (2)**  card, select  **Open (3)**  to open Synapse Studio in a new browser tab. 

    ![](images/dp4-5.png)
    
     >**Note:** Synapse Studio is a web-based interface that you can use to work with your Synapse Analytics workspace.

1. On the left side of Synapse Studio, use the  **››**  icon to expand the menu - this reveals the different pages within Synapse Studio that you'll use to manage resources and perform data analytics tasks, as shown here:
    
    ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-7.png)

### Task 2 : Ingest data

One of the key tasks you can perform with Azure Synapse Analytics is to define  _pipelines_  that transfer (and if necessary, transform) data from a wide range of sources into your workspace for analysis.

1. In Synapse Studio, on the **Home** page, select **Ingest** to open the **Copy Data tool** tool.

    ![](images/dp4-8.png)
    
1. In the Copy Data tool, on the  **Properties**  step, ensure that  **Built-in copy task (1)**  and  **Run once now (2)**  are selected, and click  **Next > (3)**.

    ![](images/dp4-9.png)
    
1. On the  **Source**  step, in the  **Dataset**  substep, select the following settings and click  **Create**.
     
    - **Source type**: **All (1)**
    - **Connection**:  Create a new connection by selecting **+ New Connection (2)**.
    
      ![](images/dp4-11.png)

    - In the **New connection** pane that appears, on the **Generic protocol (1)** tab, select **HTTP (2)** and then **continue (3)**.
    
      ![](images/dp4-10.png)

    - Create a **New connection** to a data file using the following settings:
        - **Name**: **AdventureWorks Products (1)**
        - **Description**: **Product list via HTTP (2)**
        - **Connect via integration runtime**: **AutoResolveIntegrationRuntime (3)**
        - **Base URL**:  `https://raw.githubusercontent.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/master/Azure-Synapse/products.csv` **(4)**
        - **Server Certificate Validation**: **Enable (5)**
        - **Authentication type**: **Anonymous (6)**
        - Click on **Create (7)**

          ![](images/dp4-12.png)

1. After creating the connection, on the  **Source/ Dataset**  substep, ensure the following settings are selected, and then select  **Next >**:

    - **Relative URL**:  Leave blank
    - **Request method**: GET
    - **Additional headers**:  Leave blank
    - **Binary copy**:  Unselected
    - **Request timeout**:  Leave blank
    - **Max concurrent connections**:  Leave blank

1. On the  **Source**  step, in the  **Configuration**  substep, select  **Preview data**  to see a preview of the product data your pipeline will ingest, then close the preview.

    >**Note:** **Preview data** may take some time to enable. 

    ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-13.png)

    ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-14.png)    
    
1. After previewing the data, on the  **Source/Configuration**  step, ensure the following settings are selected, and then select  **Next > (6)**:

    - File format: **DelimitedText (1)**
    - Column delimiter: **Comma (,) (2)**
    - Row delimiter: **Line feed (\n) (3)**
    - First row as header: **Selected (4)**
    - Compression type: **No compression (5)**

      ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-15.png) 

1. On the  **Destination**  step, in the  **Dataset**  substep, select the following settings, and select **Create**:
    
    - Destination type: **Azure Data Lake Storage Gen 2** 
    - Connection:  _Create a new connection by selecting **+ New Connection** with the following properties:
        - Name: **Products (1)**
        - Description: **Product list (2)**
        - Connect via integration runtime: **AutoResolveIntegrationRuntime (3)**
        - Authentication method: **Account key (4)**
        - Account selection method: **From azure subscription (5)**
            - Azure subscription: **Select your subscription (6)**
            - Storage account name:  Select your storage account named **datalake<inject key="DeploymentID" enableCopy="false"/> (7)**
        - Test connection: **To linked service (8)**
        - Click on **Create (9)**

          ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-16.png)        

1. After creating the connection, on the  **Destination/Dataset**  step, ensure the following settings are selected, and then select  **Next >**:
    
    - **Folder path**:  Click on **Browse** to your file system folder and select **fs<inject key="DeploymentID" enableCopy="false"/>** then select **Ok**
    - **File name**: products.csv
    - **Copy behavior**: Leave blank
    - **Max concurrent connections**:  Leave blank
    - **Block size (MB)**:  Leave blank

1. On the  **Destination/Configuration**  step, ensure that the following properties are selected. Then select  **Next >**:
    
    - **File format**: DelimitedText
    - **Column delimiter**: Comma (,)
    - **Row delimiter**: Line feed (\n)
    - **Add header to file**: Selected
    - **Compression type**: No compression
    - **Max rows per file**:  Leave blank
    - **File name prefix**:  Leave blank

1. On the  **Settings**  step, enter the following settings and then click  **Next >**:

     - **Task name**: Copy products
     - **Task description**: Copy products data
     - **Fault tolerance**: Leave blank
     - **Enable logging**: Unselected
     - **Enable staging**: Unselected

1. On the  **Review and finish**  step, on the  **Review**  substep, read the summary and then click  **Next >**.
    
1. On the  **Deployment**  step, wait for the pipeline to be deployed and then click  **Finish**.

    ![](images/dp4-17.png)
    
1. In Synapse Studio, select the  **Monitor (1)**  page, and in the  **Pipeline runs (2)**  tab, wait for the  **Copy products**  pipeline to complete with a status of  **Succeeded (3)**  (you can use the  **↻ Refresh**  button on the Pipeline runs page to refresh the status).

    ![](images/dp4-18.png)
    
1. Navigat to **Data (1)**  page from the left navigation pane, select the  **Linked (2)**  tab and expand the  **Azure Data Lake Storage Gen 2 (3)**  hierarchy until you see the file storage for your Synapse workspace. Then select the file storage **fs<inject key="DeploymentID" enableCopy="false"/> (4)** to verify that a file named  **products.csv (5)**  has been copied to this location, as shown here:
    
     ![Image showing Synapse Studio expanded Azure Data Lake Storage Gen 2 hierarchy with the file storage for your Synapse workspace](images/dp4-20.png)

  >**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

   <validation step="f63ac60a-1265-47c2-8043-4b696ac5ffbf" />     
    

### Task 3 : Use a SQL pool to analyze data

Now that you've ingested some data into your workspace, you can use Synapse Analytics to query and analyze it. One of the most common ways to query data is to use SQL, and in Synapse Analytics you can use a  _SQL pool_  to run SQL code.

1. In Synapse Studio, right-click the  **products.csv (1)**  file in the file storage for your Synapse workspace, point to  **New SQL script (2)**, and select  **Select TOP 100 rows (3)**.

    ![](images/dp4-21.png)
    
1. In the  **SQL Script 1**  pane that opens, review the SQL code that has been generated, which should be similar to this:
    

    
    ```SQL
    -- This is auto-generated code
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0'
        ) AS [result]
    
    ```
    
    This code opens a rowset from the text file you imported and retrieves the first 100 rows of data.
    
1. In the  **Connect to**  list, ensure  **Built-in**  is selected - this represents the built-in SQL Pool that was created with your workspace.

    ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-22.png)
    
1. On the toolbar, use the  **▷ Run**  button to run the SQL code, and review the results, which should look similar to this:
    
    ![](images/dp4-23.png)

1. Note the results consist of four columns named `C1, C2, C3, and C4` and that the first row in the results contains the names of the data fields. To fix this problem, add a **HEADER_ROW = TRUE** parameters to the OPENROWSET function as shown here (replacing  _datalakexx_  with **datalake<inject key="DeploymentID" enableCopy="false"/>** and  _fsxx_  with **fs<inject key="DeploymentID" enableCopy="false"/>** the names of your data lake storage account and file system), and then rerun the query:

    ```SQL
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0',
            HEADER_ROW = TRUE
        ) AS [result]
    ```

    Now the results look like this:

    ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-23.png)

     >**Note:** Please ignore the warnings in code.
 
1. Modify the query as follows (replacing  `datalakexx`  with **datalake<inject key="DeploymentID" enableCopy="false"/>** and  `fsxx`  with **fs<inject key="DeploymentID" enableCopy="false"/>** the names of your data lake storage account and file system):
    

    ```SQL
    SELECT
        Category, COUNT(*) AS ProductCount
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0',
            HEADER_ROW = TRUE
        ) AS [result]
    GROUP BY Category;
    ```
   
1. **Run** the modified query, which should return a resultset that contains the number products in each category, like this:
    
    ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](images/dp4-26.png)

     >**Note:** Please ignore the warnings in code.
     
1. In the  **Properties**  pane for  **SQL Script 1**, change the  **Name**  to  **Count Products by Category (1)**. Then in the toolbar, select  **Publish (2)**  to save the script.

    ![](images/dp4-27.png)
    
1.  Close the  **Count Products by Category**  script pane.
    
1. In Synapse Studio, select the  **Develop (1)**  page, and notice that your published  **Count Products by Category (2)**  SQL script has been saved there.

    ![](images/dp4-28.png)
    
1. Select the  **Count Products by Category (1)**  SQL script to reopen it. Then ensure that the script is connected to the  **Built-in (2)**  SQL pool and **Run (3)** it to retrieve the product counts.

    ![](images/dp4-29.png)
    
1. In the  **Results (1)**  pane, select the  **Chart (2)**  view, and then select the following settings for the chart **(3)**:
    
     - **Chart type**: Column
     - **Category column**: Category
     - **Legend (series) columns**: ProductCount
     - **Legend position**: bottom - center
     - **Legend (series) label**:  Leave blank
     - **Legend (series) minimum value**: Leave blank
     - **Legend (series) maximum**:  Leave blank
     - **Category label**:  Leave blank
    
     The resulting chart should resemble this **(4)**:
    
     ![Image showing the product count chart view](images/dp4-31.png)
    

### Task 4 : Use a Spark pool to analyze data

While SQL is a common language for querying structured datasets, many data analysts find languages like Python useful to explore and prepare data for analysis. In Azure Synapse Analytics, you can run Python (and other) code in a  _Spark pool_; which uses a distributed data processing engine based on Apache Spark.

1. In Synapse Studio, select the **Manage** page.

1. Select the **Apache Spark pools** tab, and then use the **&#65291; New** icon to create a new Spark pool with the following settings:

    ![](images/dp4-32.png)

    - **Apache Spark pool name**: Enter **spark<inject key="DeploymentID" enableCopy="false"/> (1)**
    - **Node size family**: **Memory Optimized (2)**
    - **Node size**: **Small (4 vCores / 32 GB) (3)**
    - **Autoscale**: **Enabled (4)**
    - **Number of nodes**: **3----3 (5)**
    - Click on **Reviw+create (6)**

      ![](images/dp4-33.png)    

1. Then click on **Create**, then wait for it to deploy (which may take a few minutes).

1. When the Spark pool has been deployed, in Synapse Studio, on the **Data (1)** page, navigate to **Linked (2)** tab then browse to the file system **fs<inject key="DeploymentID" enableCopy="false"/> (3)** for your Synapse workspace. Then right-click **products.csv (4)**, point to **New notebook (5)**, and select **Load to DataFrame (6)**.

    ![](images/dp4-34.png)

1. In the **Notebook 1** pane that opens, in the **Attach to** list, select the ****spark<inject key="DeploymentID" enableCopy="false"/> (1)** Spark pool to created previously and ensure that the **Language** is set to **PySpark (Python) (2)**.

1. Review the code in the first (and only) cell in the notebook, which should look like this: **(3)**

    ```Python
    %%pyspark
    df = spark.read.load('abfss://fsxx@datalakexx.dfs.core.windows.net/products.csv', format='csv'
    ## If header exists uncomment line below
    ##, header=True
    )
    display(df.limit(10))
    
    ```

    ![](images/dp4-35.png)

1. Use the  **▷ (1)**  icon to the left of the code cell to run it, and wait for the results. The first time you run a cell in a notebook, the Spark pool is started - so it may take a minute or so to return any results.
    
    > **Note**: 
    If an error occurs because the Python Kernel isn't available yet, run the cell again.

1. Eventually, the results should appear below the cell, and they should be similar to this: **(2)**
    
    ![Image showing the product count chart view](images/dp4-36.png)
    
1. Uncomment the  **header=True**  line (because the products.csv file has the column headers in the first line), so your code looks like this:
    
   
    ```Python
    %%pyspark
    df = spark.read.load('abfss://fsxx@datalakexx.dfs.core.windows.net/products.csv', format='csv'
    ## If header exists uncomment line below
    , header=True
    )
    display(df.limit(10))
    
    ```
    >**Note**: Modify the query as follows (replacing  _fsxx_ with **fs<inject key="DeploymentID" enableCopy="false"/>** and _datalakexx_ with **datalake<inject key="DeploymentID" enableCopy="false"/>** the names of your data lake storage account and file system):

1. **Rerun** the cell and verify that the results look like this:
    
    ![Image showing the product count chart view](images/dp4-37.png)
    
    > Notice that running the cell again takes less time, because the Spark pool is already started.
    
1.  Under the results, use the  **＋ Code**  icon to add a new code cell to the notebook.
    
1.  In the new empty code cell, add the following code **(1)**:

    ```Python
    df_counts = df.groupby(df.Category).count()
    display(df_counts)
    ```
    
1.  Run the new code cell by clicking its  **▷ (2)**  icon, and review the results **(3)**, which should look similar to this:

       ![Image showing category count chart view](images/dp4-38.png) 
     
1.  In the results output for the cell, select the  **Chart**  view. The resulting chart should resemble this:
    
     ![Image showing category count chart view](images/dp4-40.png)
    
1.  Close the  **Notebook 1**  pane and discard your changes.

     >**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
    > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
    > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
    > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

   <validation step="659a2fac-2657-4dee-bf66-e9eb3ddba059" />

## Review
In this lab, you have completed:
- Explore an Azure Synapse Analytics workspace
- Ingest data
- Use a SQL pool to analyze data
- Use a Spark pool to analyze data
  
## You have successfully completed this lab
