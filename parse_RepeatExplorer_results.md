# Parse RepeatExplorer results

## **1. Prerequisites**

- Results of RepeatExplorer analyses obtained from the version running on Galaxy  
- python  
- R (and basic knowlege of it if you want to customize the graphs)  
- basic unix knowledge  

## **2. Parsing results from multiple individual analyses**

### Summarize the results of all species in a single file

Open a terminal and type the following command:
```
python RE_output-parsing_individual.py input-directory-name output-name species_table_output_name t
```
To make it easier, put the input directory and the python script in a same directory.  
**input-directory-name** is the directory with the cluster tables of all species. DO NOT put anything else in this directory!  
The cluster tables have to be renamed this way (note the double underscore): **Genus_species__ReadsNumber_GenomeSize_CLUSTER_TABLE.csv**  
**output-name** is the name you want to give to the file where all results will be reported, for instance RE_output_individual.txt  
**species_table_output_name** is the name you want to give to the file where the script will make a species table with genome sizes and read numbers (useful for R later), for instance species_table_individual.txt  
**t** is the threshold to keep a second hit in the table: we keep the hit if its score is at least t times as high as the score of the first hit. t can be between 0 and 1 (see inside script for details)  
  
  
### Manualy check the results of all species at once
- Open the results in excel and have a look at them, label the sheet "original"  
- Copy the results in a new sheet called "edited"  
- Edit manually the Supercluster classification if necessary (check if can improve the classification level of the "All" ones, check if the classification is ok when the number of hits is very low)  
- Copy the edited dataset in a new sheet called "levels"  
- Remove all columns after the "Supercluster_best_hit" column  
- Use the "text to columns" function to split the "Supercluster_best_hit" column using "/" as a delimiter  
- Relabel the "Supercluster_best_hit" column as "Supercluster_best_hit_lev1" column, and label all newly created columns as "Supercluster_best_hit_lev2", "Supercluster_best_hit_lev3", ... (use these exact names!)
- Save the whole workbook as "RE_parsing_test.xls" (or any other name)  
- Save the "levels" sheet as "RE_parsing_test_levels.txt" (or any other name) in **tab delimited** format  

### Produce graphs
See the R script and instructions in it.


## **3. Parsing results from one comparative analysis**


### Summarize the results
Type the following command in a terminal: 
```
python RE_output-parsing_comparative.py CLUSTER_TABLE.csv COMPARATIVE_ANALYSIS_COUNTS.csv output-name t
```
To make it easier, put all input files and the python script in the same folder.  
**output-name** is the name you want to give to the file where all results will be reported, for instance RE_output_comparative.txt  
**t** is the threshold to keep a second hit in the table: we keep the hit if its score is at least t times as high as the score of the first hit. t can be between 0 and 1 (see inside script for details) 


### Manualy check the results:
- Open the results in excel and have a look at them, label the sheet "original"  
- Copy the results in a new sheet "edited"  
- Edit manually the Supercluster classification if necessary (check if can improve the classification level of the "All" ones, check if the classification is ok when the number of hits is very low)  
- Copy the edited dataset in a new sheet "levels"  
- Remove all columns after the "Supercluster_best_hit" column  
- Use the "text to columns" function to split the "Supercluster_best_hit" column using "/" as a delimiter  
- Relabel the "Supercluster_best_hit" column as "Supercluster_best_hit_lev1" column, and label all newly created columns as "Supercluster_best_hit_lev2", "Supercluster_best_hit_lev3", ... (use these exact names!)  
- Save the whole workbook as "RE_parsing_test.xls" (or any other name)    
- Save the "levels" sheet as "RE_parsing_test_levels.txt" (or any other name) in **tab delimited** format  

### Make a table with species information

Make a **tab delimited** table called "species_table.txt" (for instance) following this structure, and with the same headers:

species	code	genome_size
P_sobolifera	PSO	7.015
P_brevipes	PBR	15.525

### Produce graphs
See the R script and instructions in it.
