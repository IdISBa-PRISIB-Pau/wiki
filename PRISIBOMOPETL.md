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
FZM_T_ESI_TMUNICIP|347201|65697|Location||8th level OSM|Balearic Islands and matching score 1|
FZM_T_ESI_TICD9|39319|4749|Condition|ICD9, ICPC-2 | SNOMED|>80% of codes|
FZM_T_ESI_TPRIACT_DET|16230|934|Clinical Drug Box|National Drug Nomenclator|RxNorm||
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
FZM_T_ESI_TALERGIA|36|26|Clinical Finding||SNOMED||
FZM_T_ESI_TNOC|28|26|Procedure||SNOMED||
FZM_T_ESI_TEXITUS|4|3|Event||SNOMED||


DICTIONARY FIC|Codes|Mapped|Class|Source Vocabulary|Target Vocabulary|Notes
| ------------- | ------------- | ------------- |------------- | ------------- |------------- | ------------- |
FIC_T_DIAGNOSTICOS|114388|112559|Condition|ICD9, ICD10|SNOMED|Many duplications|
FIC_T_PROCEDIMIENTOS|84374|2262|Procedure|Internal codes, ICD9Proc & ICD10PCS|SNOMED|Many duplications|
FIC_T_FAR_PRES_FAR|16243|482|Clinical Drug Boxes||RxNorm|
FIC_T_FAR_PRINACT|10630|10618|Ingredient|ATC|RxNorm|Most entries are duplicated with keys changed over time|
FIC_T_LAB_PRUEBA|5540|620|Lab Test||LOINC|95% of frequency|
FIC_T_PRESTACION_SERAM|3420|2402|Procedure|SERAM|SNOMED|Multiple entries for the same code|
FIC_T_SERVICIO|2960|2309|Location, Provider, Physician Specialty||SNOMED, LOINC, Medicare Specialty, NUCC|
FIC_T_LAB_MICROORGANISMOS|1209|1163|Organism||SNOMED|
FIC_T_FAR_FORMA_FARM|507|359|Dose Form, Qualifier Value||SNOMED|
FIC_T_PAIS|504|242|Location||SNOMED|
FIC_T_LAB_UNIDAD|186|136|Unit||UCUM|
FIC_T_FAR_FRECUENCIA|86|78|Qualifier Value||SNOMED|
FIC_T_FAR_VIA_ADMON|64|55|Qualifier Value||SNOMED|
FIC_T_TIPO_INGR|8|8|Procedure||SNOMED|
FIC_T_SEXO|4|4|Gender||Gender|

