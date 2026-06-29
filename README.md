# Azure Data Factory ETL Pipeline

## Overview

This project implements an end-to-end ETL pipeline using **Azure Data Factory (ADF)** and **Mapping Data Flows** to process CSV files stored in Azure Storage.

The pipeline automatically detects source files, processes only the required files, applies transformations through an ADF Mapping Data Flow, and writes the transformed data into a destination sink.

---

## Architecture

```text
Azure Storage (CSV Files)
          │
          ▼
   Get Metadata
          │
          ▼
      ForEach Loop
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
          ▼
      Destination Sink
```

---

# Pipeline Workflow

The pipeline performs the following operations:

1. Reads the source folder using **Get Metadata**.
2. Retrieves the list of available CSV files.
3. Iterates through each file using a **ForEach** activity.
4. Uses an **If Condition** to determine whether the current file should be processed.
5. Copies the selected CSV file into the processing location.
6. Executes a Mapping Data Flow to transform the data.
7. Writes the transformed data into the configured sink dataset.

---

## Pipeline Design

<img width="1916" height="909" alt="image" src="https://github.com/user-attachments/assets/c8f7cb42-9258-46e6-baee-78051169c868" />

---

## Individual Copy Pipeline

The Copy Data activity is responsible for moving the selected CSV file before transformation.

**Features**

- Reads CSV source
- Parameterized dataset
- Reusable Copy Activity
- Used by the main orchestration pipeline

![Copy Pipeline](images/copy_pipeline.png)

---

# Mapping Data Flow

The Mapping Data Flow performs multiple transformations on the copied CSV file.

The transformations include:

- Selecting required columns
- Filtering records
- Conditional branching based on payment type
- Aggregating customer-level information
- Creating derived columns
- Altering output columns
- Writing transformed data to the sink

---

## Data Flow Design

<img width="1920" height="633" alt="image" src="https://github.com/user-attachments/assets/5d34e636-1d56-4e93-a078-95dcab421264" />

---

# Data Flow Steps

### 1. Source

Reads the input CSV dataset.

---

### 2. Select

Keeps only the required columns and renames columns where necessary.

---

### 3. Filter

Filters rows using conditions on the dataset.

---

### 4. Conditional Split

Splits incoming records into multiple streams based on payment type.

Visible branches include:

- Visa
- MasterCard
- AmEx

---

### 5. Aggregate

Groups customer records and produces aggregated values.

---

### 6. Derived Column

Creates or updates output columns.

---

### 7. Alter Row

Applies row-level actions before writing to the destination.

---

### 8. Sink

Exports the transformed dataset into the configured sink.

---

# Technologies Used

- Azure Data Factory
- Azure Mapping Data Flow
- Azure Blob Storage / ADLS (CSV datasets)
- Copy Activity
- Get Metadata Activity
- ForEach Activity
- If Condition Activity
- Parameterized Datasets

---

# Pipeline Features

- Dynamic file discovery
- Parameterized datasets
- Automated iteration using ForEach
- Conditional file processing
- Reusable Copy Activity
- Mapping Data Flow transformations
- End-to-end ETL workflow

---

# Repository Structure

```
.
├── pipeline/
│   ├── OnlySelectedFiles
│   ├── pipelinemanager
│
├── dataflow/
│   └── transform_csv
│
├── dataset/
│   ├── param_source_csv
│   ├── reporting_sink
│
└── README.md
```

---

# Sample Execution

The execution flow:

```
Get Metadata
      │
      ▼
ForEach
      │
      ▼
If File Matches
      │
      ▼
Copy CSV
      │
      ▼
Transform Data
      │
      ▼
Sink
```

---

# Result

The pipeline successfully:

- Discovers CSV files
- Processes only matching files
- Copies the selected source file
- Performs data transformations
- Loads the transformed data into the destination
