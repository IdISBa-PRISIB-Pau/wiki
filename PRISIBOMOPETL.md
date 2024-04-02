### Introducció

El 2021 es va signar un acord amb la European Health Data Evidence Network(EHDEN) per harmonitzar les dades que utilitzava la PRISIB al model de dades 
Observational Medical Outcomes Partnership (OMOP) creat per la Observational Health Data Sciences and Informatics (OHDSI, pronounced “Odyssey”) initiative 
i passar a ser un nou node de la xarxa. 

L'acord estableix la entrega de 3 informes (Milestones) amb la documentació desenvolupada en el procés d'harmonització que en una de les últimes fases, 
és certificada per una empresa externa aprovada per EHDEN (en aquest cas, Veratech).
Per facilitar el seguiment del progrés s'estableixen una sèrie de passes que van generant uns resultats que es detallen a continuació:

### Dataset profiling and documentation	
En aquesta passa s'utilitza l'eina d'OHDSI WhiteRabbit per connectar-se a la base de dades i generar un informe en format xlsx que describeix totes les taules i totes les columnes de la font de dades. Inicialment es planejava fer servir com a fonts de dades ESIAP per l'Atenció Primària i les taules de SOPHIA (FIC_T_) per a la atenció especialitzada. Donada la quantitat de taules a mapeijar, la redundància de moltes de les dades (ja que també hi ha dades d'AP a SOPHIA) i l'escàs detall que algunes dades tenen a SOPHIA per els propòsits de la PRISIB, es va optar finalment per només mapeijar les taules del CMBD. En futures iteracions del procés ETL s'aniran incorporant altres taules amb dades provinents de l'atenció hospitalària. 
#### ScanReport FIC
ALL_FIC-2022.xlsx és l'informe generat per WhiteRabbit sobre 6552 camps a 449 taules de SOPHIA.
#### ScanReport SIAP
ALL_ESIAP-2022.xlsx és l'informe generat per WhiteRabbit sobre 146 taules i 2355 variables del Sistema d'Informació d'Atenció Primària
#### Complete table description
Completar la columna Description de la fulla Table Overview dels anteriors informes amb la descripció de cada taula dels dos conjunts de dades analitzats.
#### Complete field description
Completar la columna Description de la fulla Field Overview dels anteriors informes amb la descripció del contingut de cada columna dels dos conjunts de dades analitzats.
#### Remove innecessary tables
Un cop analitzades les taules presents a la font de dades, decidir aquelles que finalment es traslladaran al model de dades OMOP. 
### Generation of the ETL Design	
En aquesta passa s'utilitza l'eina d'OHDSI RabbitInAHat per llegir el informes generats per WhiteRabbit i explicitar la relació entre cada cap de cada taula de la font de dades i un camp d'entre els 371 de les taules de l'OMOP Common Data Model.
En acabar, aquesta eina genera un informe en format comprimit json.gz que es port exportar a .docx, .csv o  .html.
Durant el procés de mappeig, fa servir una interficie gràfica per anar enllaçant una taula a una altra que dona una primera vista general del procés ETL.


![RIAHScreenshot](https://github.com/IdISBa-PRISIB-Pau/wiki/assets/142481605/0ad70d50-ba31-4a1d-9c28-f2761d2c65a6)

#### Create relationships FIC-CDM
FIC ETL target_fields.csv
#### Create relationships SIAP-CDM
SIAP ETL target_fields.csv
### Mapping of source vocabularies	
En aquesta passa es fa servir l'eina d'OHDSI Usagi per tal de mappeijar no les taules en si, si no el contingut de les taules que fan de diccionari a la font de dades a algun dels conceptes standard dels diccionaris incorporats dins de OMOP. 
Es tracta d'un mapeig més conceptual que estructural que depenent de on i com s'utilitzi un codi, pot donar com a resultat un mapeig a un concepte diferent amb algun matís diferent. 
Durant el procés de càrrega de dades, quan es carrega una informació codificada en aquests diccionaris, es busca a la taula source_to_concept_map que genera usagi amb el codi i la taula d'origen a un concept_id d'un concepte dels diccionaris d'OMOP. 
#### Identify source vocabulary tables
En aquesta passa es van buscar tots els diccionaris utilitzats a les fonts de dades. Al Milestone I report es citen aquests diccionaris.
DICTIONARY ESI|Codes|Mapped|Class|Source Vocabulary|Target Vocabulary|Notes
| ------------- | ------------- | ------------- |------------- | ------------- |------------- | ------------- |
FZM_T_ESI_TMUNICIP|347201|65697|Location|8th level OSM|Balearic Islands and matching score 1|
FZM_T_ESI_TICD9|39319|4749|Condition|ICD9, ICPC-2, SNOMED|>80% of codes|
FZM_T_ESI_TPRIACT_DET|16230|934|Clinical Drug Box|National Drug Nomenclator|RxNorm|
FZM_T_ESI_TPRIACT_CAB|12331|1758|Clinical Drug Form||RxNorm|>80% of prescriptions|
FZM_T_ESI_TANALITI_DET|3115|1233|Measurement||LOINC||
FZM_T_ESI_TANALITI|1776|705|Measurement||LOINC||
FZM_T_ESI_TIMAGENES|924|846|Procedure|SERAM|SNOMED||
FZM_T_ESI_TACTU_DE|528|368|Procedure|ICD9CM|LOINC & SNOMED||
FZM_T_ESI_TACTIVIDADES|462|134|Procedure||SNOMED||
FZM_T_ESI_TPAIS|266|248|Location||SNOMED||
FZM_T_ESI_TRX|170|152|Procedure|SERAM|SNOMED||
FZM_T_ESI_TPROCEDIMIENTOS|129|117|Procedure||SNOMED||
FZM_T_ESI_TVACUNAS|101|100|Drugs||RxNorm||
FZM_T_ESI_TCATEGOR|87|67|Social Context, Answer, Physician Specialty, Provider||SNOMED, LOINC, Medicare Specialty, NUCC||
FZM_T_ESI_TPC|86|75|Observable Entity, Clinical Observation||SNOMED, LOINC||
FZM_T_ESI_REC_FRECUENCIA|69|62|Qualifier Value||SNOMED||
FZM_T_ESI_TFAC_RIE|64|55|Observation||SNOMED||
FZM_T_ESI_TVIA_ADMI|63|60|Qualifier Value||SNOMED||
FZM_T_ESI_TTIPOVIA|49|49|Location||OSM, SNOMED||
FZM_T_ESI_TINTERVENCIONES|48|48|Procedure||SNOMED||
FZM_T_ESI_TALERGIA|36|26|Clinical|Finding||SNOMED||
FZM_T_ESI_TNOC|28|26|Procedure||SNOMED||
FZM_T_ESI_TEXITUS|4|3|Event||SNOMED||
#### Match with standard concepts
#### Create SOURCE_TO_CONCEPT_MAP table
## MILESTONE 1 ETL DOCUMENTATION (March)	
### Technical architecture design	
#### 	Define hardware requirements
#### 	Define software requirements
#### 	Define security policies
### Technical ETL Development	
#### 	Write ETL code
#### 	Documentation of code
### Setting up of infrastructure	
#### 	Hardware installation
#### 	Connection configuration
#### 	Java installation
#### 	User configuration
#### 	System variables
### Installation of the OHDSI / EHDEN tools	
	WebAPI
	ATLAS
	Python
	R
## MILESTONE 2 ETL IMPLEMENTED AND INFRASTRUCTURE OPERATIONAL (September)	
### Technical testing of the ETL	
#### 	Create test case framework
#### 	Achilles HEEL Analysis
#### 	Correction of incidences
### Data Quality Assessment	Data quality dashboard
### Completion of the data catalogue	Data catalogue export
#### Inspection Report	
