# CONCEPTS OF DATA FACTORY
---

## Pipelines and Activities
ref: [docs.microsoft](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipelines-activities?tabs=data-factory)

**Overview**

* A `Data Factory` or `Synapse Workspace` can have one or more pipelines. 
* A `Pipeline` is a logical grouping of activities that together perform a task.
* The `Pipeline` allows to manage the activities as a set instead of each one individually.
* Deploy and schedule the pipeline instead of the activities indenpently.
* The `Activities` in a pipeline define actions to perform on the data.

### Pipeline with JSON format

```JSON
{
    "name": "PipelineName",
    "properties":
    {
        "description": "pipeline description",
        "activities":
        [
        ],
        "parameters": {
        },
        "concurrency": <your max pipeline concurrency>,
        "annotations": [
        ]
    }
}
```

**For example**:

You may use `COPY ACTIVITIES` to copy data from `SQL Server` to an `Azure Blob Storage`. Then, use a `DATA FLOW ACTIVITIES` or `DATABRICKS NOTEBOOK ACTIVITIEY` to process and transform data from the blob storage to an `Azure Synapse Analytics` pool on top of which business intelligence reporting solutions are built.

The relationship between pipeline, activity, and dataset.
![Relationship btw pipeline, activity, dataset](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/introduction%20to%20Data%20Factory/images/relationship-between-dataset-pipeline-activity.png)

* An input dataset represents the input for the activity.
* An output dataset represents the output for the activity.
* Datasets identify data within different data stores:
  * Tables
  * Files
  * Folders
  * Documents
**Note**: Must be create a dataset before use it with activities in a pipeline.

### Activity with JSON format

```JSON
{
    "name": "Execution Activity Name",
    "description": "description",
    "type": "<ActivityType>",
    "typeProperties":
    {
    },
    "linkedServiceName": "MyLinkedService",
    "policy":
    {
    },
    "dependsOn":
    {
    }
}
```

Azure Data Factory and Azure Synapse Analytics have three groupings of activities:
### Data movement activites

Copy activity in Data Factory copies data from a `source` data store to `sink` data store.
Data Factory supports the data stores listed in [this table](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipelines-activities?tabs=data-factory#data-movement-activities)

### Data transformation activities

Azure Data Factory and Azure Synapse Analytics support the following transformation activities that can be added either individually or chained with another activity.

For example:
* Data Flow
* Azure Function
* Hiv
* Spark
* Databrick
* [See more](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipelines-activities?tabs=data-factory#data-transformation-activities)

### Control flow activities

The following control flow activities are supported.
* Append Variable
* Execute Pipeline
* Filter
* [See more](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipelines-activities?tabs=data-factory#control-flow-activities)
    
        
 ## Linked services
 ref: [docs.microsoft](https://docs.microsoft.com/en-us/azure/data-factory/concepts-linked-services?tabs=data-factory)
 
* Before you create a dataset, you must create a **linked service** to link your data store to the Data Factory or Synapse Workspace. 
* `Linked services` are much like **connection strings**, which define the connection information needed for the service to connect to external resources.

The linked service defines the connection to the data source.

The following diagram shows the relationships among pipeline, activity, dataset, and linked service in the service.
![relationship btw pipeline, activity, dataset, and linked service](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/introduction%20to%20Data%20Factory/images/relationship-between-data-factory-entities.png)

### Linked service with JSON format:

```JSON
{
    "name": "<Name of the linked service>",
    "properties": {
        "type": "<Type of the linked service>",
        "typeProperties": {
              "<data store or compute-specific type properties>" //("connectionString")
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## Dataset
ref [docs.microsoft](https://docs.microsoft.com/en-us/azure/data-factory/concepts-datasets-linked-services?tabs=data-factory)

The dataset represents the structure of the data within the linked data stores

### Dataset with JSON format

```JSON
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: DelimitedText, AzureSqlTable etc...>",
        "linkedServiceName": {
                "referenceName": "<name of linked service>",
                "type": "LinkedServiceReference",
        },
        "schema":[

        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        }
    }
}
```

The service supports many different types of datasets, depending on the data stores you use:
* Arvo
* Binary
* CSV
* Excel
* JSON
* ORC
* Parquet
* XML

Find the list of supported data stores from [`Connector overview`](https://docs.microsoft.com/en-us/azure/data-factory/connector-overview)

For examlple with CSV file in **DelimitedText** format

```JSON
{
    "name": "DelimitedTextInput",
    "properties": {
        "linkedServiceName": {
            "referenceName": "AzureBlobStorage",
            "type": "LinkedServiceReference"
        },
        "annotations": [],
        "type": "DelimitedText",
        "typeProperties": {
            "location": {
                "type": "AzureBlobStorageLocation",
                "fileName": "input.log",
                "folderPath": "inputdata",
                "container": "adfgetstarted"
            },
            "columnDelimiter": ",",
            "escapeChar": "\\",
            "quoteChar": "\""
        },
        "schema": []
    }
}
```
