# Wikidata Reference Statistics
---
**IMPORTANT NOTE**

Due to a logical error in one of the queries, the data in one of the columns in Table 1 in the paper changes slightly. The column shows the number and percentage of referenced statements. In the original query used, the expression DISTINCT was applied to the external (alias) variable instead of the internal variable ([this commit](https://github.com/seyedahbr/Wikidata_Reference_Statistics/commit/0bfba7251286fbe539ebdb2b40067cd8986c9aef)). Below is the correct data for each dataset. Other paper's information as well as datasets are absolutely correct.
 
<table>
  <thead>
    <tr>
      <th>Project</th>
      <th>Dump</th>
      <th>Referenced Statements</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan=2>Gene Wiki</td>
      <td>2016</td>
      <td><strike>8,789,246(50%)</strike> 8,699,626(49%)</td>
    </tr>
    <tr>
      <td>2021</td>
      <td><strike>65,780,005(71%)</strike> 61,080,346(66%)</td>
    </tr>
    <tr>
      <td rowspan=2>Taxonomy</td>
      <td>2016</td>
      <td><strike>8,146,218(51%)</strike> 8,061,019(50%)</td>
    </tr>
    <tr>
      <td>2021</td>
      <td><strike>19,423,938(60%)</strike> 16,778,074(52%)</td>
    </tr>
    <tr>
      <td rowspan=2>Astronomy</td>
      <td>2016</td>
      <td>
        <strike>751,158(85%)</strike> 695,795(78%)
      </td>
    </tr>
    <tr>
      <td>2021</td>
      <td><strike>128,394,763(89%)</strike> 127,751,791(88%)</td>
    </tr>
    <tr>
      <td rowspan=2>Law</td>
      <td>2016</td>
      <td><strike>48,225(27%)</strike> 48,132(27%)</td>
    </tr>
    <tr>
      <td>2021</td>
      <td><strike>2,266,462(53%)</strike> 2,257,890(53%)</td>
    </tr>
    <tr>
      <td rowspan=2>Music</td>
      <td>2016</td>
      <td><strike>2,298,330(61%)</strike> 2,135,020(57%)</td>
    </tr>
    <tr>
      <td>2021</td>
      <td><strike>6,342,019(54%)</strike> 5,920,103(51%)</td>
    </tr>
    <tr>
      <td rowspan=2>Ships</td>
      <td>2016</td>
      <td><strike>114,528(62%)</strike> 111,121(61%)</td>
    </tr>
    <tr>
      <td>2021</td>
      <td><strike>315,381(29%)</strike> 295,885(27%)</td>
    </tr>
  </tbody>
</table>


---
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
