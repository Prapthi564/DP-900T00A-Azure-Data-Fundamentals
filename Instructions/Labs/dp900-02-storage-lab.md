# Lab 02: Explore Azure Storage

## Lab scenario
In this lab, you will provision an Azure Storage account and explore various storage options available in Azure. You will start by setting up an Azure Storage account, which serves as the foundation for storing different types of data. Then, you will explore Blob Storage for unstructured data, Azure Data Lake Storage Gen2 for hierarchical data management, Azure Files for cloud-based file sharing, and Azure Tables for key-value data storage. Through these tasks, you will gain hands-on experience in configuring and managing different Azure storage solutions.

## Lab Objectives

In this lab, you will perform following tasks:

+ Task 1: Provision an Azure Storage account
+ Task 2: Explore blob storage
+ Task 3: Explore Azure Data Lake Storage Gen2
+ Task 4: Explore Azure Files
+ Task 5: Explore Azure Tables
  
## Estimated timing: 30 minutes

## Architecture diagram

![](images/sc900module2.png)  

## Lab Prerequisites

Before starting this lab, you should have the following prerequisites:

  - **Azure Subscription** – An active Azure account with permissions to create and manage storage resources.
  - **Basic Storage Concepts** – Understanding of cloud storage types such as blobs, files, and tables.

## Exercise 1: Explore Azure Storage

In this exercise you'll provision an Azure Storage account in your Azure subscription, and explore the various ways you can use it to store data.

### Task 1: Provision an Azure Storage account

In this task, you will create an Azure Storage account in your Azure subscription as an initial step in working with Azure Storage.

1. On the Azure portal home page, select  **＋ Create a resource**  from the upper left-hand corner. 

    ![](images/dp2-1.png)

1. Search for **Storage account (1)** and select **Storage account (2)**.

    ![Screenshot of Azure Database for PostgreSQL deployment options](images/dp2-2.png)

1. On the **Storage account** page, click on the **Create (1)** dropdown and select **Storage account (2)**.    

    ![](images/dp2-3.png)
    
1. Enter the following values on the  **Create a storage account**  page:
    
    - Subscription: **Leave default Azure subscription (1)**
    - Resource group:Choose the existing resource group **DP-900-Module2-<inject key="DeploymentID" enableCopy="false"/> (2)**
    - Storage account name: **str<inject key="DeploymentID" enableCopy="false"/> (3)**.
    - Region: **East US (4)**.
    - Performance:  **Standard (5)**
    - Redundancy:  **Locally-redundant storage(LRS) (6)**
    - Click on **Next (7)** twice, to navigate to **Advanced** tab.

      ![](images/dp2-4.png)    

1. On the Advanced tab, make sure **enable hierarchical namespace** to support Azure Data Lake Storage Gen2 is unselected **(1)**. Then click on **Next (2)** twice to navigate to **Data protection** tab.      

    ![](images/dpm2-1.png)
  
1. On the **Data protection** tab, in the  **Recovery**  section,  deselect all of the  **Enable soft delete... (1)**  options. These options retain deleted files for subsequent recovery, but can cause issues later and then click on **Review+create (2)**.

    ![](images/dp2-5.png)
    
1. Select  **Create**  to create your Azure Storage account.
   
1.  Wait for deployment to complete. Then click on **Go to resouce** to go to the resource that was deployed.

    ![](images/dp2-6.png)
    
### Task 2 : Explore blob storage

In this task, you will create a blob container to store and manage data within your Azure Storage account.

1. Right click on the following link, https://aka.ms/product1.json, then click on **copy link** and then paste it on the browser. It will download the **product1.json** JSON file and press **Ctrl+S** to save it on your computer (you can save it in any folder - you'll upload it to blob storage later).

1. Select **Downloads (1)**, keep the file name as **product1 (2)** then make sure that **Save as type** is **JSON** and click on **Save (3)**.

    ![](images/dp2-7.png)
    
     >**Note:** If the JSON file is displayed in your browser, save the page as **product1.json**.
    
1. In the Azure portal page go to the newly created storage account for your storage container, on the left side, in the  **Data storage**  section, select  **Containers**.

    ![](images/dp2-8.png)
    
1. In the **Containers** page, select **&#65291; Container** and add a new container named **data (1)** with an anonymous access level of **Private (no anonymous access) (2)** and then click on **Create (3)**.

    ![](images/dp2-9.png)

1. When the  **data**  container has been created, verify that it's listed in the  **Containers**  page.

    ![](images/dp2-10.png)
    
1. Go back to the storage account, in the pane on the left side, in the top section, select  **Storage browser (1)**. In the storage browser page, select  **Blob containers (2)**.

    ![Screenshot of Azure Database for PostgreSQL deployment options](images/dp2-11.png)  

1. Verify that your  **data**  container is listed. Select the  **data**  container, and note that it's empty.    

    ![](images/dp2-12.png)
    
