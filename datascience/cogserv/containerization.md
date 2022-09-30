# Containerization 

The Computer Vision service allows its model to be containerized. Literally a self-contained version of the model capable of making inferences. Containerization results in the packaging of a pre-trained model along with its runtime dependencies into a self-contained image. Briefly, as they _share_ the kernel provided by the operating system of the host device, containers are lean implementations ideally suited to deployment in a variety of scenarios from the cloud to the edge.

> **Note:**
> Containers are a 'leaner implementation' than a virtual machine (VM). VMs, of course, require their own ‘guest’ operating system. 

<!--- schematics? --->

Pre-trained model can be stored securely in the Azure Container Registry (ACR) - a convenient repository that encourages container reuse. 