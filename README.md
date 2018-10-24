# Corpus Analysis with iLCM


cravioto y varela (dos documentos que estaban vacíos)
Based on: https://ilcm.informatik.uni-leipzig.de/download/starting_guide.pdf


## 1.  Download the tool

### Preparation

1. Go to https://ilcm.informatik.uni-leipzig.de/software/download/
2. Download pre-requisites
	+ Docker CE:
		+ [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository)
		• `sudo apt install docker.io`
		• `sudo systemctl start docker`
		• `sudo systemctl enable docker`
		• `docker --version` (with this you confirm you have docker installed) 
		+ [Windows 10 Pro](https://store.docker.com/editions/community/docker-ce-desktop-windows) -- you will need to create an account and log in
		+ Windows 10 Home -- you will need to install [DockerToolbox](https://docs.docker.com/toolbox/toolbox_install_windows/); to check your installation has been sucessful click [here](https://docs.docker.com/toolbox/toolbox_install_windows/#step-3-verify-your-installation) (you might need to uninstall and install again your VirtualBox)
		+ Mac
	+ Docker Compose (**Docker Toolbox** already includes Compose)
	+ R (and perhaps also RStudio)

Tip:
For commodity you can type the following commands in order to 
• sudo groupadd docker
• sudo usermod -aG docker $USER

3. Dowload the Install_ilcm.zip 

### Installing the tool

#### Downloading
1. Download the zip file (install_iLCM.zip) 
2. Copy the iLCM folder in your "home"
	+ Linux: /home/christian/ paste here and then add permissions with `sudo chmod -R 777 /home/christian/iLCM/`
	+ Windows: C:/User/christian/
		+ Right click your folder, select "Properties", go to "Security" and add "Everyone" to the group of users that can edit this folder (Number of groups or users -- Edit -- write "Everyone" in the empty box, then click Add and afterwards make sure you click all boxes in the Permissions section)
	+ Mac: /Users/christiankahmann/

#### Setting docker
3. Do your docker-compose
	3.1 Open your terminal / Powershell
	3.2 Open your tmca folder*
	3.3 Then type: `docker-compose up -d`
	3.4 Proof if everything was downloaded properly with `docker ps`
> \* Windows: something like `cd
>C:\Users\username\Documents\Install_iLCM\Install_iLCM\tmca`(cd =change
> directory)



Make sure you have enough space in your system, if not, it is better to change your docker to your home directory you can do this by following this instructions: https://linuxconfig.org/how-to-move-docker-s-default-var-lib-docker-to-another-directory-on-ubuntu-debian-linux

ExecStart=/usr/bin/dockerd -g /home/myname/docker -H fd://

#### Setting Solr
4. Tell Solr which configuration to use `docker exec -i --user=solr tmca_solr-1_1 bin/solr zk upconfig -n iLCM -d /store/solr/config/iLCM`
5. Initialise Solr: http://localhost:8081/solr/admin/collections?action=CREATE&collection.configName=iLCM&maxShardsPerNode=1&name=iLCM&numShards=1&replicationFactor=1&router.name=compositeId&routerName=compositeId&wt=json

> If you're a Windosws Home user you should type:
> http://192.168.99.100:8081/solr/admin/collections?action=CREATE&collection.configName=iLCM&maxShardsPerNode=1&name=iLCM&numShards=1&replicationFactor=1&router.name=compositeId&routerName=compositeId&wt=json

Remember to clic `docker-compose stop` to close your docker session (your data will be still there when you come back)

****

6. ?? Didn't find ---- `install_ilcm_toolbox.R`   
7. Run the docker_commands.R commands in the docker-console by hand.
	+ ?? Had problems with: `$ docker pull ckahmann/ilcm_r:latest`
		+ Problem:     Error response from daemon: manifest for ckahmann/ilcm_r:latest not found
		+ Sollution:
     `$ docker pull ckahmann/ilcm_r:0.91` (folllowing the name of the tag: https://hub.docker.com/r/ckahmann/ilcm_r/tags/)  -- although I did have time out problems (??)
     + ?? Also: couldn't do `$ cd Downloads/Install_ilcm` (in the instructions it's called install_ilcm but the downloaded file is written with capital I)
	     + Problem: `bash: cd: Downloads/Install_ilcm: No such file or directory` 

##Collection Worker

The Collection Worker is the tab where the user starts various NLP algorithms. Also the results of the started analysis can be accessed in the Collection Worker.

##Categories

In the Categories tab the user can have a closer look at the made annotations, create new annotation schemes or create further annotations.


##Scripts

Here the user is offered 3 functionalities. First, if the user is familiar with R, he can type R-commands, which are then executed. This can be useful for debugging or reconfiguring some default settings. The second option is given by the possibility of creating or manipulating blacklists. These can be used in the preprocessing chain when applying different NLP algorithms. The third option is changing the scripts of the NLP algorithms. The user should be enabled, to create different versions of the script. But he has to keep in mind though, that he has to produce the same output formats like the original script did. This is the case, because the result visualisation is dependent on certain variables and variable names.

##Importer

*****


## 2. Import your own Documents


If you're a Windows Home user, you have to set some parameters in your VirtualBox before you get here.



docker-machine start default 


http://192.168.99.100:3839/


In the Importer-tab the user can upload his own text data. The data will then be preprocessed and uploaded to the database and Solr.

### 2.1 CSV file
1. The input csv files need to be stored in the directory: `/home/username/.iLCM/data/import_data/` . 
For pre-processed data (iLCM style) it should be stored in "
2. The csv files will then be displayed inside the import subtab. You have to choose one of them and then click the import button.
3. Once the file is loaded into the tool, you can either check whether the data is imported correctly or directly start the mapping. 
-----

a) after pre-processing with R 
b) Upload your two csv files to your Rstudio Environment
c) then move them to ShinyApp -- TMCA -- Beipieldaten
d) Run your ILCM app
e) Go to importer upload selected data to DB 


