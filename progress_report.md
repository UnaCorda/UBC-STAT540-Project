## What has changed based on the final proposal
* Did your dataset change? If so, why? 

  Our dataset didn’t change so much as our understanding of how best to access the data evolved, and we realized that CPMs were not     sufficient for our needs. The recount database RSE objects appeared to contain only a fraction of the data, and lacked some of the metadata, as well. A file from GEO that we understood to contain the final count data lacked the majority of the controls. After correspondence with the lead author of the study, we learned that the dataset was split over two files, and that the best metadata source was in supplementary materials available on the journal website.

* Have you decided to do a different analysis than what was mentioned in your proposal? If so, Why?

  No changes so far. 

* Are there any changes in task assignments of group members?
  
  We have made some adjustments to reflect changes in tasks thus far and made additional tasks more explicit.

  | Contributor  | Changes |
  |---|---|
  | Tonya Severson | FastQC, CPM to RPKM conversion, data subsetting, enrichment analysis |
  | Fatema Tuz Jhohura | Data exploration and visualization, linear regression, pheatmap, PCA |
  | Sam Breaux | Dataset validation, imputation, PCA, comparative analysis, paper reproduction |
  | Yao Chen | GGpairs, Analyzing and find explanation to the resuly, Refining the figure |
  
## What is the progress of the analyses
* Briefly and concisely explain your methodology and progress for the aims you have investigated so far. Which parts were modified and which parts remained the same?

	Our aim is to understand the relationship between RNA-seq expression profile and the clinical information in the infected children. Before the analysis, we did the QC check of the dataset, It took more time than we expected due to some problem in the dataset. We contacted the original author and ensured that we have the complete dataset. We checked the distribution of the genes as well as the balance of the groups. The density plot and the histogram didn’t show any abnormality. We haven’t check the batch effect yet because we haven’t find the batch information about the sample. But the heatmap showed some potential batch effect.
Then we did the PCA and heatmap for understanding the high dimensional structure of our data. We were able to recreate and optimized the PCA result in the original study. We did a more throughout PCA pairs and get some preliminary result. Next we will do the differentially expressed gene analysis.

* What R packages or other tools are you using for your analyses?

	Database Query: GEOquery, biomaRt, recount, GenomicRanges, GenomicFeatures\
	Dataframe Manipulation: Tidyverse, data.table, reshape2, readxl, Hmisc\
	Analysis: pheatmap, prcomp, limma

* Provide the links to any markdown reports within your repo to refer to the relevant analysis.

	Provided in the Result Section.
	
* Provide references.

