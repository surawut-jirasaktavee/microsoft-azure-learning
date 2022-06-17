# INTRODUCTION TO DATA FACTORY
---

## What is Azure Data Factory?

On this day on big data we have a lot of type of data:
- Raw data
- Organized data
- Unorganized data

Which ofthen stored in relational, non-relational and other storage systems. raw data doesn't have
-the proper context or meaning to provide meaningful insights to:
- Data analysts
- Data scientists
- Business decision makers

Big data requires a service that can orchestrate and operationalize processes to refine these enormouse
-stores of raw data into actionable business insights. Azure Data Factory is managed cloud service that's
built for these complex hybrid extract-transform-load(ETL), extract-load-transform(ELT), and data integration projects.

## How does it work?

Data Factory contains a series of interconnected systems that provide a complete end-to-end platform for
data engineers.

![CodeFree ETL as a service](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/introduction%20to%20Data%20Factory/images/overview.svg)

## Connect and collect

In the enterprises level, they have data of various types that are located in disparate sources:
- On-premises
- Cloud

And various data types such as:
- Structure
- Unstructure
- Semmi-structure

The first step in building an information productionn system is to connect to all the required sources of
data and processing:
- Software-as-a-service(SaaS)
- databases
- file shares
- FTP web services

The next step is to move the data as needed to a centralized location for subsequent processing.

**Without Data Factory**, Enterprises need to cusdom data movement components or write custom services to intregrate these data sources and processing. So it's hard and maybe cannot possible to do it for the full syetem.

**With Data Factory**, The [`Copy Activity`](https://docs.microsoft.com/en-us/azure/data-factory/copy-activity-overview) in a data pipeline can help to move data from both on-premises and cloud source data 
stores to a centralization data store in the cloud for further analysis.

## Transform and enrich

For this process after data is present in a centralized data store in the cloud already, Using `ADF mapping data flows` can enable data engineers to build and maintain data transformation graphs that execute on Spark without needing to understand Spart clusters or Spark programing. But we still can code to make transformation by hand and executing on compute sevices such as:
- HDInsight Hadoop
- Spark
- Data Lake Analytics
- Machine Learning

## CI/CD and publish

[Data Factory offers support for CI/CD](https://docs.microsoft.com/en-us/azure/data-factory/continuous-integration-delivery) of you data pipeline using:
- Azure DevOps
- Git Hubs

resources: [Azure CI/CD](https://azure.microsoft.com/en-us/services/devops/#overview)

So you can incrementally develop and deliver your ETL processes before publishing the finished product.

## Monitor

Azure Data Factory has buid in-support for pipeline monitoring via:
- [Azure Monitor](https://docs.microsoft.com/en-us/azure/azure-monitor/overview)
- [API](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/rest-api-walkthrough)
- [PowerShell](https://docs.microsoft.com/en-us/powershell/module/az.monitor/?view=azps-8.0.0)
- [Azure Monitor logs](https://docs.microsoft.com/en-us/azure/azure-monitor/logs/data-platform-logs)
- [Health panels on the Azure portal](https://azure.microsoft.com/en-us/features/service-health/)


## Top-level concepts

Azure Data Factory is composed of below key components.
- Pipelines
- Activites
- Datasets
- Linked services
- Data Flows
- Integration Runtimes

These components work together to provide the platform on which you can compose data-driven workflows with steps to move and transform data.

### Pipeline

1. A Data Factory might have one or more pipelines. 
2. A pipeline is a logical grouping of activies that performs a unit of work.
3. The activities in a pipeline perform a task.

We perform these three things together. The activiteis in a pipeline can be chained together to operate
sequentially, or they can operate independently in parallel.
- Sequentially
- Parallel

### Mapping data flows

The mapping data flows allow you to create and manage graphs of data transformation logic that you can; - - Transform any-sized data
- Build-up a reuseable library as routines
- Execute those process in a scaled-out manner from ADF pipelines
- Execute on Spark cluster that spins-up and down when you need it.

### Activity

Activities represent a processing step in a pipeline.
- Data movement activities
- Data transformation activities
- Control flow activities

resources for [`Azure Activities`](https://docs.microsoft.com/en-us/azure/data-factory/concepts-pipelines-activities?tabs=data-factory)

### Dataset

Datasets represent data structures within the data stores, which simply point to or reference the data you want to use in your activities as inputs or outputs.

### Linked services

Linked services are much like `Connection Strings`, which define the connection information that's needed for Data Factory to connect to external resources.

Linked services are used for two purposes in Data Factory.
- [**Data store** ](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/data-store-overview)
- [**Compute resource**](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)

### Integration Runtime

The Integration runtime provides the bridge between the activity and linked services by provides the compute environment where the activity either runs on or gets dispatched from.

This way, the activity can be performed in the region closest possible to the target data store or compute service in the most performant way while meeting security and compliance needs.

### Triggers

[**Triggers**](https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?tabs=csharp) represent the unit of processing that determines when a pipeline execution needs to be kicked off. There are different types of triggers for different types of events.

### Pipeline runs

A pipeline run is an instance of the pipeline execution. Pipeline runs are typically instantiated by passing the arguments to the parameters that are defined in pipelines. The arguments can be passed manually or within the trigger definition.

### Parameters

1. Parameters are the key-value pairs of read-only configuration.
2. Parameters are defined in the pipeline.
3. The arguments for the defined parameters are pass during execution from the run context.
4. The trigger or pipeline will execute the run context.
5. The Activites within the pipeline consume the parameter values

A dataset is a strongly typed parameter and a reusable/referenceable entity. An activity can reference datasets and can consume the properties that are defined in the dataset definition.

A linked service is also a strongly typed parameter that contains the connection information to either a data store or a compute environment. It is also a reusable/referenceable entity.

### Control flow

An orchestration of pipeline activities that can chaining activities in a sequence, branching, defined parameters at the pipeline level. it's still can pass the arguments while invoking the pipeline on-demand or from a trigger.

### Variables

Variables can be used inside of pipelines to store temporary values and can also be used in conjunction with parameters to enable passing values between pipelines, data flows, and other activities.

