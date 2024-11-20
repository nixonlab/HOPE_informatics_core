# Analysis Workflow Overview

## **What Analysis Means in This Subgroup**

We structure and think of this analysis work as having different stages. Different people will have varying levels of experience in each stage.

### **Primary Analysis**
Processing raw data into a usable data structure for biological questions. For example, going from raw scRNA-seq FASTQ files into a counts matrix. This involves:

- Programming across different languages
- Managing large files
- Working in the terminal, without a user-friendly graphical interface

### **Secondary Analysis**
Using the data structures produced during primary analysis to perform analyses that address specific biological questions and/or biologically characterize the samples. Examples include:

- Differential gene expression between cell types
- Identifying HERV (or gene) markers for cell types under specific conditions
- Trajectory inference
- Integration with other data types (e.g., experiments measuring more than expression or additional datasets such as epigenetic data, CITE-seq, etc.)
- etcetera (there are so many of these, and the field continues to develop quickly)

**Secondary Analysis Key Tools:**  
R and its graphical environment (e.g., RStudio) are widely used, with Seurat being the most popular tool for this work. These analyses require applying each lab's biological expertise and specific objectives.

---

## **How We Will Work**

For scRNA-seq, our vision is that we will handle primary analysis: 
- People will provide their raw reads in fastq format and we will run them through the Stellarscope workflow and provide raw count matrices where the columns are cell barcodes (i.e. each column is one cell) and the rows are features (i.e. gene transcripts and locus-resolution TE transcripts). 
- Everyone from the bioinformatics group (all of us) will then perform different secondary analyses according to the goals set by the labs and the papers.

- In the bioinformatics subgroup meetings we will discuss together the secondary analyses and results.


**Collaboration:**  
- People in the group have extensive knowledge of scRNA-seq secondary analyses (e.g., corrections, normalization, cell type annotations, sample integration, statistical methods, etc.).  
- Most importantly, each lab has biological expertise and knows the experimental context, enabling them to make the most impactful decisions during secondary analysis.  

---

## **Resources**

To support this bioinformatics subgroup, the following resources have been set up:

1. **Cluster Access**  
   - For primary analysis tasks (e.g., aligning RNA-seq reads and running Stellarscope).

2. **File Sharing System**  
   - A platform for uploading raw data (FASTQ files) and metadata.  
   - Includes a spreadsheet template for specifying data characteristics, some examples are:
     - Experiment type  
     - 10x chemistry version (v1, v2, etc.)  
     - 5’ or 3’ data  
     - Sample-file mapping
     - etcetera
   - Scripts are being developed to automatically configure workflows for Stellarscope and streamline primary analysis.

3. **RStudio Web Server**  
   - Provides a user-friendly environment for secondary analysis.  
   - Results from Stellarscope will be accessible here, enabling secondary analysis as soon as matrices are generated.

**Usage:**  
We will discuss how to best utilize these resources based on everyone's needs during our meetings.
