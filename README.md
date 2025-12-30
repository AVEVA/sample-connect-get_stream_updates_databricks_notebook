# CONNECT Write From Databricks Notebook
**Version:** 1.0.0

The sample code in this folder demonstrates how to write data back to CONNECT data services from Databricks. In order to run this sample, you need to have a Databricks environment.

Developed against Python 3.10.12

## About the Sample

This sample is intended to show you how you can write time series to CONNECT data services from a Databricks notebook. This may be useful after performing analytics or modelling in Databricks to bring those insights back to the CONNECT platform (and then perhaps back to an on-prem system.) There are two sample notebooks in this repository. The first, **Write Single Stream to CONNECT using API Notebook.ipynb**, uses the CONNECT data services sequential data store (sds) REST API to write values to a stream. It also makes use of the [Python sample library](https://github.com/AVEVA/sample-adh-sample_libraries-python) to keep the code simple. This is method is straightforward and is more suited towards sending minimal data to one or a few streams. The second notebook, **Write Multiple Streams to CONNECT using OMF Notebook.ipynb**, is more suited to sending large amount of data to one or many streams. The sample demonstrates using the CONNECT data services OMF endpoint to write data to a few streams.

## Getting Started

- Clone the GitHub repository or download the .ipnyb files
- Import the notebook(s) into your Databricks environment. Follow the instructions at [Import and export Databricks notebooks](https://docs.databricks.com/aws/en/notebooks/notebook-export-import)
- Follow the instructions in the notebook an run each code block in order.

### Creating the secret scope

This sample makes use of secret scopes in Databricks to securely store the credentials to CONNECT data services. To set up the secret scope, first create a client credentials client in CONNECT data services. For this sample, the client credentials client needs to be given a role that has read and write access to a Cds namespace. For instructions, see: [Add a client-credentials client](https://docs.aveva.com/bundle/connect-data-services/page/1263324.html) 

You can then create the secret scope with one of two options. The first is to use the Databricks CLI. To do this option, use the workspace terminal or command prompt. You can follow [Create a secret](https://docs.databricks.com/aws/en/security/secrets#create-a-secret) Create two secrets within that secret scope called cdsclientid and cdsclientsecret containing the client id and secret generated from Cds

The second option is to create a secret scope using the Databricks SDK for Python. If using this option, you can use the sample code included to create the secret scope and secrets. This option which requires entering your client credentials into the notebook in plain text temporarily. It's recommended to delete these credentials after the block is run.

### Running The Notebook

To run the Notebook(s), you first need to attach it to a compute resource (cluster or SQL warehouse). Once attached, you can run cells individually, run all cells, or schedule the notebook as a job.

### Test the Notebook

The last cell in the notebooks are for running tests so that you can test to make sure the whole notebook is working as expected. As it tests the methods defined earlier in the notebook, you need to run the previous cells of the notebook before trying to run the tests. If the tests pass, the block will succeed without any exceptions.

---

For the main Cds samples page [ReadMe](https://github.com/AVEVA/AVEVA-Samples-CloudOperations)  
For the main AVEVA samples page [ReadMe](https://github.com/AVEVA/AVEVA-Samples)