1.  Select  **＋ Add Directory**.

    ![](images/dp2-14.png)

1. Create a new directory named  **products (1)** and click on **Ok (2)**.

    ![](images/dp2-13.png)
    
1. In Storage Explorer, verify that the current view shows the contents of the  **products**  folder you just created - observe that the "breadcrumbs" at the top of the page reflect the path  **Blob containers > data > products**.

    ![](images/dp2-15.png)

1. In the breadcrumbs, select **data** to switch to the **data** container.

    ![](images/dp2-16.png)

1. Note that it does <u>not</u> contain a folder named **products**.

    ![](images/dp2-17.png)

     >**Note:** Folders in blob storage are virtual, and only exist as part of the path of a blob. Since the **products** folder contained no blobs, it isn't really there!
      
1. Use the  **⤒ Upload**  button to open the  **Upload blob**  panel.

    ![](images/dp2-18.png)
    
1. In the  **Upload blob**  panel, select the **Browse for files (1)**, navigate to **Downloads (2)** then select **product1.json (3)** file you saved on your local computer previously and then click on **Open (4)**. 

    ![](images/dp2-19.png)

1. Then expand **Advanced (1)**  section, in the  **Upload to folder**  box, enter  **product_data (2)**  and select the  **Upload (3)**  button.

    ![](images/dp2-20.png)
    
1. Close the  **Upload blob**  panel if it's still open, and verify that a  **product_data**  virtual folder has been created in the  **data**  container.

    ![](images/dp2-21.png)
    
1. Select the  **product_data**  folder and verify that it contains the  **product1.json**  blob you uploaded.

    ![](images/dp2-22.png)
   
1. On the left side, in the  **Data storage**  section, select  **Containers**.
    
1. Open the  **data**  container, and verify that the  **product_data**  folder you created is listed.

     ![Screenshot of Azure Database for PostgreSQL deployment options](images/dp900-mod2-cont1.1.png)
    
1. Select the  **elipses(...)**  icon at the right-end of the folder, and note that it doesn't display any options. Folders in a flat namespace blob container are virtual, and can’t be managed.

    ![](images/dp2-23.png)
    
1. Use the  **X**  icon at the top right in the  **data**  page to close the page and return to the  **Containers**  page.
    

### Task 3:  Explore Azure Data Lake Storage Gen2

In this task, you will use Azure Data Lake Store Gen2 to organize and manage access to blobs with hierarchical folders. You will also leverage Azure Blob Storage to host distributed file systems for big data analytics platforms.

