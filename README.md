# Az-Synapse-Mini-Project

A bootcamp mini project using Azure Synapse to create an end to end example pipeline.

## Pipeline Creation
Below is a screenshot showing the data flow created for the project. the project_instructions.pdf file shows the instructions that were followed to create the pipeline.
![A Screenshot of the Dataflow Created](dataflow.png?raw=true)

## Response to Questions

1. Why should one use Azure Key Vault when working in the Azure environment? What are the alternatives to using Azure Key Vault? What are the pros and cons of using Azure Key Vault?

    > Azure Key Vault allows for centralization of all of the secrets for an application, and allows for the use of RBAC to control access. The alternatives are to have secrets present in the code of the application, or in a configuration file. Some of the pros of using Azure Key Vault is that you can create a vault for each application in order to segregate secrets and access to only what is required. Azure Key Vault is not ideal for use in applications outside of Azure.

2. How do you achieve the loop functionality within an Azure Data Factory pipeline? Why would you need to use this functionality in a data pipeline?

    > The ForEach and Until activities allows you to achieve loop functionality in a Data Factory pipeline. ForEach can take an input array as the output of another activity, or as a pre-defined array variable. While the Until activity uses a logical condition to evaluate when to stop looping. A few examples would be to perform a copy action from a list of paths to a single output or from a single path to a list of output paths. Multiple activities can be looped over by creating a separate pipeline, and calling that pipeline in the looping activity.

3. What are expressions in Azure Data Factory? How are they helpful when designing a data pipeline (please explain with an example)?

    > Expressions are json values that can either specify a literal, or use the pipeline parameters as inputs using the @ symbol. An easy example would be to append a date to the end of a filename as shown below:
    ``` json
    "filename" : "@concat('Pipeline_output_', FormatDateTime(utcnow(), 'YYYY-MM-DD'))"
    ```
4. What are the pros and cons of parametrizing a dataset in Azure Data Factory pipeline’s activity?

    > The pros of paratetrizing a dataset in ADF is that it can eliminate the duplication of work, and allow for easier management of datasets. By parametrizing a dataset, you can make your pipelines less verbose, as some fo the important information is stored in the parameter, and not in the title.

5. What are the different supported file formats and compression codecs in Azure Data Factory? When will you use a Parquet file over an ORC file? Why would you choose an AVRO file format over a Parquet file format?

    > The supported file formats for the copy activity are as follows: delimited data, Excel format, XML format, JSON format, Binary format, Avro format, ORC format, and Parquet format. Supported compression codecs vary based on the file format being used, the supported codecs for Avro, ORC, and Parquet are shown in the table below. I would use a Parquet format over an ORC format if I were ingesting a file already in this format, or sending data externally as it is a more widely used format than ORC. I would also use Parquet format for analytical workloads that require complex querying. I would use AVRO if I were in need of an evolving schema, since schema data is stored with the data, changes to the schema are easily recognized, and older files are still able to be interperated by applications. [^1]


    |  | Supported Formats |
    |---|---|
    | **Avro** | "none", "deflate" and "snappy" |
    | **Parquet** | "none", "gzip", "snappy" and "lzo" |
    | **ORC** | "none", "zlib", "snappy" and "lzo" |

[^1]: [Choosing the Right Big Data File Format: Avro vs. Parquet vs. ORC](https://blog.det.life/choosing-the-right-big-data-file-format-avro-vs-parquet-vs-orc-c868ffbe5a4e)
