Proposal
================
The ATGC Team
Wed Feb 13, 2019

Motivation and background work
------------------------------

The Global Burden of Disease Study in 2016 found that diarrhoeal diseases ranked eighth among the leading causes of deaths at any age, and fifth for deaths of children younger than 5 years of age \[1\]. Moreover, according to the World Health Organization, in 2017 diarrhoea was the leading cause of malnutrition in children under 5, the second leading cause of death, with about 525,000 deaths occurring annually in this age group \[2\]. Diarrhoea in children can have various causes, including viral or bacterial pathogens or non-pathogenic causes. A recent study reported the use of RNA-Seq to identify genetic signatures that could be used to diagnose specific pathogenic agents responsible for cases of childhood diarrhoea \[3\]. Whole blood specimens were collected from 48 healthy children (controls) and 198 children with diarrhea caused by a single bacterial or viral pathogen as confirmed by pathogen-specific tests of stool samples. Children were included in the study if diagnosed with rotavirus (n=55), *E. coli* (55), Salmonella (36), Shigella (37), adenovirus (8), or norovirus (7). The authors of the study focused on differential expression of genes related to chemokine receptors, inflammasome signaling and interferon response, looking at relationships between complement and interferon-stimulated gene expression with patient age and severity of illness, but did not mention any analyses of relationships between other pathways with age, severity or days post onset. We hypothesize that genes related to the host response to microorganism infection will be expressed differently based on host sex, and that the gene expression profile of each group can be quantitatively differentiated. We will build a parametric classifier to predict pathogen types even the severity of the disease, since the nonparametric method like PCA didn’t work well.

Division of labour
------------------

<table style="width:86%;">
<colgroup>
<col width="9%" />
<col width="18%" />
<col width="12%" />
<col width="20%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Background</th>
<th>Degree</th>
<th>Affiliations</th>
<th>Job Assignments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sam Breaux</td>
<td>Pharmacogenomics, Microbiology</td>
<td>M.Sc.</td>
<td>Pharmaceutical Sciences</td>
<td>data filtering, PCA, batch effects</td>
</tr>
<tr class="even">
<td>Yao Chen</td>
<td>Populational Pharmacokinetics</td>
<td>M.Sc.</td>
<td>Pharmaceutical Sciences</td>
<td>differentially expressed gene identification, classification model, poster design</td>
</tr>
<tr class="odd">
<td>Fatema Tuz Jhohura</td>
<td>Biostatistics</td>
<td>M.Sc.</td>
<td>Statistics</td>
<td>data exploration, model fitting</td>
</tr>
<tr class="even">
<td>Tonya Severson</td>
<td>Sequencing, Entomology</td>
<td>M.Sc.</td>
<td>Genome Science and Technology</td>
<td>maintain bibliography, data exploration and visualization, presentation design</td>
</tr>
</tbody>
</table>

Dataset
-------

The dataset \[3\] was retrieved from GEO \[4\] and the recount2 database \[5\] and contain counts of genes observed in each sample in a tidy format. Metadata included demographics (age, sex, height, weight) and clinical data captured for each patient (e.g., cell counts for eight types found in whole blood, WHO diarrhoea severity scores, highest temperature, duration of illness, and days post onset). Only samples that passed quality filtering in the initial study and that have complete clinical metadata will be used (193 of 208 original samples). The count data were derived from 58-cycle, single-read sequence data generated on a HiSeq 2500 (Illumina, CA) using libraries prepared from globin-reduced RNAs and Illumina TruSeq reagents.

Aims and methodology
--------------------

1.  We will prepare the data and perform QC and exploratory analyses to identify any problems with our dataset and confirm that we can reproduce initial analyses from the original paper \[3\]. Methods to assess quality will include visualization of expression levels for genes that exhibited differential expression in patients infected by different pathogens (e.g., CCR3, CXCR8, NLRC4, associated with Shigella, or IFI44 and OASL, associated with rotavirus), comparison of overall expression levels among samples to assess uniformity of coverage, and correlation heatmaps, and will be used to determine whether any outliers need to be removed from further analysis or if additional normalization is required.

2.  Perform differential gene expression analysis and look for enrichment of pathways or relationships between genes and clinical characteristics other than the ones identified in the original study. For example, do responses mounted by male and female children against pathogens differ? Does expression of any genes or pathways correspond to the highest temperatures, or is expression of any genes related to severity score, age or days post onset? For pathway enrichment, we could use EnrichR \[6\] and/or FGSEA \[7\] packages from Bioconductor \[8\]. The pathway analysis could help us look into the mechanism of pathogenesis.

3.  Build a classifier to predict pathogen type, based on differentially expressed genes. We will use Logistic Regression, SVM.

References
----------

1. Troeger C, Blacker BF, Khalil IA, Rao PC, Cao S, Zimsen SRM, et al. Estimates of the global, regional, and national morbidity, mortality, and aetiologies of diarrhoea in 195 countries: a systematic analysis for the Global Burden of Disease Study 2016. The Lancet Infectious Diseases. 2018;18:1211–28. doi:[10.1016/S1473-3099(18)30362-1](https://doi.org/10.1016/S1473-3099(18)30362-1).

2. WHO. Diarrhoeal disease. 2017. <https://www.who.int/news-room/fact-sheets/detail/diarrhoeal-disease>. Accessed 10 Feb 2019.

3. DeBerg HA, Zaidi MB, Altman MC, Khaenam P, Gersuk VH, Campos FD, et al. Shared and organism-specific host responses to childhood diarrheal diseases revealed by whole blood transcript profiling. PLOS ONE. 2018;13:e0192082. doi:[10.1371/journal.pone.0192082](https://doi.org/10.1371/journal.pone.0192082).

4. Barrett T, Wilhite SE, Ledoux P, Evangelista C, Kim IF, Tomashevsky M, et al. NCBI GEO: Archive for functional genomics data sets - Update. Nucleic Acids Research. 2013;41. doi:[10.1093/nar/gks1193](https://doi.org/10.1093/nar/gks1193).

5. Collado-Torres L, Nellore A, Kammers K, Ellis SE, Taub MA, Hansen KD, et al. Reproducible RNA-seq analysis using recount2. Nature Biotechnology. 2017;35:319. doi:[10.1038/nbt.3838](https://doi.org/10.1038/nbt.3838).

6. Kuleshov MV, Jones MR, Rouillard AD, Fernandez NF, Duan Q, Wang Z, et al. Enrichr: a comprehensive gene set enrichment analysis web server 2016 update. Nucleic acids research. 2016;44:W90–7. doi:[10.1093/nar/gkw377](https://doi.org/10.1093/nar/gkw377).

7. Sergushichev A. An algorithm for fast preranked gene set enrichment analysis using cumulative statistic calculation. bioRxiv. 2016;60012. doi:[10.1101/060012](https://doi.org/10.1101/060012).

8. Gentleman RC, Carey VJ, Bates DM, Bolstad B, Dettling M, Dudoit S, et al. Bioconductor: open software development for computational biology and bioinformatics. Genome Biology. 2004;5:R80. doi:[10.1186/gb-2004-5-10-r80](https://doi.org/10.1186/gb-2004-5-10-r80).