#### Match with standard concepts
Amb usagi es carrega la taula que conté com a mínim els camps source code, source name i source table. Opcionalment es pot afegir una columna amb la freqüència i alguna altra informació. La descripció del concepte que Usagi utilitza per intentar trobar un concepte equivalent ha destar en anglés, de manera que la taula amb tots els conceptes d'origen es va traduir fent us de google translate tal com es recomana a ehden i després de comprobar que realment no s'allunya massa del significat original. 
En carregar la taula, s'ha de dir a quina columna del fitxer llegit es troba cada un dels camps i amb quin criteris s'ha de buscar un mappeig probable a un concepte standard. Abans de que Usagi faci aquest primer mapeig automàtic, s'han de descarregar els vocabularis destí de [Athena](https://athena.ohdsi.org). A la part inferior de la pantalla de càrrega hi ha les opcions per configurar aquest mapeig automàtic. Si no es limita a un domini o clase concret, pot tardar molt. 
![usagiimport](https://github.com/IdISBa-PRISIB-Pau/wiki/assets/142481605/218184af-b792-4bc8-b819-ceacd4869256)

#### Create SOURCE_TO_CONCEPT_MAP table
Com a resultat d'aquest procés s'ha generat una taula amb les columnes file_name, source_vocabulary_id, source_code, Source concept, target_concept_id, target_vocabulary_id, valid_start_date, valid_end_date i invalid_reason.
Aquesta taula s'exporta a source_to_concept.csv que es carregarà a la taula source_to_concept_map de la base de dades i s'utilitzarà durant la càrrega de dades per codificarles amb els nous codis concept_id.

---
## MILESTONE 1 ETL DOCUMENTATION 
---

### Technical architecture design	
En aquest punt, quan ja es té conéixement de les dades a harmonitzar, s'han de definir els requeriments del sistema en que es treballarà amb aquestes dades. Això inclou el maquinari i el programari del sistema on s'emmagatzemaran les dades i s'executaran les eines d'OHDSI, i les configuracions de seguretat i els procediments per accedir al servidor.

#### 	Define hardware requirements
Per tenir una referència, es va contactar amb la [SIDIAP](https://www.sidiap.org/index.php/ca/). Ens van donar una idea de les característiques del seu equipament, destacant que tenien més memòria RAM de la que seria estrictament necessària. 
Després de buscar entre diferents proveidors de diferents fabricants, es va adquirir el següent maquinari que va instal·lar el DTIC de l'IBSalut al seu centre de dades. 

Product|Description|Qty
| ------------- | ------------- | ------------- |
PYR2536RAN1|Fujitsu Primergy RX2530 M6 Server 10x 2.5' w/o Expander|1
PYBCP62X3|Intel Xeon Gold Processors 6330 28C 2.0 GHz|2
S26361-F3849-E100|Cooler Kit 2nd CPU|1
PYBME64S J|64GB (1x64GB) 2Rx4 DDR4-3200 R ECC Modules (Total: 1,024 GB of memory)|16
PYBSS48NKQ|SSD Drives SATA 6G 480GB Mixed-Use 2.5' H-P EP|2
PYBSS96NKQ|SSD Drives SATA 6G 960GB Mixed-Use 2.5' H-P EP|3
PYBSR4C6L|PRAID EP680i LP Controller|1
PYBLA342U|Network card PLAN EP X710-T2L 2x10GBASE-T OCPV3 (2 ports of 10G BaseT)|1
PYBRRS8S|Rack Mount Kit 1 S26361-F1452-E140 Region-kit Europe|1
S26361-F1790-E243|Management software iRMC advanced pack|1
PYBPU901|Power Supplies Modular PSU 900W titanium hp|2
T26139-Y1968-E250|Power cable, 2.5m, black|2
FSP:GN3S20Z00ESSV2|3-year warranty on site, in 9x5 conditions, NBD. Includes parts, labor and travel|1
INSTALL|Basic hardware installation service|1

#### 	Define software requirements
Després de parlar amb el DTIC es va decidir instal·lar un SO windows server. 
També es va decidir en aquest punt, que es faria servir postgres també com a Sistema gestor de base de dades primari per a les dades harmonitzades.
Un cop instal·lat el servidor i després de començar a treballar amb ell es va veure que no podiem fer servir tots la versió desktop de RStudio simultàneament, pel qual es va buscar com instal·lar una instància d'RStudio Server i es va veure que s'havia de fer amb el Windows Subsystem for Linux (WSL). Amb aquesta eina de Windows Server, es crea un sistema virtual que fa servir com a Sistema Operatiu Ubuntu Server X.X. D'aquesta manera podem accedir des del navegador web a l'RStudio Server sense iniciar sesió com usuari de Windows. 

#### 	Define security policies
També en col·laboració del DTIC es van definir quines funcions en la instal·lació, posada en marxa, manteniment i resolució d'incidències  realitzaria cada una de els parts implicades.

### Technical ETL Development	
Aquesta passa implica escriure, provar i documentar el codi que farà l'extracció, transformació i càrrega (ETL) de les dades des de la font al nou servidor. Per desenvolupar aquest codi, es va fer servir el portatil adquirit per aquest projecte i es va generar una màquina virtual on es van crear dos esquemes de bases de dades un amb l'estructura de les taules d'origen i l'altra amb l'OMOP CDM. Es va fer servir VirtualBox per virtualitzar la màquina, ubuntu server com a sistema operatiu de la màquina virtual i mariadb com a sistema gestor de base de dades per generar aquest entorn de proves. 

#### 	Write ETL code
El proces d'ETL es va desenvolupar fent servit l'Hitachi Pentaho Community Edition ja que permetia integrar tot el procés mantenint les conexions a les diferents bases de dades clarament definides, fer un us extensiu de la memòria carregant taules a la RAM durant la transformació i paral·lelitzar procesos de lectura i escriptura amb una interficie fàcil d'entendre i compatibilitat amb tots els sistemes tant de proves com de producció. 

#### 	Documentation of code
Pentaho genera un seguit de fitxers xml que defineixen cada passa a seguir amb el seu codi.

### Setting up of infrastructure	
Aquesta passa suposa l'execució de tot el definit a la definició de requeriments de maquinari feta anteriorment. El procés s'ha realitzat en col·laboració amb el DTIC, el proveidor del hardware, el proveidor del sistema operatiu i el departament d'informàtica de l'IdISBa. 

#### 	Hardware installation
Realitzat pel proveïdor segons les condicions de la DTIC.

#### 	Connection configuration
Realitzada per la DTIC.

#### 	Java installation
El departament d'informàtica de l'IdISBa, amb permisos d'administrador, va instal·lar el sistema operatiu i va realitzar algunes de les configuracions bàsiques.

#### 	User configuration

#### 	System variables

### Installation of the OHDSI / EHDEN tools	
	- WebAPI
	- ATLAS
	- Python
	- R
 Realitzada també amb l'ajuda del departament d'informàtica de l'IdISBa


Un cop realitzades totes les taques prèvies, es va procedir a la primera càrrega de dades. En principi, es preveu repetir-la cada 3 mesos millorant en cada iteració el mapeig de dades amb noves taules i nous conceptes. 
Per això es va instal·lar Hitachi Pentaho Community Edition al servidor, es va càrregar el procediment ETL desenvolupat al portatil i es van canviar els paràmetres de les connexions. També es van fer alguns ajustos al codi per canviar de fer servir mariadb a llegir de Oracle i escriure a Postgresql. 
Per minimitzar l'impacte de la càrrega de dades per altres usuaris, des del DTIC es va fer una còpia de les taules a carregar de NIXP a NIXT, el servidor de preproducció. 
Es van realitzar algunes proves parcials d'algunes passes del procés amb Pentaho, limitant les queries a 1000 files de resultats. 

El dia XX/XX/XXXX es va executar el procés de càrrega complet que va finalitzar en X h.

---
## MILESTONE 2 ETL IMPLEMENTED AND INFRASTRUCTURE OPERATIONAL 
---

### Technical testing of the ETL
Equesta passa consisteix en fer servir les eines d'OHDSI per fer un primer anàlisi descriptiu de com han quedat les dades després de la ETL.

#### 	Create test case framework

#### 	Achilles HEEL Analysis

#### 	Correction of incidences

### Data Quality Assessment	
En aquesta passa s'executen els anàlisis de qualitat estandarditzats en el Data quality dashboard, una eina d'OHDSI ([exemple amb dades sintètiques](https://data.ohdsi.org/DataQualityDashboard/)). La informació obtinguda amb aquesta eina s'ha utilitzat per depurar les dades i corregir el codi de la ETL. 

### Completion of the data catalogue	
Aquesta passa consisteix en generar un informe estandarditzat amb el [paquet d'R](https://github.com/EHDEN/CatalogueExport) desenvolupat per EHDEN per publicar-lo a l'EHDEN Portal, on es poden explorar les característiques bàsiques de les fonts de dades dels diferents nodes de la xarxa. 

#### Inspection Report	
Amb el paquet d'R [CDMInspector](https://github.com/EHDEN/CdmInspection) d'EHDEN es genera una documentació amb els resultats de les diferents anàlisis de qualitat. 
Una empresa certificada per EHDEN, en aquest cas Veratech, revisa tota la documentació de la ETL així com els diferents informes de qualitat de les dades generats després de carregar les dades. Si aquesta revisió és satisfactoria, dona certifica que el procés s'ha completat i es pot passar a participar en un primer estudi de la xarxa EHDEN. 

---
## MILESTONE 3
---
