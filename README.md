The Role of Sex in Moderating Response to Pathogens in Childhood Diarrhoeal Disease
================
The ATGC Team
2019-04-03

Members and tasks
-----------------

<table style="width:11%;">
<colgroup>
<col width="5%" />
<col width="5%" />
</colgroup>
<thead>
<tr class="header">
<th>Contributor</th>
<th>Responsibilities</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tonya Severson</td>
<td>FastQC, CPM to RPKM conversion, data subsetting, enrichment analysis</td>
</tr>
<tr class="even">
<td>Fatema Tuz Jhohura</td>
<td>Data exploration and visualization, linear regression, pheatmap, PCA</td>
</tr>
<tr class="odd">
<td>Sam Breaux</td>
<td>Dataset validation, PCA, comparative analysis, paper reproduction</td>
</tr>
<tr class="even">
<td>Yao Chen</td>
<td> Explore alternative method, Refining the figure, build classifier</td>
</tr>
</tbody>
</table>

Introduction
------------

The Global Burden of Disease Study in 2016 found that diarrhoeal diseases ranked eighth among the leading causes of deaths at any age, and fifth for deaths of children younger than 5 years of age \[1\]. Moreover, according to the World Health Organization, in 2017 diarrhoea was the leading cause of malnutrition in children under 5, the second leading cause of death, with about 525,000 deaths occurring annually in this age group \[2\]. Diarrhoea in children can have various causes, including viral or bacterial pathogens or non-pathogenic causes. A recent study reported the use of RNA-Seq to identify genetic signatures that could be used to diagnose specific pathogenic agents responsible for cases of childhood diarrhoea \[3\]. Whole blood specimens were collected from 48 healthy children (controls) and 198 children with diarrhea caused by a single bacterial or viral pathogen as confirmed by pathogen-specific tests of stool samples. Children were included in the study if diagnosed with rotavirus (n=55), *E. coli* (55), Salmonella (36), Shigella (37), adenovirus (8), or norovirus (7). The authors of the study focused on differential expression of genes related to chemokine receptors, inflammasome signaling and interferon response, looking at relationships between complement and interferon-stimulated gene expression with patient age and severity of illness, but did not mention any analyses of relationships between other pathways with age, severity or days post onset. We hypothesized that genes related to the host response to microorganism infection would be expressed differently based on host sex, and that the gene expression profile of each group could be quantitatively differentiated. We built a parametric classifier to predict pathogen types, since nonparametric methods like PCA didn’t work well.

Objectives
----------

1.  Recreate several analyses from the original paper as a reality check.
2.  Determine whether sex of patient influences response to pathogen.
3.  Build a classifier to predict pathogen type based on differentially expressed genes.

Our Dataset
-----------

The original paper describing the dataset is [here.](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0192082) Descriptions of the source files and links are located in our repo [here.](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/tree/master/data)

Links to results
----------------

#### Data preparation and QC

-   [Merging of files](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/fileMerging.md) and [creation of RPKMs](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/RPKM.md)
-   [FastQC ribosomal check](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/ribosomalCheck.md)
-   Imputation testing
    -   [NAs Imputed](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/IMPst.md)
    -   [NAs Removed](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/NArest.md)
-   [Prep of counts for voom](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/prepCountsForVoom.md)

#### Exploratory analyses
-   [Vizualization of the filtered data](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/New_processdata_Exploration_fatema.md)
-   [Principle components analyses](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/lm.md)
-   [Differential expression analyses](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/regression_pheatmap_pca.md)
-   [Gene enrichment/multifunctionality analysis](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/GeneEnrichment.md)

#### Effect of patient sex on pathogen response

-   [PCA](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/lm.md)
-   [p-value distribution](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/GeneEnrichment.md)

#### Classifier

-   [Classifier development](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/yao/Yao_edgeR_Classifier.md)

Summary of presented results
----------------------------

