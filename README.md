ADF-Databricks ETL Pipeline

Fig 1: Pipeline Architecture

<img width="1907" height="991" alt="image" src="https://github.com/user-attachments/assets/f1d00b26-fd16-467d-a631-2899a28cf21e" />

What this pipeline does:

1. Copy Data - Copies data files from the input folder to the output folder.
2. Upon Successful completion file is read by a Notebook on Databricks -> Transformation is applied, and data is saved in the  output folder in **delta** format.
   *For Databricks to read the data file stored on Azure containers, I set up storage credentials and configured **Unity catalog** to read data from external Sources.
   
4. If this Databricks activity **fails**, an email is sent with the pipeline Name and failure logs. (Implemented through Azure Logic apps)

   <img width="1456" height="319" alt="image" src="https://github.com/user-attachments/assets/f0584431-5a50-4c6c-963f-b4a928bb01e3" />

5. If this Databricks activity **succeeds**, file is deleted from source folder. 

Key Components:
**Linked Services**: These are like connection strings. They define the connection information needed for ADF to connect to external resources (e.g., "Here is the login for my SQL Database" or "Here is the key for my Blob Storage").

**Datasets**: These represent the data structures within your data stores. If a Linked Service is the connection to the library, the Dataset is the specific book you want to read (e.g., a specific table in a database or a file in a folder).

**Activities**: These are the actions performed on your data.

**Data Movement**: Copy data from Source A to Destination B.

**Data Transformation**: Run a Spark job in Databricks, run a stored procedure in SQL, etc.
Control Flow: Loops, Wait, If conditions.

**Pipelines**: A logical grouping of activities that performs a unit of work. For example, a pipeline might contain three activities: 1. Copy data from AWS S3 to Azure Blob. 2. Clean the data using Databricks. 3. Load the data into a Data Warehouse.

**Integration Runtime (IR)**: The compute infrastructure used by ADF to provide data integration capabilities. It’s the "engine" that actually executes the movement or dispatches the activities.

**Azure IR**: For cloud-to-cloud movement.

**Self-Hosted IR**: For moving data between cloud and on-premise (private) networks.

**Triggers**: The unit of processing that determines when a pipeline execution needs to be kicked off (e.g., a schedule, or when a file lands in a storage account).






