# ChIPchip-analysis
R code for analyzing ChIPchip data generated using the Agilent 4x44k yeast platform 

This program has been made for analysis of Agilent microarray 4x44k format containing probes covering the S. cerevisiae genome. 
The analysis process has been described in the following publication: Sommermeyer V., Béneut C., Chaplais E., Serrentino M. E. and Borde V. (2013) Spp1, a member of the Set1 complex, promotes meiotic DSB formation in promoters by tethering histone H3K4 methylation sites to chromosome axes. Mol. Cell 49, 43-54. 

1. Copy the entire "Signal_processing" Folder onto your computer.
The "Common" folder contains three subfolders: the "Coord files" folder, containing files that will be used by the script; the "GPR files" where you should put your raw data tables files in the GPR (GenePix Results) format; the "Tables files", if your files are in a tab-deliminted text format.
2. Add your files to be processed to the "Common folder"
The "Signal Processing" folder contains the main script "SignalProcessingMain". The "Other files" folder contains the scripts used by "SignalProcessingMain". The "Saved files" contains the Processed table files and the pdf graphs that will be generated upon the analysis by "SignalProcessingMain".
3. Install the TOSCA_1.1 package in R
4. Open the "SignalProcessingMain" file. You can run it with the default parameters or change any of them. Add the name of your .gpr or .txt files after "arrayfile=".
Copy the whole content of the "SignalProcessingMain" file into the R programm.

The results will be in the "Saved files" folder.

Explanations for the processed data table contents: 
"First column"  #AgilentRef Number

"Ratio1"         Ratio of the first array

"Ratio2"         Ratio of the second array

"MeanRatio"      Mean of the two Ratios (or Ratio1 if there is only one array)

"Chromosome"     Chromosome number

"Position"       Position of the middle of the probe on the chromosome, in bp

"RatioNorm"      Ratio obtained after the normalization step (Dividing all the ratio values by the mean of the 10% lowest ratios)

"RatioDenoised"  (=RatioSmooth) This column is only used in the script for the generation of pdf file called "Denoising"

"RatioSmooth"    Obtained by using successively the Denoising and the TOSCA package smoothArray functions on RatioNorm

"RatioSmoothed1" =RatioSmooth if smooth=1; if smooth=2, it idicates the ratio after two successive rounds of smoothing using smoothArray function

"Sites"          Indicates a probe with a peak adjacent to another probe with a peak. In this case, the same rank is given to the two adjacent probes because they likely correspond to a single peak. To obtein the final number of peaks, the number of probes with a value in the "Sites" column different than NA are removed

"Peaks"          Is egal to 1 if we consider there is an enrichment peak on the concerned probe with our Signal Processing criteria and threshold, NA if no peak

"PeakOrders"     If the column Peaks value is of 1 on the probe, PeakOrders is the rank of peaks' RatioSmooth (1 for the highest peak)
