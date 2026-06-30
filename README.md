# Azure Data Factory ETL Pipeline

## Overview

This project demonstrates an end-to-end ETL pipeline built using **Azure Data Factory (ADF)**. It automates the ingestion, validation, transformation, and loading of CSV files stored in Azure Data Lake using parameterized pipelines and Mapping Data Flows.

The implementation follows a production-style workflow that dynamically discovers source files, processes only the required files, performs data transformations, and loads the processed data into a reporting dataset.

---

## Project Workflow

The pipeline consists of the following stages:

1. **Get Metadata**
   - Retrieves the list of files from the source folder.
   - Enables dynamic processing without hardcoding filenames.

2. **ForEach Activity**
   - Iterates through every discovered file.
   - Passes the current filename to downstream activities.

3. **If Condition**
   - Validates whether the filename matches the required pattern (for example, files beginning with `fact`).
   - Prevents unnecessary processing of unrelated files.

4. **Copy Activity**
   - Copies the selected CSV file using a parameterized dataset.
   - Demonstrates reusable pipeline design.

5. **Mapping Data Flow**
   - Applies graphical Spark-based transformations, including:
     - Selecting required columns
     - Filtering records
     - Conditional Split based on payment type
     - Aggregate transformation
     - Derived Columns
     - Alter Row transformation
     - Writing the transformed data to the sink

---

## Features

- Dynamic file discovery using **Get Metadata**
- Automated file iteration using **ForEach**
- Conditional file validation using **If Condition**
- Parameterized source datasets
- Dynamic filename handling
- Copy Activity for reusable ingestion
- Mapping Data Flow transformations
- End-to-end orchestration within Azure Data Factory
- Debugging and monitoring through ADF

---

## Azure Services Used

- Azure Data Factory
- Azure Data Lake Storage Gen2
- Azure Mapping Data Flow
- Azure Integration Runtime

---

## Data Flow

```text
Azure Data Lake
       │
       ▼
Get Metadata
       │
       ▼
ForEach
       │
       ▼
If Condition
       │
       ▼
Copy Activity
       │
       ▼
Mapping Data Flow
       │
       ├── Select
       ├── Filter
       ├── Conditional Split
       ├── Aggregate
       ├── Derived Column
       ├── Alter Row
       ▼
Destination Sink
```

---

## Pipeline Screenshots

### Main Pipeline

<img width="1873" height="876" alt="image" src="https://github.com/user-attachments/assets/38d4cde0-c295-49f1-bae9-f653cfa10ace" />

---

### Copy Activity Pipeline

<img width="1920" height="718" alt="image" src="https://github.com/user-attachments/assets/cf610325-6994-42e1-af0c-db014bff21f4" />

---

### Mapping Data Flow

<img width="1918" height="617" alt="image" src="https://github.com/user-attachments/assets/ba7bf1ba-aa10-45aa-a260-d486bc76043a" />


---

## Skills Demonstrated

- Azure Data Factory Pipeline Development
- ETL Pipeline Design
- Dynamic Pipeline Parameterization
- Mapping Data Flows
- Azure Data Lake Integration
- Conditional Workflow Automation
- File Metadata Processing
- Pipeline Debugging and Monitoring

---

## Learning Outcomes

Through this project, I gained practical experience with:

- Building reusable ADF pipelines
- Processing files dynamically using metadata
- Implementing conditional execution and looping
- Designing graphical data transformation pipelines
- Parameterizing datasets and activities
- Executing and monitoring production-style ETL workflows

- Discovers CSV files
- Processes only matching files
- Copies the selected source file
- Performs data transformations
- Loads the transformed data into the destination
