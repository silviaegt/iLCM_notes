# Corpus Analysis with iLCM

Based on: https://ilcm.informatik.uni-leipzig.de/download/starting_guide.pdf


## 1.  Download the tool

1. Go to https://ilcm.informatik.uni-leipzig.de/software/download/
2. Download pre-requisites
	+ Docker CE:
		+ [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository)
		+ Windows
		+ Mac
	+ Docker Compose
	+ R (and perhaps also RStudio)
	
3. Dowload the Install_ilcm.zip 
4. 


## 2. Upload your corpus


### CSV
The first option is importing your data as a csv file, which can basically have any format, but they need to be stored in the directory: /home/username/.iLCM/data/import_data/
The csv files will then be displayed inside the import subtab. You have to choose one of them and then click the import button.


The second option is importing multiple text files, like .pdf, .txt, .doc, .docx, where every file is imported as a single document. The import is only possible, if the user has installed the app on his local machine. 


## 3. Explore your corpus

### Search

#### Simple Search

1. Select your corpus in "which corpus?"
2. Go to "Search Results" Window
3. Make a Search, the default option is "Simple search". Terms may be combined with boolean options such as: 
>\+ = AND ( "method + methodology" will yield results with both words, and so on)
\# = OR
\- = NOT
4. Once you've searched for a word or a group of terms using the flashcards above, your results will be shown in a table with ten headings

id | id_doc | score | dataset | section | 
-- | --| -- | -- | -- | 
?? | number you give to identify your document | ?? | name of your collection (format, good practices??) | is this only thought for newspapers data??



And




title | author | date  | token| keyword.and.context
-- | --  | -- | -- | -- |
name of your document | format?? | YYYY/MM/DD | ?? | only one occurrence by document??

#### Detailed (maybe)

#### Custom (??) 


### Time Series

Plot (describe options??)  / frequencies - raw (??)
Heatmap (download possiblities??)

### Document View

POS-Tagging (which algorithm, language default??)
Entity tags (same questions as above, also: can one train the data / use ML to improve results??)


### Facets

Didn't really understand what happens here

## 4. Work with your collection

First go to "Task Scheduler"; select your collection and the analysis you want to run

(didnt' understand what 
+ "Download Collection as CSV" does
+ Nor "Save Collection as token object"
+ Nor "Save Collection as meta object") 

### Topic Models

Algorithm??
Pre-processing??

### Term Frequency Extraction

### Dictionary Frequency Extraction

### Classification

### Co-occurrences

### Context Volatility

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NDk1NDE4NDMsNzc4NzQwNzM3LC0xOD
I3OTY0MSwtMTE1MDM3ODI1NSwtNDkzNTM4MDE3LC0yMDYzMzQ5
NDc2LDEyNjQ0OTc3MTAsMTEwMTY1OTM5NCw3NjA2OTI2NTldfQ
==
-->