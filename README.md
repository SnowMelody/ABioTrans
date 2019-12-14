## ABioTrans
A Biostatistical Tool for Transcriptomics Analysis

This tool is an extention to the original ABioTrans, with updated and newly implemented features. Credit goes to the contributors of the original implementation of ABioTrans, which can be found [here.](https://github.com/buithuytien/ABioTrans) 
A detailed user guide and test data for the original features can be accessed via the same link.


## Contents 
- [Getting started](#getting-started)</br>
  - [Prerequisites](#prerequisites)</br>
  - [Running the program](#running-the-program)</br>
- [Updated features](#updated-features)</br>
	- [Layout](#layout)</br>
	- [Heatscatter](#heatscatter)</br>
	- [Sparse PCA](#sparse-pca)</br>
- [New features](#new-features)</br>
	- [t-SNE directional plot](#t-sne-directional-plot)</br>
	- [t-SNE directional plot demo](#t-sne-directional-plot-demo)</br>
	- [Scatter overlay](#scatter-overlay)</br>
	- [Clustering with random forest](#clustering-with-random-forest)</br>
	- [Self-organising map (SOM)](#som)</br>
- [Additional notes](#additional-notes)</br>  


## Getting started

### Prerequisites
It is recommended to have the latest version of R and Python 3 installed. Python dependencies used are ```numpy```, ```pandas```, ```matplotlib```, ```scipy```, ```scikit-learn```, ```mplcursors``` and ```asdf```. They can be installed by running the following in command line: </br>

```
pip install numpy pandas matplotlib scipy scikit-learn mplcursors asdf
```

As for required R packages, they will be installed automatically when the tool is launched for the first time.

### Running the program
ABioTrans can now be launched via the shortcut instead of running the R script in RStudio. Simply copy the shortcut icon to your preferred location, double click it and you're good to go.


## Updated features

### Layout
The layout of ABioTrans has been reorganised into 4 tab headings: ```Home```, ```Preprocessing```, ```Original``` and ```New```. ```Original``` is a dropdown selection which contains all initial features and updates applied to them, while ```New``` contains newly added features.
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/Layout.png)

### Heatscatter
In the updated heatscatter, the plot can be navigated interactively. Hovering the mouse over a point displays the sample names and their corresponding values. Additionally, the plot can be zoomed in/out.
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/Heatscatter.png)

### Sparse PCA
In the updated PCA, an option has been added to toggle between using PCA or sparse PCA.
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/Sparse%20PCA.png)

## New features

### t-SNE directional plot
t-SNE directional plot is used to find the paths of samples across different time points. The script for the t-SNE directional plot utilises the preprocessing method from [DigitalCellSorter.](https://github.com/sdomanskyi/DigitalCellSorter) PCA is applied to the preprocessed data, then t-SNE on the PCA step. </br>
**Note: At the time of upload the script is no longer up-to-date with the latest release of DigitalCellSorter** </br>

The plot is currently only applicable **for samples with time points**. Samples have to be named in the format ```samplename_time```. Time can be in seconds ```s```, minutes ```min```, hours ```hr``` or days ```d```. All units will be automatically converted to minutes equivalent (if unspecified, minutes is taken as the default). Thus, *sample1_20s*, *sample1_2min*, *sample1_10* are all valid names. </br>

There are 3 parameters to control the t-SNE output. ```Perplexity value``` tweaks the position of points on the t-SNE plot. A suitable perplexity value usually ranges between 5 to 50. ```No. of PCs``` determines the number of principal components to retain in the PCA step. ```No. of clusters``` classifies the samples into the specified cluster size. </br>

The following keys can be used to interact with the generated t-SNE plot: </br>
```Left```, ```Right```, ```Left mouse click```: Find points on the plot </br>
```Enter```, ```Space```: Select a point </br>
```Shift```: Generate paths connecting time points of selected points </br>
```A```: Auto generate paths in a sequential manner </br>
```R```: Reset plot to default state </br>
```Esc```: Close plot </br>

t-SNE directional plots are saved in the ```tsne_output``` folder after each run.

### t-SNE directional plot demo
First, launch ABioTrans and open the ```test data``` folder. Under ABioTrans' ```Home``` tab, select ```Normalised file```. Load ```yeast_nm.csv``` as the normalised expression file and ```yeast_meta``` as the meta data file. Press on ```Submit``` once both files have been loaded. Next, click on the ```Preprocessing``` tab. Input **0** for ```Min. value``` and **1** for ```Min. columns```. Click on ```Submit``` and wait for the preprocessing to be done. Then, click on the ```New``` tab and choose ```t-SNE``` from the dropdown selection. Following which, input **25** for ```Perplexity value```, **4** for ```No. of PCs```, **6** for ```No. of clusters``` and **None** for ```Transformation```. Click on ```Submit```. The t-SNE plot once generated should as such:
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/t-SNE_1.png)

Feel free to interact with the plot. After generating paths of selected points, it might look like this:
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/t-SNE_2.png)
 

### Scatter overlay
By using the overlap of 2 scatter plots, differential genes from gene expression data can be identified. More information on the original implementation can be found [here.](https://github.com/SnowMelody/ScatterOverlay) </br>

There are 4 parameters to control the scatter plots. They correspond to the samples used in the x and y axes of the first and second scatter.
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/Overlay.png)

### Clustering with random forest
While generally used for classification and regression problems, here random forest is used for clustering. The plot can be navigated in a similar manner to the updated heatscatter. </br>

There are 2 parameters to control the random forest cluster plot. ```No. of trees``` defines the size of the forest. ```No. of clusters``` classifies the samples into the specified cluster size. </br>

The ```diff_genes.csv``` file will be generated after each run, containing names of differential genes.
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/Random%20forest.png)

### SOM
5 types of SOM plots are available for use: </br>
```Property```: Uses values of codebook vectors (weight of gene vectors) and output as coloured nodes </br>
```Count```: Shows how many genes are mapped to each node </br>
```Codes```: Displays codebook vectors </br>
```Distance```: Shows how close genes are from each other when they are mapped </br>
```Cluster```: Uses hierarchical clustering to cluster the SOM </br>

There are 4 parameters to control the SOM plots. ```Samples used``` determines the sample chosen for the plots, either all samples or individual ones. ```No. of horizontal grids``` and ```No. of vertical grids``` changes the number of nodes used in the SOM. ```No. of clusters```  classifies the SOM nodes into the specified cluster size (for cluster plot).
![alt text](https://github.com/SnowMelody/ABioTrans/blob/master/ABT_updated/screenshots/SOM.png)


## Additional notes
Technically, transformation is not necessary for t-SNE, random forest or SOM. It is simply left in for those interested to see how it affects the output.
