# Details of selected and Ignored classes
Here is the WDumper specification files for each project in a separate directory. In each directory, there are two files. The first file contains the top-level classes which we infered from the projects' wiki pages. The details of the files for each project listed here. The second file (with _sub suffix), is teh enriched one with the add_subclass.py script.

**1. Gene Wiki**
All instances (wdt:P31) of the 24 main classes (+ all subclasses) at the Gene Wiki UML class diagram from the project’s web page are considered for extraction.

**2. Taxonomy** 
All instances (wdt:P31) of Taxon(Q16521) and all its subclasses will be in. We have also a taxon_related spec file based on related items on project’s web page. I investigated each related item by the SPARQL query below to see which can be included in the subset. To see what are the main predicates that points to the item (specially P31) and see how configure WDumper to extract the item if it is selected:
```
Select Distinct (Count(?item) as ?itemCount) ?properties where{
  ?item ?properties wd:Q42696902.
}group by ?properties
```
The ignored taxon-related items and reason:
* taxon redescription (Q42696902), species nova (Q27652812), genus novus (Q52800401): There are no instance of (P31) – there are a lot of main subject (P921) which connects scholarly articles to taxons and are not a part of project.
* first description (Q1361864): There are no instance of (P31) - it is not a class.   
* nomen alternativum (Q66092043), nomen conservandum (Q941227), nomen conservandum propositum (Q15708833), Sanctioned name (Q7415672), nomen utique rejiciendum propositum (Q15708837), nomen protectum (Q15709300), orthographia conservanda (Q51165361), orthographia conservanda (Q51165361), genus novus (Q52800401), genus novus (Q52800401), correct name (Q3342920), validly published name (Q17134993), effective publication (Q62846500), effective publication (Q62846500), ?( Q3025852), conserved type (Q66425288), lectotypification (Q61458071), genus femininum conservandum (Q67943921), genus masculinum conservandum (Q67943805), genus neutrum conservandum (Q67943587), Alliance (Q25202922): There are no instance of (P31) or not used as a class of something.

After running the Python script, the spec file of taxon_related contains 37 conditions (classes)

**3. Astronomy**
There are two ontology hierarchies in the project’s web page: 1)based on the subclass of (P279),  2) based on part of (P361). The second hierarchy is a part-whole relation of the first one. For our purpose, the first hierarchy would be sufficient. We extract all instances of the first hierarchy classes and subclasses. All instances of all subclasses of these 2 classes are in the subset:
* astronomical object (Q6999)
* universe (Q36906466) [to include universe (Q1)]. 

After running the Python script, the spec file contains 576 conditions (classes)

**4. Law**
Based on the mentioned items and classes on the project’s web page, all instances of all subclasses of the following classes are in the subset:
•	law (Q7748)
•	civil procedure (Q206937)
•	public order (Q294199)
•	Adelsrecht (Q355509)
•	mining law (Q427257)
•	health law (Q530962)
•	right to social security (Q548461)
•	conveyancing (Q759815)
•	Q811705	construction law
•	Q895986	food law
•	Q1162317	Wine law
•	Q1230212	Disziplinarrecht
•	Q1309660	container deposit legislation
•	Q1416588	financial law
•	Q1438384	Forest law
•	Q1453439	Sports law
•	Q1466479	Sprengstoffrecht
•	Q1495680	Gaststättenrecht
•	Q1550476	Grundbuchrecht
•	Q1577380	ecclesiastical law
•	Q1711323	Youth Welfare Law
•	Q1752579	economic law
•	Q1900600	trademark law
•	Q1941172	customs law
•	Q1987559	social law
•	Q2101827	police law
•	Q2313683	Sprengstoffrecht (Deutschland)
•	Q2325126	Staatsorganisationsrecht
•	Q2515700	Public procurement law in Germany
•	Q2632182	medical law
•	Q3039676	droit de la communication
•	Q3039827	droit pénal de la presse
•	Q4376039	Право на землю
•	Q4774377	Anti-homelessness legislation
•	Q5253952	delict
•	Q7972824	waste management law
•	Q8009938	municipal law
•	Q11826893	telecommunications law
•	Q14518216	welzijnsrecht
•	Q17113465	civil law
•	Q17363091	State law
•	Q19392966	dynamisk tingsrett
•	Q19393365	Trygderett
•	Q19971701	iT law
•	Q21403057	norsk avtalerett
•	Q25098713	transactional law
•	Q28147639	Execution of court decision
•	Q45949533	data law
•	Q47450595	theatre law
•	Q47517044	Etten Beiler dingspel
•	Q53036384	Arverett
•	Q61451648	Arbeitnehmererfinderrecht
•	Q628967	labor law
•	Q1567259	Sozialrecht
•	adjudication (Q357789)
•	legal proceeding (Q1301203)
•	legal case (Q2334719)
•	Q66599007	bankruptcy law
•	area of law (Q1756157) [it will include some of the T-Boxes bot it is essential as some A-Boxes depend on it]
•	Q18657604	intellectual property law
•	bundle of rights (Q4997551)
•	Q176763	evidence
•	jurisprudence (Q4932206)
•	Q105327849	election offence
•	Q664183	consumer protection
•	trade regulation (Q7832073)
•	Jurisdiction (Q5982983)
After running the Python script, the spec file contains 1294 conditions (classes)

**5. Music**
Based on the mentioned items and classes on the project’s web page, all instances (or occupation, for humans) of all subclasses of the following classes are in the subset:
•	[occupation (P106)] musician (Q639669)
•	musical ensemble (Q2088357)
•	musical work (Q2188189)
•	audio track (Q7302866)
•	music video (Q193977)
•	record label (Q18127)
After running the Python script, the spec file contains 1067 conditions (classes) = 375 for P106 and 692 for P31.

**6. Ships**
Based on the mentioned items and classes on the project’s web page, all instances of all subclasses of the following classes are in the subset:
•	watercraft (Q1229765)
•	ship class (Q559026)
The project has a well-structured class hierarchy. With above classes, other subclasses like ship (Q11446), boat (Q35872), submarine (Q2811), submersible (Q1570255), etc. will be added to the spec file. After running the Python script, the spec file contains 827 conditions (classes).