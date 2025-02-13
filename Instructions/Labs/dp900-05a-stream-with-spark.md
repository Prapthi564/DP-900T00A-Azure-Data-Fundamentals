# Lab 05a: Explore Spark Streaming in Azure Synapse Analytics

## Lab scenario 
In this lab, you'll use *Spark Structured Streaming* and *delta tables* in Azure Synapse Analytics to process streaming data.

## Lab objectives

In this lab, you will perform the following tasks:

+ Task 1: Create a Synapse Analytics workspace
+ Task 2: Create a Spark pool
+ Task 3: Explore stream processing
  
## Estimated timing: 15 minutes

## Architecture diagram

![](images/dp900module(5a).png)

## Exercise 1: Provision a Synapse Analytics workspace and Spark Pool

### Task 1: Create a Synapse Analytics workspace
    
1. In the Azure portal, on the **Home** page, use the **&#65291; Create a resource** icon to create a new resource.

    ![](images/dp1.png)

1. Search for **Azure Synapse Analytics (1)** and select **Azure Synapse Analytics (2)**.

    ![](images/dp4-1.png)

1. On the **Azure Synapse Analytics** page, click on **Create (1)** drop down and then click on **Azure Synapse Analytics (2)**.

    ![](images/dp4-2.png)

1. Create a new **Azure Synapse Analytics** resource with the following settings:
    - **Subscription**: *Your Azure subscription*
    - **Resource group**: *Select existing resource group,  **DP-900-Module-5-<inject key="DeploymentID" enableCopy="false"/>**
    - **Workspace name**: Enter **synapse-ws-<inject key="DeploymentID" enableCopy="false"/>**
    - **Region**: *Select any available location*.
    - **Select Data Lake Storage Gen 2**: From subscription
    - **Account name**: *Create a new account with a unique name, for example "datalake<inject key="DeploymentID" enableCopy="false"/>"*.
    - **File system name**: *Create a new file system with a unique name, for example "fs<inject key="DeploymentID" enableCopy="false"/>"*.
    
    ![](images/DP900_lab5a_1.png)
    
1. When you've entered these details, select **Review + create**, and then select **Create** to create the workspace.

1. Wait for the workspace to be created - this may take five minutes or so.

1. When deployment is complete, go to the resource group that was created and notice that it contains your Synapse Analytics workspace and a Data Lake storage account.
   
1.  Select your Synapse workspace, and in its  **Overview**  page, scroll down to the  **Open Synapse Studio**  card, select  **Open**  to open Synapse Studio in a new browser tab. Synapse Studio is a web-based interface that you can use to work with your Synapse Analytics workspace.
    
1.  On the left side of Synapse Studio, use the  **››**  icon to expand the menu - this reveals the different pages within Synapse Studio that you'll use to manage resources and perform data analytics tasks, as shown here:
    
    ![Synapse Studio](images/synapse-studio1.png)
    
 
 ### Task 2: Create a Spark pool

To use Spark to process streaming data, you need to add a Spark pool to your Azure Synapse workspace.

1. In Synapse Studio, select the **Manage** page.

1. Select the **Apache Spark pools** tab, and then use the **&#65291; New** icon to create a new Spark pool with the following settings:
    - **Apache Spark pool name**: "sparkpool<inject key="DeploymentID" enableCopy="false"/>"
    - **Node size family**: Memory Optimized
    - **Node size**: Small (4 vCores / 32 GB)
    - **Autoscale**: Enabled
    - **Number of nodes** 3----3
1. Review and create the Spark pool, and then wait for it to be deployed (which may take a few minutes).
   
   ![](images/DP900_lab5a_2.png)

### Task 3: Explore stream processing

To explore stream processing with Spark, you'll use a notebook that contains Python code and notes to help you perform some basic stream processing with Spark Structured Streaming and delta tables.

1. Download the [Structured Streaming and Delta Tables.ipynb](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/Spark%20Structured%20Streaming%20and%20Delta%20Tables.ipynb) notebook to the lab (if the notebook is opened as a text file in your browser, save it to a local folder then open the downloaded file in **File Explorer** then click on **View** check the box of **File name extensions** then rename it as **Structured Streaming and Delta Tables.ipynb** if .txt extension is there remove it)

1. In Synapse Studio, select the **Develop** page.

1. On the **&#65291;** menu, select **&#8612; Import**, and select the **Structured Streaming and Delta Tables.ipynb** file in the file explorer.

1. Follow the instructions in the notebook to attach it to your Spark pool and run the code cells it contains to explore various ways to use Spark for stream processing.

  >**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

   <validation step="fd970f3e-885a-419d-98cd-434ceda7621e" />

## Review
In this lab, you have completed:
- Create a Synapse Analytics workspace
- Create a Spark pool
- Explore stream processing
  
## You have successfully completed this lab

