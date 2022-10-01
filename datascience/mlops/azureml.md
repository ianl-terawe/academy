# Azure Machine Learning: An Overview 

## Code-Centric Development 

Azure Machine Learning (Azure ML) is the savviest way to leverage the breadth and depth of technologies available on Azure. Moreover, as Azure ML is a Platform-as-a-Service (PaaS) on Azure, the development _and_ operationalization of models are both in scope. 

Jupyter Notebooks offer a compelling means for developing Machine and Deep Learning models in Python and other programming languages. Other than the Azure ML ‘branding,’ those familiar with scikit-learn will immediately recognize its use in the figure below. Because Azure ML provides built-in support for scikit-learn, transitioning model development to the cloud can be as simple as uploading an existing Jupyter Notebook.  For those needing to code models for Machine and Deep Learning, Azure ML includes built-in support for:

![Jupyter Notebooks via Azure ML](https://raw.githubusercontent.com/ianl-terawe/academy/main/datascience/mlops/media/aml_jupyter.png "Jupyter Notebooks via Azure ML")

- Development tools – such as Command-Line Interfaces (CLIs), PyCharm and Visual Studio Code in addition to Jupyter Notebooks
- Programming languages – such as R in addition to Python 
- Frameworks – such as PyTorch, TensorFlow, and various others, in addition to scikit-learn 

Notably, Azure ML includes support for the Open Neural Network Exchange (ONNX); thus, the interoperability challenge resulting from framework proliferation is addressed on Azure as it is on the ground. In some ways more compelling in the case of a cloud-based deployment, availability of ONNX on Azure allows a model to be developed and pre-trained initially through use of one framework, and then subsequently:

- Deployed for inferencing purposes using a different toolchain
- Refactored and/or further enhanced by making use of a completely different framework

Between them, development tools and frameworks, deliver a powerful means for creating and/or refactoring Machine and Deep Learning models. Recall, however, that a critical aspect of the value they deliver is that of abstraction: programming the framework replaces programming distributed processors directly. Programming in the context of PyTorch, scikit-learn, TensorFlow, or similar frameworks, all but _removes_ the need to program for distributed infrastrucutres. In other words, the abstraction afforded developers by frameworks is one of simplified syntax and semantics. Of course, if needed, the lower-level programming of distributed accelerators remains a possibility for making contributions (e.g., purpose-built libraries) in support of applications. 

## No-Code Development 

There exists the potential for a ‘no-code option’ in the development of Machine and Deep Learning applications when use is made of Azure Machine Learning Designer. By making use of a visual authoring canvas, pre-existing modules can be _composed_ to address the requirements of quite sophisticated use cases. In the example illustrated in the figure below, the objective is to classify images by making use of the DenseNet model via the PyTorch framework. In principle, this highly abstracted approach for model development _removes_ the coding requirement. Thus, someone without coding knowledge or skills, who appreciates Machine or Deep Learning at more of a conceptual level, can rapidly build models. Such an authoring canvas may also be of value to architects or even experienced developers in cases where they need to rapidly prototype an algorithmic approach or model for consideration. Because Azure Machine Learning Designer allows code written in Python or R to be incorporated into the mix, the offering can also be considered to be of the ‘low-code variety.’ 

![Azure ML Designer](https://raw.githubusercontent.com/ianl-terawe/academy/main/datascience/mlops/media/aml_designer.png "Azure ML Designer")

## Automated Machine Learning

Whereas Azure Machine Learning Designer abstracts the creation of Machine and Deep Learning models from writing code to composing modules, Automated Machine Learning (variously Automated ML and AutoML) provides the means for surfacing an optimized model as follows (see figure below):

1.	Based upon the data provided to it, Automated ML engages in feature engineering (e.g., selection, and even generation) to accelerate the development of multiple models  
1.	From the suite of candidate models employed, Automated ML selects the best-performing model  
1.	For the selected model, a suite of hyperparameter tuning workload is generated, and Automated ML selects the tuned model offering the highest level of accuracy

![AutoML](https://raw.githubusercontent.com/ianl-terawe/academy/main/datascience/mlops/media/automl.png "AutoML")

Thus, Automated ML applies ‘meta-learning’ to derive an optimized model, from a suite of models, with minimal effort from the developer. Based upon technological breakthroughs from Microsoft Research, Automated ML is already proving effective in classic use cases such as classification, regression, and time-series forecasting. As was the case with Azure Machine Learning Designer, Automated ML need not be perceived as a replacement for 'hand-coding' models; rather, Automated ML can:

- Empower those without programmatic knowledge and skills to develop optimized and sophisticated models 
- Objectively inform architects or even experienced developers in cases where they might benefit from different algorithmic approaches in model development 