### Metadata

In the database the texts are saved with certain metadata-fields. Very often they will not perfectly match the metadata the user has. Therefore you might want to use some given metadata fields for your purposes (e.g. publisher, section...). 
1. After clicking "Start Mapping" you will see two data tables. In the first one, the user needs to set the the mapping. In the header the metadata-fields of the database are given. In the rows the user can see the fields, which were found in the imported csv-file. Now its the users task to find the right mapping. In this example you can see, that the body-database column is mapped to the "text"-field of the csv-file. 
2. Sometimes the user does not always have the metadata included in the csv file. Then one has 2 other possibilities on how to get the data into the iLCM database. 
	* The first one is writing some R-commands in a short script, for a certain database column. Here the column "title"" is filled by using the word "speechnumber" pasted together with the values in the column "speechnumber" of the csv file. For other metadata fields like publisher or type, its sometimes the same value for the whole dataset. If this is the case the user can just click the Type Button to input the value by hand. This value will then be used for all documents.
On the right side the user has to specify a language, the date-format and give an abbreviation for imported data.
It is necessary that the abbreviation and the id_doc field together form aunique key. So when uploading multiple csv files, which all belong to the same dataset (same abbreviation), the user needs to use unique id_doc values.
In the second table below, the user sees the Metadata input file being created, dependent on the decisions he made in the data table above. Once the user is sure everything is set correctly, he then has to click "Start Preprocessing and save csv-files" or "Start preprocessing and directly write to DB". In both options the imported data are preprocessed using Spacy and then saved as 2 csv files. Having clicked the second button, the data gets already imported in the database and Solr using the 2 created csv-files (token and meta).  
Once the user restarts the app (open the link in a new tab) the data will be available and ready to work.

### 2.2 Multiple text files
The input for multiple text files, is almost the same as for csv files. The only big difference is the fact, that for the text files only , to the fields: "id_doc", "title" and "text" exist. The other missing columns have to filled in by hand, if the user wants to include them. Otherwise he can also just leave them empty.(id_doc and body have to be non empty)

Once the import is succesful, the user can choose the dataset in the sidebar panel below the explorer button. It is possible to work on multiple datasets at the same time.



## 3. Explore your corpus

In this section the user can search the database, get extra information about the search results, annotate text, and in the end create a collection of documents, which serves as the starting point for further analysis.

?? What if one wants to search the whole corpus?
?? What if one wants to really "explore" (get most frequent words, tendencies, etc)

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
unique id the database gives to the document | number you give to identify your document | ?? | name of your collection (format, good practices??) | is this only thought for newspapers data??



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


### Edit your "blacklist"

Scripts -- 
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
eyJoaXN0b3J5IjpbLTE0Nzk4MDUxNjksLTUxNTY1MDc4MSw0NT
YwOTM5MDIsLTE4NzY2NDgyMzQsLTk5NDEyMjkxNywtNTk3NDA1
MDIyLC01OTU2MTIwMDMsLTE3MDgxOTA5MjEsLTIwMDQ3NzQ5NT
QsMzM5MjI4ODM3LDIyMTUwOTAxNCwtMTc5NzEzMjM0OCwtMTU1
Mjk5MzkzMCw0ODQxNjAwMDcsLTI1NzI4ODI3NCwxNjMwODE4ND
k4LDE2OTI5MjU4MywtMTQ5NjczMDM3NywtMTM3NjQ1MTc3Myw2
NDc3MDk1MTZdfQ==
-->