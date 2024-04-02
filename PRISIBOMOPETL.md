### Introducció

El 2021 es va signar un acord amb la European Health Data Evidence Network(EHDEN) per harmonitzar les dades que utilitzava la PRISIB al model de dades 
Observational Medical Outcomes Partnership (OMOP) creat per la Observational Health Data Sciences and Informatics (OHDSI, pronounced “Odyssey”) initiative 
i passar a ser un nou node de la xarxa. 

L'acord estableix la entrega de 3 informes (Milestones) amb la documentació desenvolupada en el procés d'harmonització que en una de les últimes fases, 
és certificada per una empresa externa aprovada per EHDEN (en aquest cas, Veratech).
Per facilitar el seguiment del progrés s'estableixen una sèrie de passes que van generant uns resultats que es detallen a continuació:

### Dataset profiling and documentation	
#### ScanReport FIC
#### ScanReport SIAP
#### Complete table description
#### Complete field description
#### Remove innecessary tables
### Generation of the ETL Design	
#### Create relationships FIC-CDM
#### Create relationships SIAP-CDM
### Mapping of source vocabularies	
#### Identify source vocabulary tables
#### Match with standard concepts
#### 	Create SOURCE_TO_CONCEPT_MAP table
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
