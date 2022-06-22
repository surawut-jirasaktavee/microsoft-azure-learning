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

## Pipeline execution and triggers

ref: [docs.microsotf](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipeline-execution-triggers)

* A pipeline run in `Azure Data Factory` and `Azure Synapse` defines an instance of a pipeline execution.
* Each pipeline run has a unique run ID. A run ID is a GUID that uniquely definees that particular pipeline run.
* Pipeline runs are typically instantiated by passing arguments to parameters that you difine in the pipeline.
* Pipeline can either manually or by using a trigger.
**NOTE**: If `Manully trigger` the pipeline, it will execute immediately. Otherwise if choose `New/Edit`, you will be prompted with the add triggers window to either choose an existing trigger to edit, or create a new trigger.

### Manual execution (on-demand) with JSON

ref [docs.microsoft](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipeline-execution-triggers#manual-execution-on-demand-with-json)

The manual execution of a pipeline is also referred to as on-demand execution.
For example with basic pipeline `copyPipeline` the following JSON definition shows this sample pipeline

```JSON
{
    "name": "copyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "name": "CopyBlobtoBlob",
                "inputs": [
                    {
                        "referenceName": "sourceBlobDataset",
                        "type": "DatasetReference"
                    }
                ],
                "outputs": [
                    {
                        "referenceName": "sinkBlobDataset",
                        "type": "DatasetReference"
                    }
                ]
            }
        ],
        "parameters": {
            "sourceBlobContainer": {
                "type": "String"
            },
            "sinkBlobContainer": {
                "type": "String"
            }
        }
    }
}
```

In the JSON definition, the pipeline takes two parameters. **sourceBlobContainer** and **sinkBlobContainer**. You pass values to these parameters at runtime.

The method following can manually run pipeline by using:
* .NET SDK
* Azure PowerShell module
* REST API
* Python SDK

### Trigger execution with JSON

Trigger represent a unit of processing that determines when a pipeline execution needs to be kicked off.
For now the sevice supports three types of trigger.
* Schedule trigger: A trigger that invokes a pipeline on a wall-clock schedule.
* Tumbling window trigger: A trigger that operates on a periodic interval, while also retaining state.
* Event-based trigger: A trigger that responds to an event.

**Basic trigger definition**

```JSON
{
    "properties": {
        "name": "MyTrigger",
        "type": "<type of trigger>",
        "typeProperties": {...},
        "pipelines": [
            {
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "<Name of your pipeline>"
                },
                "parameters": {
                    "<parameter 1 Name>": {
                        "type": "Expression",
                        "value": "<parameter 1 Value>"
                    },
                    "<parameter 2 Name>": "<parameter 2 Value>"
                }
            }
        ]
    }
}
```

**Schedule trigger with JSON**

A schedule trigger runs pipelines on a wall-clock schedule. This trigger supports periodic and advanced calendar options. 
The schedule trigger is flexible:
* The dataset pattern in agnostic
* The trigger doesn't discern between time-series and non time-series data.
* [More information](https://docs.microsoft.com/en-us/azure/data-factory/how-to-create-schedule-trigger)

**Schedule trigger definition**
When you create a schedule trigger, you specify scheduling and recurrence by using a JSON definition.
Schedule trigger kick off a pipeline run include a pipeline reference of the particular pipeline in the trigger definition:
* Pipelines and triggers have a many-to-many relationship
* Multiple triggers can kick off a single pipeline
* A single triggle can kick off multiple pipelines
* [Schema overview](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipeline-execution-triggers#schema-overview)

```JSON
{
  "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": {
      "recurrence": {
        "frequency": <<Minute, Hour, Day, Week, Year>>,
        "interval": <<int>>, // How often to fire
        "startTime": <<datetime>>,
        "endTime": <<datetime>>,
        "timeZone": "UTC",
        "schedule": { // Optional (advanced scheduling specifics)
          "hours": [<<0-24>>],
          "weekDays": [<<Monday-Sunday>>],
          "minutes": [<<0-60>>],
          "monthDays": [<<1-31>>],
          "monthlyOccurrences": [
            {
              "day": <<Monday-Sunday>>,
              "occurrence": <<1-5>>
            }
          ]
        }
      }
    },
  "pipelines": [
    {
      "pipelineReference": {
        "type": "PipelineReference",
        "referenceName": "<Name of your pipeline>"
      },
      "parameters": {
        "<parameter 1 Name>": {
          "type": "Expression",
          "value": "<parameter 1 Value>"
        },
        "<parameter 2 Name>": "<parameter 2 Value>"
      }
    }
  ]}
}
```
**Schedule trigger example**

```JSON
{
  "properties": {
    "name": "MyTrigger",
    "type": "ScheduleTrigger",
    "typeProperties": {
      "recurrence": {
        "frequency": "Hour",
        "interval": 1,
        "startTime": "2017-11-01T09:00:00-08:00",
        "endTime": "2017-11-02T22:00:00-08:00"
      }
    },
    "pipelines": [{
        "pipelineReference": {
          "type": "PipelineReference",
          "referenceName": "SQLServerToBlobPipeline"
        },
        "parameters": {}
      },
      {
        "pipelineReference": {
          "type": "PipelineReference",
          "referenceName": "SQLServerToAzureSQLPipeline"
        },
        "parameters": {}
      }
    ]
  }
}
```

[For more information](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipeline-execution-triggers)

## Integration runtime

`The Integration Runtime(IR)` is the compute infrastructure used by `Azure Data Factory` and `Azure Synapse` pipeline to provide the following data integration capabilities across difference network environments:

* **Data Flow**: Execute a Data Flow in a managed Azure compute environment.
* **Data movement**: Copy data acros data stores in a public or private (on premises or VPN). 
* **Acitivity dispatch**: Dispatch and monitor transformation activities running on a variety of compute services such as `Azure Databricks`, `Azure HDInsignht`, `Azure SQL Database`, `SQL Service`, and more
* **SSIS package execution**: Natively execute SQL Server ingetration services(SSIS) packages in a managed Azure compute enviroment.

In `Data Factory` and `Synapse` pipeline:
- **An activity** defines the `action` to be performed.
- **A linked service** defines a target `data store` or a `compute service`.
- **An integration runtime** provides the `bridge` between `activities` and `linked services`.

It's referenced by the linked service or activity, and provides the compute environment where the activity is either run directly or dispatched. This allows the activity to be performed in the closest possible region to the target data store or compute service to maximize performance while also allowing flexibility to meet security and compliance requirements.

**Integration runtime types**

* Azure
* Self-hosted
* Azure-SSIS

The capabilities and network support for each the integration runtime types:

| **IR type** | **Public Network Support** | **Private Link Support** |
| ------------|----------------------------|--------------------------|
| Azure       | Data Flow<br>Data movement<br>Activity dispatch | Data Flow<br>Data movement<br>Activity dispatch |        
| Self-hosted | Data movement<br>Activity dispatch | Data movement<br>Activity dispatch |      
| Azure-SSI   | SSIS packages execution    | SSIS package execution   |
 
### Azure integration runtime 

An Azure integration runtime can:
* Run Data Flows in Azure
* Run copy activities between cloud data store
* Dispatch transform activites in a public network [transform activities](https://docs.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime#azure-integration-runtime)
 
**Azure IR network environment**

1. Azure Integration Runtime supports connecting to data stores and compute services with public accesible endpoints.
2. Enabling Managed Virtual Network, Azure IR supports connecting to data stores using private link service in private network environment.

**Azure IR compute resource and scaling**

Azure interration runtime provides:
* Fully managed
* Severless compute
* Secure
* Reliable
* High-performance manner
* No infrastructure provision
* No software installation
* Patching or Capacity scaling
* Only pay for the duration of actual utilization
* lightweight operation to route the activity to the target compute service

### Self-hosted integration runtime

A self-hosted IR is capable of:
* Running copy activity between a cloud data stores and a data store in private network
* Dispatching the transform activities against compute resources in on-premises or Azure Virtual Network [transform activities](https://docs.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime#self-hosted-integration-runtime)

**Self-hosted IR network environment**

The self-hosted integration runtime only makes outbound HTTP-based connections to the internet. Need to install a self-hosted IR in on-premises environment behind a firewall, or inside a virtual private network.

**Self-hosted IR compute resourec and scaling**

This self-hosted IR only supported on a Windows OS. Can install a self-hosted IR on an on-premises machine or virtual machine inside a private network.
For high availability and scalability can scale out the self-hosted IR by associatng the logical instance with multiple on-premises in active-active mode.