1. Troeger C, Blacker BF, Khalil IA, Rao PC, Cao S, Zimsen SRM, et al. Estimates of the global, regional, and national morbidity, mortality, and aetiologies of diarrhoea in 195 countries: a systematic analysis for the Global Burden of Disease Study 2016. The Lancet Infectious Diseases. 2018;18:1211–28. doi:[10.1016/S1473-3099(18)30362-1](https://doi.org/10.1016/S1473-3099(18)30362-1).

2. WHO. Diarrhoeal disease. 2017. <https://www.who.int/news-room/fact-sheets/detail/diarrhoeal-disease>. Accessed 10 Feb 2019.

3. DeBerg HA, Zaidi MB, Altman MC, Khaenam P, Gersuk VH, Campos FD, et al. Shared and organism-specific host responses to childhood diarrheal diseases revealed by whole blood transcript profiling. PLOS ONE. 2018;13:e0192082. doi:[10.1371/journal.pone.0192082](https://doi.org/10.1371/journal.pone.0192082).

4. Barrett T, Wilhite SE, Ledoux P, Evangelista C, Kim IF, Tomashevsky M, et al. NCBI GEO: Archive for functional genomics data sets - Update. Nucleic Acids Research. 2013;41. doi:[10.1093/nar/gks1193](https://doi.org/10.1093/nar/gks1193).

5. Collado-Torres L, Nellore A, Kammers K, Ellis SE, Taub MA, Hansen KD, et al. Reproducible RNA-seq analysis using recount2. Nature Biotechnology. 2017;35:319. doi:[10.1038/nbt.3838](https://doi.org/10.1038/nbt.3838).

6. Kuleshov MV, Jones MR, Rouillard AD, Fernandez NF, Duan Q, Wang Z, et al. Enrichr: a comprehensive gene set enrichment analysis web server 2016 update. Nucleic acids research. 2016;44:W90–7. doi:[10.1093/nar/gkw377](https://doi.org/10.1093/nar/gkw377).

7. Sergushichev A. An algorithm for fast preranked gene set enrichment analysis using cumulative statistic calculation. bioRxiv. 2016;60012. doi:[10.1101/060012](https://doi.org/10.1101/060012).

8. Gentleman RC, Carey VJ, Bates DM, Bolstad B, Dettling M, Dudoit S, et al. Bioconductor: open software development for computational biology and bioinformatics. Genome Biology. 2004;5:R80. doi:[10.1186/gb-2004-5-10-r80](https://doi.org/10.1186/gb-2004-5-10-r80).

9. Andrews S. (2010). FastQC: a quality control tool for high throughput sequence data. Available online at: http://www.bioinformatics.babraham.ac.uk/projects/fastqc

10. Daniel R. Zerbino, Premanand Achuthan, Wasiu Akanni, M. Ridwan Amode, Daniel Barrell, Jyothish Bhai, et al. Ensembl 2018. doi:10.1093/nar/gkx1098

## Results 
### 1. QC

**Data Cleaning:** Metadata check based on gender specific genes. We filtered out 1 sample that was mislabeled. Identifying the value in the expression data, necessary conversion from CPM and RPKM using the gene length. GGpairs check the balance of the sample groups. Filtering the noise signal in the expression data using the cutoff of 70bp which is the shortest RNA exist.

**FastQC analysis:** The authors mentioned globin RNA reduction, but did not mention any means of eliminating ribosomal RNA [DeBergEtAl2019]. The fastq files from SRA were uploaded to a server for FastQC analysis [BabrahamFASTQC]. Five samples were selected at random to check whether overrepresented sequences corresponding to ribosomal RNA were present. The FastQC data indicated that the libraries were of unusually high quality, suggesting the fastq reads had been filtered. A representative report is in [available here](http://198.154.99.156:8080/).

**Merging of datasets:** Two files were downloaded from GEO (accession GSE69529): GSE69529_mexico_processed_data_for_GEO.csv.gz (containing CPM data from 20347 transcripts and 203 samples) and GSE69529_GSM2241808-GSM2241855_mexico2_data.csv.gz containing 20980 transcripts and 50 samples. Only a subset of each of these files appeared in the clinical metadata - 164 cases and 10 controls from the first, and 19 controls from the second - so these were selected and merged into one dataset. The code used for merging the datasets is here:https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/fileMerging.md

**Retrieval of coordinates from Ensembl and conversion of CPM to RPKM:** We discovered that the samples had actually been polyA-selected, so that normalization for length would be required. The dataset only contained gene start and stop coordinates for the original batch submitted to GEO. We inferred from this that the authors normalized to gene length. Ensembl gene identifiers were used to query bioMaRt and retrieve gene start and end coordinates, transcript lengths, and HGNC symbols, in order to confirm that we were getting the right genes. Unexpectedly, the HGNC symbols retrieved for some Ensembl identifiers differed from the ones in the published dataset, and a subset of the identifiers without matching symbols had no symbol at all. We proceeded with the original HGNC symbols, but it is unclear why they should be different since the genome build reported for mapping matched the build for the current version of Ensembl. Separate files have been created reporting RPKM based on gene and transcript lengths. The RPKMs were grouped by sample and gene and separate files generated with averaged or summed RPKMs. Subsequent analyses used the file of RPKMs normalized to gene length and summed for each gene within a sample. The markdown files describing this work is available here: https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/bioMaRt.md


**Data Validation:** The various datasets created had to be compared to determine the most appropriate one to work with for further analysis. We accomplished this by comparing the datasets in several key metrics to each other, the original processed data file, and results from paper. The first 2 datasets created were from one of the original data that contained the correct control names (we were unaware that there were two at the time) and were of the sum and mean of the duplicated genes. They each contained 15508 genes compared to the original processed data which had 20347. The results from the analysis indicated that they were both pretty similar to each other and the fairly similar to the processed data that lacked controls. Evident by the distribution of variance in the first two PCAs (sum: 35.37% & 10.36%, mean: 34.97% & 10.29%, processed: 31.28% & 9.09%). Although all were fairly distinct from the PCA results from the paper (28.2 & 8.2).  We then discovered the additional dataset which need to be combined with the other. After this the CPM values were converted to RPKM values and it became apparent that the authors had most likely had taken the mean expression of their duplicated genes. The combination of two datasets though introduced many NA values as they were sequenced at different times and captured a different array of genes. We had to determine the best way to deal with the NA values. We compared transforming the NA values to 0 (NA=0), removing those genes that contain NA values (NA=RE), or imputation by mean. The datasets originally contained 23826 genes. After filtering out NA values NA=RE contained 15487 genes. Once the NA values in the NA=0 were transformed to 0; genes with 0 expression values in less than or equal two three genes were filtered out (similar to what was done in the paper) leaving us with 20536 genes. The variance for the first two PCAs for the NA=0 dataset were 27.58 and 8.6 respectively. For the NA=RE dataset the variance of the PCAs was 35.05 and 9.87. However the graphs for PC1 vs PC2 and PC1 vs %neutrophils more closely matched those in the paper in the NA=RE dataset (although they seem backwards?). The NA=RE PCAs also matched that of the original processed dataset more closely. The imputation datset was made quickly. As the controls contained most of the missing data points we only imputed 19 controls using data from 3 other that had expression values for the missing genes. Other NA values were deleted from the dataset. Imputation created a noticable amount of variance in PC2 related to the infection group (case or control) with an R-squared value of .4548 compared to the same value in next the next highest dataset, .3062 in NA=0; this difference is also higlighted in the PC1 vs PC2 graph with is distinctly different from the other datasets and that found in the paper. We expect that futher imputation will make this worse as we are artificially correalating the data. Although, the trends in the heatmap between the original and imputed data track closely. See **Data Validation Figures**.

### 2.**Data Quality Figures**

#### **Histogram: NA=RE**

<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatameanPGnaremoved_files/figure-html/look-1.png" width="600" title="Histogram">

#### **Density plot**

<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/yao/Yao_files/Rplot.png" width="600" title="Density Plot">

#### **GGpairs**

<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/yao/Yao_files/GGpairs.png" width="600" title="Density Plot">


### 3. **Data Validation Figures**

#### **Variance in first 3 PCAs** 

**Sum Method**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/varPCsum.png" title="Variance PC1:PC3">

**Mean Method**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/varPCAmean.png" title="Variance PC1:PC3">

**Original Processed Data**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/varPCprocData.png" title="Variance PC1:PC3">

**NA=0**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/varPCAna0.png" title="Variance PC1:PC3">

**NA=RE**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/varPCAnaRE.png"  title="Variance PC1:PC3">

**NA=Imputed**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/varPCimp.png"  title="Variance PC1:PC3">

#### **Heatmaps**  

Heatmap shows correlation value between the heathy control and the infected groups is low. In a sense it tell us the gene is differentilly expressed when a patient has the infection. But because of the missing value in the data set, we somehow get drastically different result if we use different method to handle missing value.

**Original Proccessed data**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdata_files/figure-html/look-3.png" width="600" title="HeatMapprocdata">

**NA=RE**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatameanPGnaremoved_files/figure-html/look-3.png" width="600" title="HeatMapNA=re">

**NA=0**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanPG_files/figure-html/look-3.png" width="600" title="HeatMap=0">

**NA=Imputed**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanIMP_files/figure-html/look-3.png" width="600" title="HeatMapimputed">

#### **Variance Due to Infection Group in PC2**
**Original Proccessed data**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/procpc2r2.png" title="procdataR2infect">

**NA=RE**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/naREpc2r2.png" title="NARE_R2infect">

**NA=0**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/na0pc2r2.png" title="na0R2infect">

**NA=Imputed**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/imppc2r2.png" title="naimpR2infect">

### **Paper Reproduction: PC1 vs PC2 & PC1 vs %Neutrophils**

The PCA result in the original study and our replica. We are able to achieve a very close result and come up with the same conlcusion in this study. 

**Paper figures**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/paperfigPC%26neut.png" width="600" title="paperfig">

**NA=0 PC1 vs PC2**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanPG_files/figure-html/pc%20plots%202-1.png" width="600" title="na0pc1vpc2">

**NA=0 PC1 vs %Neutrophils**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanPG_files/figure-html/pc%20plots%202-2.png" width="600" title="na0%neut">

**NA=RE PC1 vs PC2 (both axises flipped)**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatameanPGnaremoved_files/figure-html/pc%20plots%202-1.png" width="600" title="naREpc1vpc2">

**NA=RE %Neutrophils**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatameanPGnaremoved_files/figure-html/pc%20plots%202-2.png" width="600" title="naRE5neut">

**NA=Imputed PC1 vs PC2**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanIMP_files/figure-html/pc%20plots%202-1.png" width="600" title="naIMPpc1vpc2">

**NA=Imputed %Neutrophils**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanIMP_files/figure-html/pc%20plots%202-2.png" width="600" title="na1mp%neut">

##### Further figures and analyis can be found in the RMD/MD files 
[Original.RMD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata.Rmd)
, [Original.MD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdata.md)

[sum.RMD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatasum.Rmd)
, [sum.MD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatasum.md)

[Mean.RMD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatamean.Rmd)
, [Mean.MD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatamean.md)

[NA=0.RMD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatameanPG.Rmd)
, [NA=0.MD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanPG.md)

[Na=RE.RMD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatameanPGnaremoved.Rmd)
, [NA=RE.MD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanPGnaremoved.md)

[NA=Imputed.RMD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdatameanIMP.Rmd)
, [Na=Imputed.MD](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/samdatameanIMP.md)

### 4. Preliminary Exploratory Analysis
#### Hypothesis: Preliminary findings
Using the NA=RE data set we analyzed the source of variance in the first 3 PCAs based on sex. The multiple R-squared value showed that sex accounted for 0.275%, 0.2297%, and .1196% of the variation in PC1, 2, and 3 respectively. The other datasets analyzed had similarly low values. Trends were also looked for within the sample correlation heatmap, but weren’t found. From this we can conclude that sex does not play an important role in the development of childhood diarrhea.

**PC1**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/sexnaREpc1.png" title="Variance PC1sex">

**PC2**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/SEXNArePC2.png" title="Variance PC2sex">

**PC3**\
<img align="center" src="https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/samdata/images/SEXNArePC2.png" title="Variance PC3">

