# Viralrecall Postscreen: A tool for processing ViralRecall outputs

This tool relies heavily on criteria developed by [Aylward et al](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.3001430) as well as the program [ViralRecall](https://github.com/faylward/viralrecall). 

## What it does

This program will take output files from ViralRecall ( a program that finds viral signatures in omic data) and use them to label metagenomic bins as NCLDV or not as well as identify potential non-viral contamination int he bins. 

## How to Use

1) Run [NCLDV markersearch](https://github.com/faylward/ncldv_markersearch) on all of the protein files for all of your metagenomic bins. Protein files can be prodigal outputs. 
*make sure you select all of the marker genes to be displayed in your output table as well as using the -a flag for all hits. 
2) Run Viral Recall on all of your bins. A description of how to do this in batch can be found on the ViralRecall github page. (Make sure it is running with -c flag for contig) 
3) Gather all the summary files into a single folder
4) Run Viralrecall_postscreen.py
`python viralrecall_postscreen.py ncldv_markersearch_output.tsv input_folder_of_summaries`

## Interpreting results

genome: your bin name
GVOGmxxxx: different NCLDV marker genes (can be identified on NCLDV markersearch github.
Virus: either 'yes' or 'no' depending on if overall viral recall score is positive or negative.
Contamination: number of contigs that have a negative score
Sum_score: The sum viral recall score (higher scores mean more likely to be a giant virus)
Total_contigs: The total number of contigs in the given bin.
Percent negative: Percent of contigs that are negative viral recall scores.
PolB: 'yes' or 'no' based on whether or not the bin has a polB marker gene.
Other markers: Number of other important marker genes identified by the Aylward et al. paper. 

## Is your bin a giant virus? 

This ultimately is subjective, but you can have confidence that your bin is a giant virus if
1) It contains a NCLDV PolB
2) It has a positive Sum_score
3) It has at least a score of 3 other markers

After identifying potential Giant virus bins, you can remove the contamination and contigs with negative scores from the bins for a more refined bin. 
