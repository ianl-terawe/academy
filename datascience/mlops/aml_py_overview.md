# Azure Machine Learning: An Overview of the Python Client Library

## Making Use of the DSVM

This exercise makes use of the Jupyter Notebook service provided by the Data Science Virtual Machine (DVSM) from the first module of this course. From its GitHub repo, open the Jupyter Notebook [here](https://github.com/Azure-Samples/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb).

To focus on use of Azure Machine Learning, scroll through the notebook until you locate the section heading "Using the Azure ML Python Client Library (azureml)".

Because Azure ML comes pre-installed, it can be readied for use with minimal coding; namely:

```Python
from azureml import Workspace

ws = Workspace(workspace_id='1d025f281a4040079bb163b3ea26d943',
               authorization_token='a7cfafc082c940769248299b3feda314',
               endpoint='https://studioapi.azureml.net' )
```

Replace the above `workspace_id` and `authorization_token` with those provided to you via the Academy Workspace here. Execute this block of code. 

Work through the remainder of the examples in this notebook. In so doing, you'll cover:

- The list of available examples 
- The list of datasets - including those contributed by users 

## Making Use of Azure ML Compute Instances  

Outside of the DSVM, the most-convenient way to make use of the Azure ML SDK is via Azure ML Compute Instances. As was the case with the DVSM, these compute instances come pre-loaded with the Azure ML SDK. 

## Making Use of Azure ML from Scratch

To get started, follow the steps detailed [here](https://github.com/Azure/MachineLearningNotebooks). To install the core Python module of Azure ML for example, issue the command:

```bash
pip install azureml-core
```

> **Note:**
> `pip` commands can be excecuted directly from within a Jupyter Notebook. 

As indicated at the above GitHub repo, additonal packages (e.g., AutoML) can easily be installed in an analogous fashion:

```bash
pip install azureml-mlflow
pip install azureml-dataset-runtime
pip install azureml-automl-runtime
pip install azureml-pipeline
pip install azureml-pipeline-steps
...
```