1.  Download the [product2.json](https://aka.ms/product2.json?azure-portal=true)  JSON file by right click on the following link, `https://aka.ms/product2.json` then select **Copy link** and then paste it on the browser.

1. Press **Ctrl+S** to save file on your computer in the same folder where you downloaded product1.json previously - you'll upload it to blob storage later.

1. Select **Downloads (1)**, keep the file name as **product2 (2)** then make sure that **Save as type** is **JSON** and click on **Save (3)**.

    ![](images/dp2-24.png)

1. In the Azure portal page for your storage account, on the left side, scroll down to the **Settings (1)** section, and select **Data Lake Gen2 upgrade (2)**.  

    ![](images/dpm2-2.png)

1. In the **Data Lake Gen2 upgrade** page, expand and complete each step to upgrade your storage account to enable hierarchical namespace and support Azure Data Lake Storage Gen 2. This may take some time.    

1. Expand **Step 1(1)**, click on **Review and agree to changes (2)** then select the acknowledge check box **(3)** and then click on **Agree to changes (4)**. 

    ![](images/dpm2-3.png)

1. Once the **Step 1** is completed, expand **Step 2 (1)** then click on **Start Validation (2)**.

    ![](images/dpm2-4.png)

     >**Note**: This may take some time. Please wait untill it is completed.

1. After **Step 2** is completed, expand **Step 3 (1)** then click on **Start Upgrade (2)**.

    ![](images/dpm2-5.png)

     >**Note**: This may take some time. Please wait untill it is completed.

1. Make sure all the steps are completed.

    ![](images/dpm2-6.png)

1. When the upgrade is complete, in the pane on the left side, in the top section, select  **Storage browser (1)**  and navigate back to the root of your  **data (2)**  blob container, which still contains the  **product_data (3)**  folder.

    ![](images/dp2-25.png)

1. Select the  **product_data**  folder, and verify it still contains the  **product1.json**  file you uploaded previously.

    ![](images/dp2-26.png)

1. Use the  **⤒ Upload**  button to open the  **Upload blob**  panel.

    ![](images/dp2-27.png)

1. In the  **Upload blob**  panel, select the  **product2.json**  file you saved on your local computer.

1. In the  **Upload blob**  panel, select the **Browse for files (1)**, select **product2.json (2)** file you saved on your local computer previously and then click on **Open (3)**. 

    ![](images/dp2-28.png)

1. Then select the  **Upload**  button.

    ![](images/dp2-29.png)

1. Close the  **Upload blob**  panel if it's still open, and verify that a  **product_data**  folder now contains the  **product2.json**  file.

    ![Screenshot of Azure Database for PostgreSQL deployment options](images/dp2-30.png) 

1. On the left side, in the  **Data storage**  section, select  **Containers**.

1. Open the  **data**  container, and verify that the  **product_data**  folder you created is listed.

1. Select the **elipsis (‧‧‧) (1)** icon at the right-end of the folder, and note that with **hierarchical namespace enabled**, you can perform configuration tasks at the folder-level; including **renaming folders and setting permissions (2)**.

    ![](images/dpm2-7.png)

1. Use the  **X**  icon at the top right in the  **data**  page to close the page and return to the  **Containers**  page.

### Task 4 :  Explore Azure Files

In this task, you will create cloud-based file shares using Azure Files.

1. In the Azure portal displaying the storage container, on the left side, in the  **Data storage (1)**  section, select  **File shares (2)**.

    ![](images/dp2-31.png)

1. In the File shares page, select  **＋ File share**.

1. Add a new file share named  **files (1)**  using the  **Transaction optimized (2)**  tier and then click on **Next: Backup > (3)** 

    ![](images/dp2-32.png)

1. Make sure that **Enable backup** is disabled **(1)**. Then select **Review + create (2)**.

    ![](images/dp2-33.png)

1. Click on **Create**.    

1. In the  **File shares (1)**, open your new  **files (2)**  share.

    ![](images/dp2-34.png)

1. At the top of the page, select  **Connect (1)**. Then in the  **Connect**  pane, note that there are tabs for common operating systems (**Windows, Linux, and macOS (2)**)  that contain scripts you can run to connect to the shared folder from a client computer.

    ![](images/dp2-35.png)

1. Close the  **Connect**  pane and then close the  **files**  page to return to the  **File shares**  page for your Azure storage account.

### Task 5 : Explore Azure Tables

In this task, you will use Azure Tables to store key-value data for applications that do not require the full functionality of a relational database.

1. In the Azure portal page for your storage container, on the left side, in the  **Data storage (1)**  section, select  **Tables (2)**.

    ![](images/dp2-36.png)
    
1. On the  **Tables**  page, select  **＋ Table (1)**. Create a new table named  **products (2)** and then click on **OK (3)**.

    ![](images/dp2-37.png)
    
1. After the  **products**  table has been created, in the pane on the left side, in the top section, select  **Storage browser**.
    
1. In storage explorer, select  **Tables**  and verify that the  **products**  table is listed.

    ![](images/dp2-38.png)
    
1. Select the  **products**  table.
    
1. In the  **product**  page, select  **＋ Add entity**.
    
1. In the  **Add entity**  panel, enter the following key values:

    |Property name | Type | Value |
    | ------------ | ---- | ----- |
    | PartitionKey **(1)** | String | 1  |
    | RowKey **(2)** | String | 1 |
    
    - Select  **Add property**, and create a new property with the following values:
    
      |Property name | Type | Value |
      | ------------ | ---- | ----- |
      | Name **(3)** | String | Widget |
    
    - Add a second property with the following values:
    
      |Property name | Type | Value |
      | ------------ | ---- | ----- |
      | Price **(4)** | Double | 2.99 |
    
1. Select  **Insert (5)**  to insert a row for the new entity into the table.

     ![Screenshot of Azure Database for PostgreSQL deployment options](images/dp2-39.png)
    
1. In storage browser, verify that a row has been added to the  **products**  table, and that a  **Timestamp**  column has been created to indicate when the row was last modified.

    ![](images/dp2-40.png)
    
1. Add another entity to the **products** table with the following properties and then click on **Insert (5)**:

    |Property name | Type | Value |
    | ------------ | ---- | ----- |
    | PartitionKey | String | 1 **(1)** |
    | RowKey | String | 2 **(2)** |
    | Name | String | Kniknak **(3)** |
    | Price | Double | 1.99 **(4)** |
    | Discontinued | Boolean | true **(5)** |

     ![](images/dp2-41.png)    

13. After inserting the new entity, verify that a row containing the **discontinued** product is shown in the table.

    ![Screenshot of Azure Database for PostgreSQL deployment options](images/dp2-42.png)
    
    >**Note**: You have manually entered data into the table using the storage browser interface. In a real scenario, application developers can use the Azure Storage Table API to build applications that read and write values to tables, making it a cost effective and scalable solution for NoSQL storage.

  >**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

   <validation step="87f78207-9b57-4997-8cc1-072577be255b" />

## Review
In this lab, you have completed:
- Provision an Azure Storage account
- Explore blob storage
- Explore Azure Data Lake Storage Gen2
- Explore Azure Files
- Explore Azure Tables
  
## You have successfully completed this lab
