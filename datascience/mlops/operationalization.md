# Operationalizing Models 

Jupyter Notebooks and IDEs allow developers of Deep Learning applications to run their code. When crafting prototypes of algorithmic implementations to entire models, this simplest of approaches can be effective for training, validation, and inferencing purposes. However, the need to properly operationalize the lifecycle of Deep Learning models can escalate rapidly – even before production implementations are established. 

![AML Overview](/datascience/mlops/media/automl.png "AML Overview")

Working progressively from left-to-right in the above figure, the essentials of the service are:

- Data - Their innate ability to be driven by extremely large volumes of data is what differentiates Deep Learning models. As the figure illustrates, such models may need to leverage data that resides in relational databases to file stores, or remotely stored data that can only be retrieved via API calls. Thus, a critical enabler of the Azure ML service is that of the underlying data platform available on Azure. The introduction of a data lake (e.g., via Azure Data Lake ), for example, allows data from multiple sources to be aggregated into a single storage namespace. Even though the data can retain its original format (e.g., from unstructured to semi-structured to structured), by localizing it in this fashion via a data lake, models can be more easily trained and validated. The ability to implement scalable solutions for production use is another benefit of a modern data platform that accounts for all the attributes of Big Data. 

- Build and Train Models – From support for traditional Jupyter Notebooks and IDEs, to the no/low-code option of Azure Machine Learning Designer, and finally to Azure Automated Machine Learning meta-learning model development, Azure Machine Learning provides options for developers. Not only does this allow developers to make use of the option best suited to their skill level (from no-code novice to seasoned professional), it also permits alignment with the developer’s intent.  Azure Machine Learning clearly broadens and deepens the possibilities for building and training models that serve initially as prototypes and ultimately in production. Additionally, Azure ML allows developers to again leverage ONNX – this time for runtime optimizations as opposed to interoperability between frameworks for Machine and Deep Learning. 

- Train Models – Model training is the most compute intensive aspect of the entire Machine Learning lifecycle. As models increase in complexity, so do the demands placed upon the compute infrastructure required to train them.  As Azure ML is fully integrated with the GPU computing capabilities available on Azure, model training can be scaled up to take advantage of one or more of these accelerators available from an isolated virtual machine. As complexity and/or data volumes increase, Azure ML allows model training to be scaled up and out across a distributed network of VMs.

- Validate – Once they have been trained, but prior to their use in production, models require validation.  Because containerization is a best practice for deploying and scaling models that will be used in production (see below), it makes sense to introduce this means for packaging the model and all its runtime requirements at this stage. Once available, the containerized implementation of the model can be validated on the data that was retained for this purpose. As noted in the schematic, use of Azure Container Instance is ideally suited to the needs of this validation phase. Moreover, uptake of containerization at this stage aligns well with DevOps principles that promote a proactive stance towards maintaining models (see below). 

- Deploy Models – Open-source Kubernetes is the de facto standard for orchestrating containers such as the validated pre-trained model envisaged here. The Azure Kubernetes Service (AKS) is an implementation of this ‘middleware’ available on Azure. Through its innate ability to replicate containers, AKS ensures that pre-trained can be scaled in response to demand for inferencing purposes.  From the cloud to the edge, uptake of AKS ensures that deployments are secure in addition to being scalable. 

- Monitor – Fundamental to operationalizing models is monitoring. From metrics to logs, Azure ML provides monitoring capabilities that can quantify aspects of the development process, through to production-grade deployments. Because monitoring establishes an unambiguous means for tracking their performance in production, the underpinnings of a proactive approach for maintaining models is established. 

- CI/CD – When it comes to Machine Learning applications, change is inevitable. For example, the need to incorporate more-diverse sets of data may trigger the need for retraining a Deep Learning application. As requirements evolve, so will the code, algorithms, methods, etc., needed to realize the application. Making use of code repositories (e.g., via GitHub) is therefore a best practice – a practice whose value escalates rapidly when a development team is involved (as opposed to an isolated individual). Use of GitHub is a prerequisite for implementing DevOps principles. For example, when changes to code are made, a cycle of Continuous Integration and Continuous Deployment (CI/CD) can be enabled through use of Azure DevOps. As illustrated in the figure, this Azure DevOps integration can trigger the retraining of a model. And assuming the retrained model can be properly validated, subsequent deployment and monitoring follows to complete this valuable DevOps feedback loop. 











<!--- here or intro? edit needed --->

At the outset, AI models can be prototyped on an isolated laptop. As their value becomes evident, and the need arises to transition them into more of a production deployment, operationalizing at scale can become a serious impediment to progress. In fact, redeploying a framework for Deep Learning from a laptop to more of an enterprise server, cluster, or cloud, may not resolve the challenges associated with operationalization at scale. Once again, Azure’s PaaS offering delivers tangible benefits in ensuring the transition from prototyping in the small to operationalizing at scale can be made as seamlessly as possible. 

## Accounting for Scale 

With respect to the use case considered here, the matter of scalability was addressed as a capability demanded by enterprise-grade offerings. Scale, of course, resonates soundly with the very notion of the public cloud; consequently, scale is codified into the DNA of CSPs. When it comes to use of the cloud then, scalability equates to table stakes. While this comprises a necessary condition for operationalizing AI at scale in the cloud, it is not a sufficient condition to guarantee scale.

Sufficiency is derived from the proven scalability of the PaaS components discussed in the use case considered here. The Azure Computer Vision service can be used to illustrate. The pre-trained model for the Azure Computer Vision service can be packaged in a container and be deployed to perform inferencing at the edge. Whether organizations ‘prefer’ a cloud-based deployment or one at the edge, it is evident that PaaS components such as Azure Computer Vision service have literally operationalized models at scale. The upshot for those savvy organizations that leverage PaaS components is that they have not only chosen a path that will accelerate their times to results, they have also selected a solution that scales as the AI-mediated healthcare is systematically operationalized. 