### Data filtering and vizualization
Expression data contains 23826 genes and 193 samples where 29 samples are healthy controls 
and 164 samples come from different infection group. In the gene expression data, there are 8339 rows which contains all NA and 0 information. For the purpose of our analysis we filtered out
these rows and finally obtain total 15487 genes for analysis. All the samples are matched with the sample meta data. As the expression values are not normally distributed, we take Log2 transformation to the gene expression value and draw the [boxplot](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/New_processdata_Exploration_fatema_files/figure-html/unnamed-chunk-2-1.png) and overall [density plot](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/NArest_files/figure-html/look-2.png) of the expression values . In terms of distribution all the samples looks similar in both boxplot and density plot. To examine different genes patterens with respect to the infectious group in our dataset we have draw a [scatterplot](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/New_processdata_Exploration_fatema_files/figure-html/unnamed-chunk-3-1.png) of few arbitrary genes. From this plot it is showed that there have some NA values still in the dataset after filetring NA rows. We handels these NA values when doing particulat gene expression analysis. After scaling ang centering the filtered data we draw a dendrogram to look at the 
Clustering effect. We can look at the trees that are output from different clustering  algorithms. However, it can also be visually helpful to identify what sorts of trends in the data are associated with these clusters using [hierarchical clustering plot](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/New_processdata_Exploration_fatema_files/figure-html/unnamed-chunk-4-1.png). We can look at this output using heatmaps. To examine the correlation between samples we draw different heatmaps. We use pheatmap() function with annotations and cor to correlate gene expression between each pair of samples for the [first heatmap](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/regression_pheatmap_pca_files/figure-html/unnamed-chunk-1-1.png) and after scaling and centering the filtered expression data we draw the [2nd heatmap](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/regression_pheatmap_pca_files/figure-html/unnamed-chunk-1-2.png). Second one is more closer to that one which is on the original paper. Make a bar graph of PCA showing the amount of variance explained by each PC, where variance explained is on the y axis and each PC is on the x axis. More about PCA analysis is given as follows. The [simple linear regression and multiple linear regression](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/Fatema/regression_pheatmap_pca.md) shows that the infectious group, who score, age group and sex has significant (p-value<0.0001) effect on gene expression. 

### Imputation and PCA

The various datasets created had to be compared to determine the most appropriate one to work with for further analysis. We accomplished this by comparing the datasets in several key metrics to each other, the original processed data file, and results from paper. The first 2 datasets created were from one of the original data that contained the correct control names (we were unaware that there were two at the time) and were of the sum and mean of the duplicated genes. They each contained 15508 genes compared to the original processed data which had 20347. [The results from the analyses](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/tree/master/src/sam/old) indicated that they were both pretty similar to each other and the fairly similar to the processed data that lacked controls. Evident by the distribution of variance in the first two PCAs (sum: 35.37% & 10.36%, mean: 34.97% & 10.29%, processed: 31.28% & 9.09%). Although all were fairly distinct from the PCA results from the paper (28.2 & 8.2). We then discovered the additional dataset which need to be combined with the other. After this the CPM values were converted to RPKM values and it became apparent that the authors had most likely had taken the sum expression of their duplicated genes. The combination of two datasets though introduced many NA values as they were sequenced at different times and captured a different array of genes. We had to determine the best way to deal with the NA values. We compared removing those genes that contain NA values (NA=RE), or imputation by mean (NA=IMP). The datasets originally contained 23826 genes. After filtering out NA values NA=RE contained 15487 genes. For the NA=RE dataset the variance of the PCAs was 35.05 and 9.87. The graphs for [PC1 vs PC2](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/NArest_files/figure-html/pc%20plots%202-1.png) and [PC1 vs %neutrophils](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/NArest_files/figure-html/pc%20plots%202-2.png) more closely matched those in the paper in the NA=RE dataset. The imputation dataset was made by imputing the missing genes in the cases from the other cases and the mean of the gene expression in the controls were used to impute the controls. Imputation created a noticeable amount of variance in PC1 related to the infection group (case or control) with a multiple R-squared value of .61. This difference is also highlighted in the [PC1 vs PC2](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/IMPst_files/figure-html/pc%20plots%202-1.png) and the [PC1 vs % neutrophils plots](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/sam/IMPst_files/figure-html/pc%20plots%202-2.png), with the controls and case clustering with each other. Which are distinctly different from the other datasets and the results found in the paper. From these results we moved forward with the NA=RE dataset.

### Test of hypothesis that sex of patient affects response to pathogen

Using the NA=RE data set we analyzed the source of variance in the first 3 PCAs based on sex. The multiple R-squared value showed that sex accounted for 0.275%, 0.2297%, and .1196% of the variation in PC1, 2 and 3 respectively. The other datasets analyzed had similarly low values. Trends were also looked for within the sample correlation heatmap, but weren’t found. We also looked for genes that may be differenatially expressed due to pathogen type and found none. Finally, we examined p-value distributions for differentially expressed genes for the pathogen\*sex interaction coefficient and saw uniform distributions for all [the Shigella-sex comparison is linked here](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/GeneEnrichment_files/figure-markdown_github/mf%20pval%20v%20pval-1.png). From these observations, we can conclude that sex does not play an important role in the development of childhood diarrhea.

### Gene enrichment/multifunctionality analysis

