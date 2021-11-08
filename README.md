# Wikidata Reference Statistics

This repository contains the materials of the **[Reference Statistics in Wikidata Topical Subsets, 2nd Wikidata Workshop with ISWC 2021](http://ceur-ws.org/Vol-2982/paper-3.pdf)** paper. The embeddings are:

 - **Query Results:** The output of SPARQL queries for each experiment.
 - **Scripts:** The Python script used to enrich WDumper specification files with sub-classes and the jupyter notebook for plotting the charts.
 - **SPARQL Queries:** SPARQL queries to fetch reference statistics from datasest.
 - **WDumper Specification Files:** The specification files for extracting topical subsets corresponding to 6 different WikiProjects via WDumper tool. There are two JSON file for each project. The first just contains the top-level classes. The second (with '_sub' suffix) has enriched by sub-classes. Experiments were done using the latter.
 - **ShEx schemata:** The Shape Exprision schemas of the 6 WikiProjects suitable for subsetting through ShEx validators such as shex-js and PyShex (slurping).

# To reproduce the experiments
1. You can  download the relevant dataset from [this Zenodo repository](https://doi.org/10.5281/zenodo.5117927) for the desired WikiProject. There are one or a collection of .nt.gz files for each project. Otherwise, you can use WDumper with the specification files provided in the **WDumper Specification Files** directory and build the dataset of each project from the scratch. To use WDumper, go through the following steps:
```
$ git clone https://github.com/bennofs/wdumper.git
$ cd wdumper/
$ gradle build   # you will need JDK-11 and gradle
$ cd build/install/wdumper/bin/
$ ./wdumper-cli [wikidata dump.json.gz] [specification file.json]
```
* Note: the output will be a 'wdump-1.nt.gz' file. To start another extraction, change the name or move the file as it will be overwritten.
 
2. Import the dataset' .nt.gz file(s) via Blazegrph and load a local endpoint over it:
```
$ wget https://github.com/blazegraph/database/releases/download/BLAZEGRAPH_2_1_6_RC/blazegraph.jar
$ java -cp blazegraph.jar com.bigdata.rdf.store.DataLoader fastloader.properties [dataset].nt.gz
$ java -server -Xmx4g -jar blazegraph.jar
```
* Note: 'fastloader.properties' file is in the **Scripts** directory

3. Run queries that are in the **SPARQL queries** directory over the Blazegraph local endpoint:
```
$ curl -X POST http://localhost:9999/blazegraph/sparql --data-urlencode query@[SPARQL QUERY from the dir].sparql -H 'Accept:text/CSV' > [filename.csv]
```
4. Plot the charts via the Jupyter notebook provided in the **Script** directory.
