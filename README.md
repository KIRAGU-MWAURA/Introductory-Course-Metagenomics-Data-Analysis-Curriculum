# Metagenomics Data analysis using Qiime 2

This an easy curriculum on using Qiime 2 for microbiome data analysis.

# TABLE OF CONTENT
1. [INTRODUCTION](https://github.com/KIRAGU-MWAURA/Metagenomics-Data-Analysis-Curriculum/tree/Joyce_dev#introduction)
2. [INSTALLING QIIME 2](https://github.com/KIRAGU-MWAURA/Metagenomics-Data-Analysis-Curriculum/tree/Joyce_dev#installing-qiime2)
3. [QIIME 2 BASIC COMMANDS](https://github.com/KIRAGU-MWAURA/Metagenomics-Data-Analysis-Curriculum/tree/Joyce_dev#qiime-2-command-line-interface)
4. [UNDERSTANDING HOW QIIME 2](https://github.com/KIRAGU-MWAURA/Metagenomics-Data-Analysis-Curriculum/tree/Joyce_dev#understanding-qiime)
5. [ABOUT OUR TEST DATA ]()
6. [DEMULTIPLEXING]()
7. [QUALITY CONTROL]()
8. [FEATURE TABLE CONSTRUCTION]()
9. [GENERATING A TREE FOR PHYLOGENETIC DIVERSITY ANALYSIS]()
10. [ALPHA AND BETA DIVERSITY ANALYSIS]()
11. [TAXONOMIC ANALYSIS]()

## INTRODUCTION
<details>
<summary> Tutorial introduction </summary>




- Qiime 2 is a platform for processing, analyzing, and visualizing microbiome data. 


- In this tutorial We will do an analysis of human microbiome samples from two indivuduals at four body sites and at five timepoints, the first of which immediately followed antibiotic usage.These were sequenced on an Illumina HiSeq using the Earth Microbiome Project hypervariable region 4 (V4) 16S rRNA sequencing protocol.

- QIIME 2 can also process other types of microbiome data, including amplicons of other markers such as 18S rRNA, internal transcribed spacers (ITS), and cytochrome oxidase I (COI), shotgun metagenomics, and untargeted metabolomics [[1]]() 


</details>





## INSTALLING QIIME 2 

<details>
<summary>Installing Qiime with conda environment</summary>
This is the recommended way to install qiime2


1. First you have to install Miniconda by running the following command:

 ```
bash Miniconda3-latest-Linux-x86_64.sh 

```




- Follow the prompts on the screen, set everything to default if you are not sure of anything.


- close and open your terminal for the changes to take place.


- Run `conda list` to see the conda packages installed.

```
conda list
```
Output
```
# packages in environment at /home/ben/miniconda3:
#
# Name                    Version                   Build  Channel
_libgcc_mutex             0.1                        main  
_openmp_mutex             5.1                       1_gnu  
brotlipy                  0.7.0           py39h27cfd23_1003  
ca-certificates           2022.4.26            h06a4308_0  
certifi                   2022.5.18.1      py39h06a4308_0  
cffi                      1.15.0           py39hd667e15_1  
charset-normalizer        2.0.4              pyhd3eb1b0_0  
conda                     4.13.0           py39h06a4308_0  
conda-package-handling    1.8.1            py39h7f8727e_0  
cryptography              37.0.1           py39h9ce1e76_0  
idna                      3.3                pyhd3eb1b0_0  
ld_impl_linux-64          2.38                 h1181459_1  
libffi                    3.3                  he6710b0_2  
libgcc-ng                 11.2.0               h1234567_1  
libgomp                   11.2.0               h1234567_1  
libstdcxx-ng              11.2.0               h1234567_1  
ncurses                   6.3                  h7f8727e_2  
openssl                   1.1.1o               h7f8727e_0  
pycosat                   0.6.3            py39h27cfd23_0  
pycparser                 2.21               pyhd3eb1b0_0  
pyopenssl                 22.0.0             pyhd3eb1b0_0  
pysocks                   1.7.1            py39h06a4308_0  
python                    3.9.7                h12debd9_1  
readline                  8.1.2                h7f8727e_1  
requests                  2.27.1             pyhd3eb1b0_0  
ruamel_yaml               0.15.100         py39h27cfd23_0  
setuptools                61.2.0           py39h06a4308_0  
sqlite                    3.38.3               hc218d9a_0  
tk                        8.6.12               h1ccaba5_0  
tqdm                      4.64.0           py39h06a4308_0  
tzdata                    2022a                hda174b7_0  
urllib3                   1.26.9           py39h06a4308_0  
xz                        5.2.5                h7f8727e_1  
yaml                      0.2.5                h7b6447c_0  
zlib                      1.2.12               h7f8727e_2  

```
- Update conda

```
conda update conda
```

Output
```
Collecting package metadata (current_repodata.json): done
Solving environment: done

# All requested packages already installed.

```
[More information on installing conda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)

3. Download the .yml file for Qiime 2 by running the following command:
```
wget https://data.qiime2.org/distro/core/qiime2-2022.2-py38-linux-conda.yml
```
5. Create a conda environment with the .yml file you downloaded 
You can use any name for your conda environment.
Here we are just going to name our environment as qiime2

```
conda env create -n qiime2 --file qiime2-2022.2-py38-linux-conda.yml

```
6. Activate the conda environment
```
conda activate qiime2

```
7. Test your installation by running:
```
qiime --help

```
Output:

```
qiime --help
Usage: qiime [OPTIONS] COMMAND [ARGS]...
```
To get help more with QIIME 2, visit [https://qiime2.org](https://qiime2.org)


You have successfully installed QIIME 2!

</details>




  

  

  



## QIIME 2 COMMAND LINE INTERFACE
<details>
<summary>Basic commands in Qiime 2</summary>

- Inorder to use qiime it is important to familiarize with the basic commands in qiime.

- To see a list of available commands run:

```
qiime
```
- You will see several subcommands listed, including plugin commands (e.g. feature-table, diversity) and built-in commands (e.g. info, tools).

- To See plugins installed and other information about your deployment run:
```
qiime info

```

- Use `--help` with any command to see what that command does for example:

```
qiime feature-table --help
```
Output
```
Usage: qiime feature-table [OPTIONS] COMMAND [ARGS]...

  Description: This is a QIIME 2 plugin supporting operations on sample by
  feature tables, such as filtering, merging, and transforming tables.

  Plugin website: https://github.com/qiime2/q2-feature-table

  Getting user support: Please post to the QIIME 2 forum for help with this
  plugin: https://forum.qiime2.org

Options:
  --version            Show the version and exit.
  --example-data PATH  Write example data and exit.
  --citations          Show citations and exit.
  --help               Show this message and exit.

Commands:
  core-features                  Identify core features in table
  filter-features                Filter features from table
  filter-features-conditionally  Filter features from a table based on
                                 abundance and prevalence

  filter-samples                 Filter samples from table
  filter-seqs                    Filter features from sequences
  group                          Group samples or features by a metadata
                                 column

  heatmap                        Generate a heatmap representation of a
                                 feature table

  merge                          Combine multiple tables
  merge-seqs                     Combine collections of feature sequences
  merge-taxa                     Combine collections of feature taxonomies
  presence-absence               Convert to presence/absence
  rarefy                         Rarefy table
  relative-frequency             Convert to relative frequencies
  rename-ids                     Renames sample or feature ids in a table
  subsample                      Subsample table
  summarize                      Summarize table
  tabulate-seqs                  View sequence associated with each feature
  transpose                      Transpose a feature table.
```



- To improve qiime usability and efficiency if you are using Bash, to enable tab auto-completion run:
```
source tab-qiime
```
- You can add this command your .bashrc/.bash_profile to avoid running it every time you open a new terminal and activate your qiime 2 conda environment.

- To verify that tab completion is working try running `qiime i` and press tab it should auto complete to `qiime info`


</details>



## UNDERSTANDING QIIME
<details>
<summary>Important Definitions</summary>
**ARTIFACTS** - Instead of normal data files qiime uses artifacts as the data files. These contain the actual data and the metadata. The metadata describes things about the data, such as its type, format, and how it was generated. Artifacts have `.qza` file extension.

**VISUALIZATIONS** - This are terminal outputs and cannot be used as inputs. for example statistical result tables and static images. Visualizations have `.qzv` file extension


**SEMANTIC TYPES** -These enable Qiime 2 to identify artifacts that are suitable inputs to an analysis for example, if an analysis requires distance matrix as input Qiime 2 will detect the semantic type of the artifacts with distance matrix to avoid incompatible artifacts from being used in the analysis.

**PLUGINS** -These are like 'flags' for softwares that can be used with Qiime. eg `q2 -demux ` for dimultiplexing

**METHODS AND VISUALIZERS** - Qiime 2 plugins define methods and visualizers that are used for analyses 
A method accepts some combination of Qiime 2 artifacts and parameters as input and produces one or more artifacts as output.
A visualizer accepts some combination of Qiime 2 artifacts as input but the output of a visualizer cannot be used as an input.

*NB Artifacts and visualizations are data files, pipelines methods and visualizers are actions*

[Additional information about key terms used in Qiime 2](https://docs.qiime2.org/2022.2/glossary/)

**A visual overview of how Qiime 2 works**
![qiime workflow](https://docs.qiime2.org/2022.2/_images/key.png)




</details>







##  ABOUT THE TEST DATA 
<details>
<summary>Understanding the test data</summary>

The data is obtained from [Moving pictures tutorial](https://docs.qiime2.org/2022.2/tutorials/moving-pictures/#moving-pics-diversity)

- An analysis of human microbiome samples from two indivuduals (subject-1 and subject-2) 
- At four body sites (gut,tongue left palm, right palm)
- At five timepoints, the first of which immediately followed antibiotic usage. (day 0 , day 84, day 112, day 140, day 168)
- These were sequenced on an Illumina HiSeq using the Earth Microbiome Project hypervariable region 4 (V4) 16S rRNA sequencing protocol.

*NB Bacterial 16S ribosomal RNA (rRNA) genes contain nine “hypervariable regions” (V1 – V9) that demonstrate considerable sequence diversity among different bacteria.* [(2)]()

[Explore the sample metadata here ](https://docs.google.com/spreadsheets/d/1I9TzFqkjQ9RvXMrP7StbWwMid5pjFN8exYC7nUVpKFs/edit#gid=0)


</details>


## GETTING STARTED!
<details>
<summar>The data analysis begins here</summary>
- First create a directory and move inside that directory, this is where we will do our analysis.

```
mkdir tutorial
```
```
cd tutorial
```

- To download the meta data as a tsv file (tab seperated version) run the following command:

```
wget \
  -O "sample-metadata.tsv" \
  "https://data.qiime2.org/2022.2/tutorials/moving-pictures/sample_metadata.tsv"
  
  ```
  
  
  Create emp-single-end-sequences directory and move inside it. This where we are going to download our data.
  ```
  mkdir emp-single-end-sequences
  ```
  
  ```
  cd emp-single-end-sequences
  ```
  
  Downloading the data
  ```
  wget https://data.qiime2.org/2022.2/tutorials/moving-pictures/emp-single-end-sequences/barcodes.fastq.gz
  
```
Output:

```
--2022-06-26 16:35:05--  https://data.qiime2.org/2022.2/tutorials/moving-pictures/emp-single-end-sequences/barcodes.fastq.gz
Resolving data.qiime2.org (data.qiime2.org)... 54.200.1.12
Connecting to data.qiime2.org (data.qiime2.org)|54.200.1.12|:443... connected.
HTTP request sent, awaiting response... 302 FOUND
Location: https://s3-us-west-2.amazonaws.com/qiime2-data/2022.2/tutorials/moving-pictures/emp-single-end-sequences/barcodes.fastq.gz [following]
--2022-06-26 16:35:10--  https://s3-us-west-2.amazonaws.com/qiime2-data/2022.2/tutorials/moving-pictures/emp-single-end-sequences/barcodes.fastq.gz
Resolving s3-us-west-2.amazonaws.com (s3-us-west-2.amazonaws.com)... 52.92.208.104
Connecting to s3-us-west-2.amazonaws.com (s3-us-west-2.amazonaws.com)|52.92.208.104|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3783785 (3.6M) [application/x-gzip]
Saving to: ‘barcodes.fastq.gz’

barcodes.fastq.gz                   100%[=================================================================>]   3.61M   203KB/s    in 57s     

2022-06-26 16:36:08 (64.8 KB/s) - ‘barcodes.fastq.gz’ saved [3783785/3783785]
```



  Downloading the data
  ```
  wget https://data.qiime2.org/2022.2/tutorials/moving-pictures/emp-single-end-sequences/sequences.fastq.gz

  ```
  Output
  ```
  --2022-06-26 16:39:08--  https://data.qiime2.org/2022.2/tutorials/moving-pictures/emp-single-end-sequences/sequences.fastq.gz
Resolving data.qiime2.org (data.qiime2.org)... 54.200.1.12
Connecting to data.qiime2.org (data.qiime2.org)|54.200.1.12|:443... connected.
HTTP request sent, awaiting response... 302 FOUND
Location: https://s3-us-west-2.amazonaws.com/qiime2-data/2022.2/tutorials/moving-pictures/emp-single-end-sequences/sequences.fastq.gz [following]
--2022-06-26 16:39:09--  https://s3-us-west-2.amazonaws.com/qiime2-data/2022.2/tutorials/moving-pictures/emp-single-end-sequences/sequences.fastq.gz
Resolving s3-us-west-2.amazonaws.com (s3-us-west-2.amazonaws.com)... 52.92.176.224
Connecting to s3-us-west-2.amazonaws.com (s3-us-west-2.amazonaws.com)|52.92.176.224|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 25303756 (24M) [binary/octet-stream]
Saving to: ‘sequences.fastq.gz’

sequences.fastq.gz                  100%[=================================================================>]  24.13M   181KB/s    in 3m 30s  

2022-06-26 16:42:41 (117 KB/s) - ‘sequences.fastq.gz’ saved [25303756/25303756]

  ```
  
  Your emp-single-end-sequences directory after running the `ls` command should have:
  
  Output 
  ```
 barcodes.fastq.gz sequences.fastq.gz
```
  
### Importing data as qiime 2 artifacts
- All data must imported as Qiime 2 artifacts to be used by a Qiime 2 action

- Users may use A Qiime 2 workflow in different stages eg.most may have raw data eg. FASTQ or FASTA which should be imported appropriately. Some may start with dimultiplexing data or a feature table

- Importing the data as qiime2 artifacts make sure you are in the tutorial directory ( Remember artifacts= data+metadata. This is what importing does; simply combining the data and metadata into a .qza file)

 ```
  qiime tools import   --type EMPSingleEndSequences   --input-path emp-single-end-sequences   --output-path emp-single-end-sequences.qza
```
Output:
```
Imported emp-single-end-sequences as EMPSingleEndDirFmt to emp-single-end-sequences.qza
```


To confirm your import worked as expected run:
```
qiime tools peek emp-single-end-sequences.qza
```
 Output:
 ```
 UUID:        9b85ed65-b169-4387-a994-9fc653b25613
Type:        EMPSingleEndSequences
Data format: EMPSingleEndDirFmt

```


</details>


## DEMULTIPLEXING
<details>
<summary>Demultiplexing the samples</summary>
During sequencing multiple samples are sequenced in a single lane (Multiplexing) Each sequence has a unique barcode corresponding to the sample it came from. In this step we want to know which barcode belong to each sample.

To demultiplex the sequences in our case single reads we run the command:
```
qiime demux emp-single --i-seqs emp-single-end-sequences.qza --m-barcodes-file sample-metadata.tsv --m-barcodes-column barcode-sequence --o-per-sample-sequences demux.qza --o-error-correction-details demux-details.qza

```

Output:
```
Saved SampleData[SequencesWithQuality] to: demux.qza
Saved ErrorCorrectionDetails to: demux-details.qza
```
- When you `ls ` tutorial directory you should see `demux-details.qza`  `demux.qza ` files

- We need to Generate a demultiplexing summary result file which we can view. This is important to determine how many sequences were obtained per sample, and also to get a summary of the distribution of sequence qualities at each position in your sequence data.

Command:
```
  qiime demux summarize --i-data demux.qza --o-visualization demux.qzv
  
  ```
  In your tutorial directory you should have `demux.qzv` file.
  
  To view:
 ```
 qiime tools view demux.qzv
```

- This should open a html file in your browser which you can view the demultiplexing results.
- 
 ![demux1](https://github.com/Wangari-Joyce/Qiime2_Tutorial/blob/main/demux1.png)
 
 ![demux2](https://github.com/Wangari-Joyce/Qiime2_Tutorial/blob/main/bar_graph_demux.png)
 
![demux3](https://github.com/Wangari-Joyce/Qiime2_Tutorial/blob/main/afterbar_graph1demux.png)

![demux4](https://github.com/Wangari-Joyce/Qiime2_Tutorial/blob/main/after_bar_graph2_demux_result.png)
  
  

</details>


  ## SEQUENCE QUALITY CONTROL 
  <details>
  <summary>Sequence quality control using dada2</summary>
  Inorder to remove low quality regions we will use the interactive plot in the `demux.qzv` file  to figure out which parameters to use
  
  ![interactive demux plot](https://github.com/Wangari-Joyce/Qiime2_Tutorial/blob/main/interactive_demux_plot.png)
  
  - From the plot we can see that the begining of the sequence has high quality scores which begins to drop around 120 bases
  - On the left side we are not going to trim any bases. We truncate from 120bases upwards
  - We are going to use the dada 2 denoise plugin for single end reads
  * The dada2 plugin does the following:
   * 1. Filters and trims the reads
   * 2. Finds the most likely original reads in the sequence
   * 3. Removes chimeras
   * 4. Counts the abundance
  ```
  qiime dada2 denoise-single --i-demultiplexed-seqs demux.qza --p-trim-left 0 --p-trunc-len 120 --o-representative-sequences rep-seqs-dada2.qza --o-table table-dada2.qza --o-denoising-stats stats-dada2.qza
  ```
  Output
  ```
Saved FeatureTable[Frequency] to: table-dada2.qza
Saved FeatureData[Sequence] to: rep-seqs-dada2.qza
Saved SampleData[DADA2Stats] to: stats-dada2.qza
```

  To view we need to convert the artifacts produced to .qzv files
  ```
 qiime metadata tabulate  --m-input-file stats-dada2.qza  --o-visualization stats-dada2.qzv
 ```
 To view `stats-dada2.qzv`:
 ```
 qiime tools view stats-dada2.qzv
 ```
 - This will open a html file in your browser.

Rename the files for easier identification.
```
mv rep-seqs-dada2.qza rep-seqs.qza
```
```
mv table-dada2.qza table.qza
```
</details>

## FEATURE TABLE CONSTRUCTION
<details>
<summary>Feature table and feature data summaries</summary>

- The `feature-table summarize` command output is a visualization file `table.qzv` which contains information on how many sequences are associated with each sample and with each feature also histograms for those distributions and related summary statistics

The `feature-table tabulate seqs` command out is a visualization file `rep-seqs.qzv` which contains a mapping of feature IDs to sequences, and provide links to easily BLAST each sequence against the NCBI nt database.

```
qiime feature-table summarize --i-table table.qza --o-visualization table.qzv --m-sample-metadata-file sample-metadata.tsv 

```
Output

```
Saved Visualization to: table.qzv
```


```
qiime feature-table tabulate-seqs --i-data rep-seqs.qza --o-visualization rep-seqs.qzv
```
Output
```
Saved Visualization to: rep-seqs.qzv
```

To view:
```
qiime tools view table.qzv
```
```
qiime tools view rep-seqs.qzv
```

  
</details>
  
 
  
  

## GENERATING A PHYLOGENETIC TREE FOR DIVERSITY ANALYSIS
<details>
<summary>Generating a phylogenetic tree </summary>

- The diversity metrics in the next steps require a phylogenetic tree relating the features to one another

- To generate the tree run the following command: 

```
qiime phylogeny align-to-tree-mafft-fasttree  --i-sequences rep-seqs.qza --o-alignment aligned-rep-seqs.qza --o-masked-alignment masked-aligned-rep-seqs.qza --o-tree unrooted-tree.qza --o-rooted-tree rooted-tree.qza
```
Output:
```
Saved FeatureData[AlignedSequence] to: aligned-rep-seqs.qza
Saved FeatureData[AlignedSequence] to: masked-aligned-rep-seqs.qza
Saved Phylogeny[Unrooted] to: unrooted-tree.qza
Saved Phylogeny[Rooted] to: rooted-tree.qza
```
</details>


## ALPHA AND BETA DIVERSITY ANALYSIS
<details>
<summary>Computing the core metrics </summary>

**ALPHA DIVERSITY**
This refers to the diversity within a single sample

**BETA DIVERSITY**
This refers to diverstity between different samples


- Here we use the `core-metrics-phylogenetic` command which computes several alpha and beta diversity metrics, and generates principle coordinates analysis (PCoA) plots using Emperor for each of the beta diversity metrics.
- An important parameter that should be provided is the `--p-sampling-depth` because most of the diversity metrics are sensitve to the sampling depth. if for example you choose a sampling depth of 500 any sample below 500 will be dropped from the analysis.
- The value for the sampling depth can be chosen by looking at the `table.qzv` html file in the interactive sample detail tab. 
- Here we chose 1103 as our sampling depths where only 3 samples will be dropped from the analysis.


```
qiime diversity core-metrics-phylogenetic \
  --i-phylogeny rooted-tree.qza \
  --i-table table.qza \
  --p-sampling-depth 1103 \
  --m-metadata-file sample-metadata.tsv \
  --output-dir core-metrics-results
```
Output:
This will be saved in the `core-metrics-results` directory.
The contents of this directory should be as follows:
```
bray_curtis_distance_matrix.qza  jaccard_distance_matrix.qza   shannon_vector.qza                      weighted_unifrac_emperor.qzv
bray_curtis_emperor.qzv          jaccard_emperor.qzv           unweighted_unifrac_distance_matrix.qza  weighted_unifrac_pcoa_results.qza
bray_curtis_pcoa_results.qza     jaccard_pcoa_results.qza      unweighted_unifrac_emperor.qzv
evenness_vector.qza              observed_features_vector.qza  unweighted_unifrac_pcoa_results.qza
faith_pd_vector.qza              rarefied_table.qza            weighted_unifrac_distance_matrix.qza


```

After computing the core metrics we can explore the microbial composition in context of the metadata
we will start with alpha diversity.
In alpha diversity several metrics are computed:
1. Observed features - computes the richness ,that is how many different 'things' or features are observed
2. Faith's phylogenetic richness - tells us about the shared phylogenetic history
3. Pielou's Evenness - tells us how many of each different 'thing' or feature is present
4. Shannon diversity - this is a measure of both evenness and richness




```
qiime diversity alpha-group-significance   --i-alpha-diversity core-metrics-results/faith_pd_vector.qza   --m-metadata-file sample-metadata.tsv   --o-visualization core-metrics-results/faith-pd-group-significance.qzv




```
</details>



## References

1. [Estaki, M., Jiang, L., Bokulich, N. A., McDonald, D., González, A.,Kosciolek, T., Martino, C., Zhu, Q., Birmingham, A.,Vázquez-Baeza, Y., Dillon, M. R., Bolyen, E., Caporaso, J. G., &Knight, R. (2020). QIIME 2 enables comprehensive end-to-endanalysis of diverse microbiome data and comparative studies with
publicly available data. Current Protocols in Bioinformatics, 70,e100. doi: 10.1002/cpbi.100](https://currentprotocols.onlinelibrary.wiley.com/doi/full/10.1002/cpbi.100)

2. [Chakravorty S, Helb D, Burday M, Connell N, Alland D. A detailed analysis of 16S ribosomal RNA gene segments for the diagnosis of pathogenic bacteria. J Microbiol Methods. 2007 May;69(2):330-9. doi: 10.1016/j.mimet.2007.02.005. Epub 2007 Feb 22. PMID: 17391789; PMCID: PMC2562909.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2562909/)
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  









