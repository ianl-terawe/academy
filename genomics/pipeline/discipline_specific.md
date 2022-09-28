# Discipline-Specific Pipelines

<!--- workflows vs. pipelines --->

## Motivation 

According to [Ahmed et al. (Sci Rep, 2021)](https://doi.org/10.1038/s41598-021-99288-8), the following have emerged as the key drivers for automating workflows:  

- The reality of increasingly large data volumes 
- The need for decreased time-to-results
- Guarantees of reproducible scientific results  

These drivers apply to production genomics research and clinical practice. However, these same drivers are broadly ’omics applicable – i.e., they apply to transcriptomics, proteomics, and metabolomics.

These same authors indicate that **Workflow Management Systems (WfMSs)** can:

- Compose individual tasks into cohesive pipelines
- Abstract away low-level details - ranging from data movement and processing to the management of task dependencies to the allocation of resources (e.g., compute) 

Additional 'value-added features' may include:

- Tracking data provenance
- Logging execution errors
- Authenticating users 
- Assuring data security
- ... and more ... 

## Bioinformatics 

Though related within the context of bioinformatics, the following considerations from [Ahmed et al. (Sci Rep, 2021)](https://doi.org/10.1038/s41598-021-99288-8) also apply to other areas of science:

- Modularity (e.g., support for checkpointing)
- Scalability (w.r.t. tasks, compute nodes) 
- Robustness (w.r.t. failures)
- Reproducibility (w.r.t. tasks, data, ...)
- Portability (w.r.t. compute environments)
- Interoperability (w.r.t. alternative WfMSs)
- Ease of development (e.g., support a range of end users)

## Cromwell on Azure 

The Cromwell WfMS implementation on Azure is:

- Based on the open-source implementation by the Broad Institute 
- Enabled for configuration and use as a ‘Cromwell service’ on Azure 
- Often employed as a best practice in tandem with GATK 
- Able to accept workflows detailed via Workflow Description Language (WDL) or Common Workflow Language (CWL)

> **Note:**
> Whereas WDL emphasizes human readability and an easy learning curve, CWL is more verbose to ensure reproducibility and portability.

An architectural schematic (sourced from the project's GitHub repo [here](https://github.com/microsoft/CromwellOnAzure)) is provided below. 

![Cromwell on Azure](/genomics/pipeline/media/cromwellonazure.png "Cromwell on Azure")

<!--- discuss arch & cf. w/ batch implementation used here --->