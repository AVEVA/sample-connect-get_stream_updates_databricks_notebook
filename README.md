# CONNECT Get Stream Updates From Databricks Notebook
**Version:** 1.0.0

The sample code in this folder demonstrates how to get stream updates with CONNECT data services [change broker](https://docs.aveva.com/bundle/connect-data-services/page/1288745.html) and write those changes to a delta table in Databricks. In order to run this sample, you need to have a Databricks environment.

Developed against Python 3.10.12

## About the Sample

This sample demonstrates how to use the change broker in CONNECT data services to get stream updates. In general, when getting data into Databricks from CONNECT data services, you should use the [Virtual Tables feature](https://docs.aveva.com/bundle/connect-data-services/page/1469347.html). This is a no-code solution to getting stream and asset data into Databricks. However, using the change brocker in addition to virtual tables can be useful if you need very quick (less than 15 minute) updates on how a stream's data has changed. 

This sample contains two notebooks. The first, [Get Updates from CONNECT Notebook.ipynb](https://github.com/AVEVA/sample-connect-get_stream_updates_databricks_notebook/blob/main/Get%20Updates%20from%20CONNECT%20Notebook.ipynb), is meant to be run manually and walks you through the steps to get the updates. Use this notebook as a learning guide to understand the flow of getting updates.

The second, [Get Updates from CONNECT Notebook - For Jobs.ipynb](https://github.com/AVEVA/sample-connect-get_stream_updates_databricks_notebook/blob/main/Get%20Updates%20from%20CONNECT%20Notebook%20-%20For%20Jobs.ipynb) is written to be run via a databricks job. It cannot be run manually since it uses job parameters for certain connection information and settings. This sample doesn't walk through it's logic but is meant to show how you might implement the code in a job. Other than those differences, they use the same code and logic to accomplish getting stream updates. 

Both samples assume that the chosen stream has a **Value** and **Timestamp** pair and that the values are numeric type. If your stream contains values of a type that cannot be converted to **double**, you will need to modify the code accordingly.

## Getting Started

- Clone the GitHub repository or download the .ipnyb files
- Import the notebook(s) into your Databricks environment. Follow the instructions at [Import and export Databricks notebooks](https://docs.databricks.com/aws/en/notebooks/notebook-export-import)
- For **Get Updates from CONNECT Notebook.ipynb**, follow the instructions in the notebook an run each code block in order.
- For **Get Updates from CONNECT Notebook - For Jobs.ipynb**, create a scheduled Notebook Job in Databricks by following the instructions at [Create and manage scheduled notebook jobs](https://docs.databricks.com/aws/en/notebooks/schedule-notebook-jobs) You will need to set the following as job parameters:
  - apiVersion - the API version for the signups and updates REST endpoints of CONNECT. (e.g. v1)
  - resource - the base CONNECT url for the region of your namespace. (e.g. https://uswe.datahub.connect.aveva.com)
  - tenantId - the tenant Id from CONNECT.
  - namespaceId - the namespace Id from CONNECT.
  - streamIds - the list of stream Ids to get updates for from CONNECT. This should be a comma separated list. (e.g. stream1, stream2)
  - catalog_name - the catalog name of the delta table you'd like to create and write updates to.
  - schema_name - the schema name of the delta table you'd like to create and write updates to.
  - table_name - the catalog name of the delta table you'd like to create and write updates to.
    
### Creating the secret scope

This sample makes use of secret scopes in Databricks to securely store the credentials to CONNECT data services. To set up the secret scope, first create a client credentials client in CONNECT data services. For this sample, the client credentials client needs to be given a role that has read and write access to a Cds namespace. For instructions, see: [Add a client-credentials client](https://docs.aveva.com/bundle/connect-data-services/page/1263324.html) 

You can then create the secret scope with one of two options. The first is to use the Databricks CLI. To do this option, use the workspace terminal or command prompt. You can follow [Create a secret](https://docs.databricks.com/aws/en/security/secrets#create-a-secret) Create two secrets within that secret scope called cdsclientid and cdsclientsecret containing the client id and secret generated from Cds

The second option is to create a secret scope using the Databricks SDK for Python. If using this option, you can use the sample code included to create the secret scope and secrets. This option which requires entering your client credentials into the notebook in plain text temporarily. It's recommended to delete these credentials after the block is run.

### Running The Notebook

To run the Notebook(s), you first need to attach it to a compute resource (cluster or SQL warehouse). Once attached, you can run cells individually, run all cells, or schedule the notebook as a job.

### Test the Notebook

The last cell in the [Get Updates from CONNECT Notebook.ipynb](https://github.com/AVEVA/sample-connect-get_stream_updates_databricks_notebook/blob/main/Get%20Updates%20from%20CONNECT%20Notebook.ipynb) are for running tests so that you can test to make sure the whole notebook is working as expected. As it tests the methods defined earlier in the notebook, you need to run the previous cells of the notebook before trying to run the tests. If the tests pass, the block will succeed without any exceptions.

---

For the main Cds samples page [ReadMe](https://github.com/AVEVA/AVEVA-Samples-CloudOperations)  
For the main AVEVA samples page [ReadMe](https://github.com/AVEVA/AVEVA-Samples)