Since patient sex played no role in moderating expression in response to pathogens, it didn't make sense to look for gene enrichment for that comparison, and we decided to examine gene enrichment for differentially expressed genes in Shigella-infected patients vs healthy controls. The list of all genes and log fold changes were taken from topTable output for the comparison and ranked according to the absolute logFC. Using ermineJ (launched by ermineR) \[4\], and EGAD \[5\] allowed calculation of multifunctionality scores for each of the genes (in this case, we chose to look at biological processes) - reporting a [Spearman's rank correlation](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/GeneEnrichment_files/figure-markdown_github/EGAD%20multifunc%20scores-1.png) of -0.03 for the set. Reassuringly, given we were looking at differential expression in patients infected by microbial pathogens, top ranked biological processes involved immunity. We found that [several biological process categories decreased in significance](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/src/tonya/GeneEnrichment_files/figure-markdown_github/mf%20pval%20v%20pval-1.png) after adjusting for multifunctionality (e.g., positive regulation of myeloid leukocyte mediated immunity, granulocyte migration and cell-cell adhesion via plasma-membrane adhesion molecules). Four others persisted (e.g., humoral immune response, defense response to bacterium, neutrophil migration and regulation of myeloid leukocyte mediated immunity); however, rerunning the analyses resulted in some biological processes persisting in one run and dropping in another, likely because of sampling performed during the analysis.

The original paper \[3\] reported that genes involved in complement and coagulation cascade were differentially expressed in common among Shigella, Salmonella and rotavirus cases, whereas differentially expressed genes specific to Shigella response were involved in neutrophil and leukocyte activation, cytokine and cytokine receptors, and recognition of peptidoglycan and lipopolysaccharide. Thus, the top reported biological processes are not identical to ours, but closely related. Several of the genes representing the processes reported by the authors were not confirmed by our analyses to be significantly differentially expressed, possibly because of slight differences in models applied.

### Classifier

Under the rationale that the gene expression vary in different infectious condition, it would be helpful if we could use the expression profile to aid the diagnostic in clinical practice, hence we decided to build a classifier based on the RNA-seq expression profile of the selected genes in training set.

The model we are using is a multinomial regression model with no regularization \[6\]. We fitted and tested our model using 2 fold cross validation with equal sized randomized partition in our 192 samples. We reduced the response variable from 5 categories (Rotavirus, E.coli, Salmonella, Shigella, Healthy Control) to 3 categories (Viral, Bacterial, Healthy Control) because of the limited sample size and the pathological similarity behind it. The table below shows the partition of our training and test set.

| Set   | Bacterial | Viral | Healthy Control |
|-------|-----------|-------|-----------------|
| Fold1 | 51        | 28    | 15              |
| Fold2 | 61        | 23    | 14              |

The genes used in the model were selected based on the differentially expressed genes in the training set with the criteria below:

| Criterion        | E. coli | Salmonella | Shigella | Rotavirus |
|------------------|---------|------------|----------|-----------|
| FDR              | 0.05    | 0.05       | 0.05     | 0.01      |
| log Fold changes | 2       | 2          | 2        | 3         |

2-fold training error and validation error

| Fold  | Training Error | Validation Error |
|-------|----------------|------------------|
| Fold1 | 72.3%          | 70.4%            |
| Fold2 | 79.6%          | 68.1%            |

Deliverables
------------

[**Proposal**](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/project_proposal.md)

[**Progress Report**](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/progress_report.md)

[**Presentation**](https://github.com/STAT540-UBC/Repo_team_The-ATGC-Team_W2019/blob/master/540grouppro.pptx)

References
----------

1. Troeger C, Blacker BF, Khalil IA, Rao PC, Cao S, Zimsen SRM, et al. Estimates of the global, regional, and national morbidity, mortality, and aetiologies of diarrhoea in 195 countries: a systematic analysis for the Global Burden of Disease Study 2016. The Lancet Infectious Diseases. 2018;18:1211–28. doi:[10.1016/S1473-3099(18)30362-1](https://doi.org/10.1016/S1473-3099(18)30362-1).

2. WHO. Diarrhoeal disease. 2017. <https://www.who.int/news-room/fact-sheets/detail/diarrhoeal-disease>. Accessed 10 Feb 2019.

3. DeBerg HA, Zaidi MB, Altman MC, Khaenam P, Gersuk VH, Campos FD, et al. Shared and organism-specific host responses to childhood diarrheal diseases revealed by whole blood transcript profiling. PLOS ONE. 2018;13:e0192082. doi:[10.1371/journal.pone.0192082](https://doi.org/10.1371/journal.pone.0192082).

4. Gillis J, Mistry M, Pavlidis P. Gene function analysis in complex data sets using ermineJ. Nature Protocols. 2010;5:1148–59. doi:[10.1038/nprot.2010.78](https://doi.org/10.1038/nprot.2010.78).

5. Ballouz S, Weber M, Pavlidis P, Gillis J. EGAD: Ultra-fast functional analysis of gene networks. Bioinformatics. 2017;33:612–4. doi:[10.1093/bioinformatics/btw695](https://doi.org/10.1093/bioinformatics/btw695).

6. Friedman J, Hastie T, Tibshirani R. Regularization Paths for Generalized Linear Models via Coordinate Descent. Journal of Statistical Software. 2010;33:1–22. doi:[10.18637/jss.v033.i01](https://doi.org/10.18637/jss.v033.i01).
