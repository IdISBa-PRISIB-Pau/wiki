# PROCEDIMENT GENERAL

## SOL·LICITUD
- Les sol·licituds arriben per correu a idisba.prisib@ssib.es
- A gitea, crear un nou repositori a partir de la plantilla amb la numeració que correspon i amb el nom del projecte
- Es demana al sol·licitant que ompli el formulari i que el signi i que envii el protocol (si en té) i el dictamen del CEIm (si el té) 
- Se li envia el codi de bones pràctiques i el compromís de confidencialitat (tots els que hagin de treballar amb les dades l'han de tornar signat si no son treballadors de 
l'IBSalut)
- Es posa el codi del projecte i es signa la sol·licitud amb la nota REBUT PER LA PRISIB i la data i s'envia al sol·licitant com a comprovant.
- Guardar la documentació rebuda a la carpeta Sol.licitud de la carpeta del projecte
- Copiar la sol·licitud a la carpeta MQ/Seguiment plataformes/Sol·licituds amb el nom SSPT_AAAAMMDD_PRISIB_[NOMIP].pdf
- Iniciar el README.MD del repositori amb la informació del projecte, incloent els emails a l'apartat comunicacións.

## ANÀLISI
- Crear la tasca **ANALISI** a gitea i assignar-la (per ara, a PPericàs)
- Apuntar el projecte a la taula "AVALUACIONS PENDENTS CCT" a la carpeta [Evaluación 
Proyectos](https://ibsalut.sharepoint.com/:f:/s/PRISIB-ComitCientficTcnic/EtM6_mNXJ6lMvH1h6NuYGsUBmZS7BFnNTnkKAE70nXcDlQ?e=zKEB13) del teams del CCT 
- De l'anàlisi hauria de sortir un resum de les passes a seguir per extreure la informació a l'apartat análisi del README.MD
- Renombrar el llibre de calcul PRISIB_Data_model_template amb el codi del projecte
- Començar a omplir el Data Model amb les variables sol·licitades, les seves descripcions i les possibles fonts de les dades
- Consensuar amb el sol·licitant aquest model de dades (si cal, generar dades de prova seguint aquest model per ajudar a que s'entengui) i afegir-hi els criteris d'inclusió i 
d'exclusió, i les regles de validació 
- Amb el model de dades consensuat, fer el pressupost i enviar-li a l'Investigador Principal (IP) perquè el signi
- Copiar el pressupost acceptat a la carpeta MQ/Seguiment plataformes/Pressuposts acecptats amb el nom PSPT_AAAAMMDD_PRISIB_[NOMIP].pdf 

## DESENVOLUPAMENT
- Crear la tasca **DESENVOLUPAMENT** a gitea i assignar-la a qui l'hagi d'efectuar
- Renombrar l'script PRISIBXXXXX_Extraccio.sql amb la ID del projecte. A aquest script hi ha de quedar únicament el codi que dona el dataset final. Si s'han de fer proves o 
comprovacions guardar-les en un altre script
- Descriure a l'apartat desenvolupament del README.md les passes que s'hagin seguit en l'extracció, especialment aquelles que es desviin de l'inicialment previst a l'anàlisi
- Actualitzar el data model amb els canvis que s'hagin pogut fer durant el desenvolupament
- Guardar el dataset amb el codi del projecte a la carpeta corresponent. 
- Actualitzar el README.MD explicant el procés de l'extracció

## VALIDACIÓ
- Crear la tasca **VALIDACIÓ** a gitea i assignar-la a qui correspongui
- Revisar la documentació (README.MD, DataModel), el dataset i l'script per veure que està tot complet
- Validar el dataset amb l'eina de validació
- Si es detecten errors, notificar-los a qui ha fet la tasca de DESENVOLUPAMENT perquè els corregeixi i tornar al punt 12
- Si no hi ha errors, fer l'anàlisi descriptiu 

## ENTREGA
- Compartir el dataset amb el sol·licitant mitjançant OneDrive
	- Si OneDrive no és una opció viable i s'ha d'enviar per correu electrònic, si el data set conté dades personals s'ha d'encriptar i compartir la contrasenya amb el receptor per 
	una via de comunicació diferent. 
- Si amb això el servei queda completat, passar el presupost a la carpeta MQ/Seguiment plataformes/Serveis facturables
- Si s'ha de fer alguna modificació, s'ha de descriure a l'apartat incidències del README.MD, crear la tasca **INCIDÈNCIA** a gitea i assignar-la a qui correspongui (a partir d'aqui, 
repetir la part de desenvolupament descrita més adalt)

# PROCEDIMENT CCT

# FORMULARI DE SOL·LICITUD
- A la carpeta Sol·licitud del repositori del projecte esborrar les sol·licituds que no es facin servir i canviar el nom del pdf amb la data i el nom de l'IP
- L'IP ha de ser el que consti com a IP del projecte, encara que no sigui el sol·licitant. 
- La condició de investigador Intern, Associat o Extern i d'Emergent fa referència a l'IP, no al sol·licitant
- La sol·licitud ha de ser signada per l'IP
- Si és un projecte amb fons ubicats a l'IdISBa, confirmar amb el sol·licitant que el CODI DEL PROJECTE és el que consta a Fundanet

# CREACIÓ PRESSUPOST 
- A la carpeta Pressuposts i factures del repositori del projecte hi ha la plantilla per fer el pressupost
- Seleccionar el full a omplir en funció de si son fons idisba i de si l'investigador és emergent
- Omplir les dades del pressupost amb el que consti a la SOL·LICITUD
- A les activitats a facturar, posar-hi només activitats de la cartera de serveis de la plataforma (els que consten a les tarifes)
- Posar el preu per unitat (h) segons el que s'hagi d'aplicar d'acord a les tarifes publicades
- Copiar la taula, aferrar-la a un document de text i exportar-lo a pdf amb el nom PSPT_AAAAMMDD_PRISIB_[NOMIP].pdf 

# MODEL DE DADES
- Omplir la primera fulla amb la informació del projecte. 
	- El cas d'ús seran els objectius del projecte. 
	- La provinença seran les fonts de dades a utilitzar
	- Project ID és el codi que fem servir a la PRISIB pel PROJECTE
	- Si no s'ha presentat un Pla de Gestió de dades per separat, posar el nom del fitxer del protocol a aquesta casella
- A selection criteria específicar els criteris d'inclusió i exclusió
	- l'apartat diccionaris de dades específics fa referència a si s'ha de fer servir alguna categorització particular del projecte 
- A la pestanya data model cada fila serà una de les variables sol·licitades per l'Investigador
	- Si pel tipus de dades té sentit crear diferents taules (pe: Pacients dels que es volen dades demogràfiques i múltiples analítiques) les diferents taules s'especifíquen a 
	la columna Entitat
	- Les diferents taules hauran de tenir variables identificadores (Claus primaries) amb noms clarament diferents (pe: ID_PACIENT, ID_ANALITICA)
	- Les referències d'una taula a una altra (pe: l'identificador del pacient a la taula d'analitiques) pot fer servir el mateix nom de la variable de la taula a que la que fa 
referència 
	- A la columna format es faran servir idealment expressions regulars ((Regexr)[https://regexr.com/] per referències i proves)
	- El nivell de requeriment fa referència a si es una variable que ha d'estar present Obligatòriament a totes les files o si és opcional (si la columna permet NULL o NA)
	- El diccionari de classificació aquí específicat serà un diccionari estándard (pe: CIE9: Clasificación Internacional de Enfermedades v9, CIAP:Clasificación Internacional de 
Atención Primaria, NUTS: Nomenclature of Territorial Units for Statistics)
	- si és possible, la regla de validació es descriurà com una formula (pe: >'01/01/2020' & < '31/12/2023')
		
# SCRIPTS D'EXTRACCIÓ
A continuació es presenten les normes recomanades per formatar un script SQL:

### 1. **Claritat i Comentaris**
   - **Comentaris Detallats**: Inclou comentaris explicatius per a cada secció del codi, descrivint la funcionalitat de cada part de la consulta.
   - **Encapçalat Informatiu**: Afegeix un encapçalat al principi de l’script amb informació rellevant de la tasca i la llicència amb la qual es pot distribuir el seu contingut
### 2. **Nomenclatura i Estructura**
   - **Noms Descriptius**: Utilitza noms descriptius per a les taules, columnes i variables temporals per facilitar la comprensió del codi.
   - **Estructura Clara**: Organitza l’script en seccions lògiques amb salts de línia i indentació per millorar la llegibilitat.
### 3. **Reproduïbilitat**
   - **Versió de l'Script**: Mantingues un control de versions de l’script SQL per poder traçar els canvis i tornar a versions anteriors si cal.
   - **Dependències Documentades**: Inclou una llista de totes les dependències, com ara funcions, vistes i taules utilitzades en la consulta.
### 4. **Validació i Prova**
   - **Resultats de Validació**: Inclou exemples dels resultats per facilitar la validació (mai hauran de contenir informació personal identificable).
   - **Proves**: Si es fan consultes de prova per comprovar que s'està obtenint el resultat desitjat, deixar tot el bloc de codi comentat en guardar l'script i explicar qué és el 
que s'està provant.

### Exemple d’Script:

```sql
/*
 * Títol: Extracció de dades del projecte PRISIB20001 Diabetext
 * Objectiu: Extreure dades sobre pacients amb diabetis tipus 2
 * Autor: Pau Pericàs
 * Data de Creació: 2020-07-16
 * Data de Modificació: 2022-05-26
 * Descripció: Aquesta consulta extreu dades de la taula 'pacients' i 'diagnòstics' per identificar
 *             pacients diagnosticats amb diabetis tipus 2 durant els últims 5 anys.
 * Taules Utilitzades: pacients, diagnòstics
 * Versió: 3.0
 * 2024 Plataforma de Recerca en Informació en Salut de les Illes Balears (PRISIB) - Fundació Institut d'Investigació Sanitària Illes Balears (IdISBa) 
 * Ctra. Valldemossa, 79 (Hospital Universitari Son Espases), Edifici S, 1a planta. 07010 Palma de Mallorca, Spain
 * More info: idisba.es
 * Contact: idisba.prisib@ibsalut.es
 * This work is licensed under the Creative Commons Attribution 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/.
 */
 * Historial de Canvis:
 * 2020-07-16: Creació de la consulta inicial (Pau Pericàs)
 * 2022-05-26: Modificació per incloure nous centres de salut
 */

-- Consulta de la primera data de diagnòstic de cada pacient
SELECT 
    fu.nhc, 
    fu.nombre, 
    fu.apellido1,     
    MIN(d.fecha) AS primer_diagnostic
FROM 
    atosdba.FZM_T_ESI_FUSUARIO AS fu
JOIN 
    atosdba.FZM_T_ESI_HDSIAGNOS AS d ON fu.nhc = d.nhc
WHERE 
    d.COD_1_ICD = '250'
    AND fu.cod_centro in ('0014010110', '0014010310','0014011010')
GROUP BY 
    fu.nhc, 
    fu.nombre, 
    fu.apellido1 
ORDER BY 
    primer_diagnostic DESC;

	
-- prova per detectar dates mal introduides
/*
SELECT 
    fu.nhc, 
    fu.nombre, 
    fu.apellido1,     
    MIN(d.fecha) AS primer_diagnostic
FROM 
    atosdba.FZM_T_ESI_FUSUARIO AS fu
JOIN 
    atosdba.FZM_T_ESI_HDSIAGNOS AS d ON fu.nhc = d.nhc
WHERE 
    d.COD_1_ICD = '250'
    AND fu.cod_centro in ('0014010110', '0014010310','0014011010')
	AND d.fecha < '1900-01-01' 
GROUP BY 
    fu.nhc, 
    fu.nombre, 
    fu.apellido1 
ORDER BY 
    primer_diagnostic DESC;
*/
```

Seguint aquestes normes, asseguraràs que l’script SQL sigui fàcil de comprendre, mantingui un alt nivell de seguretat i privacitat, i sigui reutilitzable i optimitzat per a futurs projectes de recerca.


# README.MD
És fonamental documentar tot el procés pels següents motius:
#### Reproduïbilitat i Transparència:
La documentació detallada permet que altres investigadors repliquin l'estudi, validin els resultats i confiïn en la integritat de la investigació. Això és essencial per a la 
credibilitat científica.
#### Estandarització del Procés:
Una documentació clara i precisa assegura que el procediment es realitzi de manera consistent cada vegada. Això ajuda a mantenir la qualitat i la coherència de les dades 
recollides.
#### Facilitació de la Revisió:
Durant el procés de revisió, els revisors poden avaluar la metodologia emprada i assegurar-se que els mètodes d'extracció de dades són adequats i correctes.
#### Millora de la Col·laboració:
En projectes on múltiples investigadors o equips estan involucrats, la documentació ajuda a coordinar els esforços, assegurant que tots segueixen els mateixos procediments i 
que les dades són comparables.
#### Optimització i Eficàcia:
Documentar el procediment permet identificar àrees de millora i optimització en futurs projectes, fent el procés més eficient i menys propens a errors.
#### Compliment de Normatives i Ètica:
Moltes agències de finançament i comitès d'ètica requereixen una documentació completa dels mètodes d'extracció de dades per assegurar-se que es compleixen les normatives i els
 estàndards ètics.
#### Gestió de Dades:
Facilita la gestió de grans volums de dades, assegurant que es mantingui una pista d'auditoria clara des de la recopilació fins a l'anàlisi.
#### Formació i Educació:
Els nous membres de l'equip poden aprendre ràpidament els procediments establerts mitjançant la documentació, reduint el temps de formació necessari.
#### Prevenció d'Errors:
Una documentació detallada ajuda a prevenir errors i a corregir-los. Especialment si ha passat molt temps des de l'extracció o si la correcció la fa un membre diferent de l'equip.

# GITEA 
### Guia d'Ús d'un Servidor de Git Compartit per l'Equip de Treball

Aquesta guia proporciona instruccions per utilitzar un servidor Git compartit, facilitant la col·laboració eficient entre els membres de l'equip de treball.

#### 1. Configuració Inicial

1.**Instal·lar Git**:
   - Si no tens Git instal·lat, baixa'l i instal·la'l des del lloc oficial: [git-scm.com](https://git-scm.com/).

2.**Configuració Bàsica**:
   - Configura el teu nom d'usuari i correu electrònic. Aquestes dades s'utilitzen per identificar els teus canvis.
     ```bash
     git config --global user.name "El teu Nom"
     git config --global user.email "el_teu_email@example.com"
     ```

#### 2. Accés al Servidor Git

1.**Clonar un Repositori**:
   - Per obtenir una còpia local d'un repositori remot, utilitza el comando `git clone` seguit de l'URL del repositori.
     ```bash
     git clone https://nom_del_servidor/nom_del_repositori.git
     ```

#### 3. Treballar amb Git

1.**Crear una Nova Branca**:
   - Treballa en una branca separada per mantenir el codi principal net i estable.
     ```bash
     git checkout -b nom_de_la_branca
     ```

2.**Fer Canvis i Commetre'ls**:
   - Afegeix els fitxers modificats a l'índex i commet els canvis amb un missatge descriptiu.
     ```bash
     git add *
     git commit -m "Descripció dels canvis"
     ```

3.**Enviar Canvis al Repositori Remot**:
   - Puja els canvis de la teva branca local al repositori remot.
     ```bash
     git push origin nom_de_la_branca
     ```

#### 4. Col·laborar amb l'Equip

1. **Obrir un Pull Request**:
   - Per fusionar els teus canvis amb la branca principal, obre una sol·licitud d'extracció des de l'interfície web 
   Fer un pull request en un servidor que usa Gitea és un procés similar a altres serveis de control de versions com GitHub o GitLab. Aquí tens una guia pas a pas:
	- **Accedir a la Interfície Web de Gitea**:
		- Obre el teu navegador web i accedeix al servidor Gitea.
	- **Navegar al Repositori**:
		- Ves al repositori on has pujat la teva nova branca.
	- **Obrir la Secció de Pull Requests**:
		- Fes clic a la pestanya "Pull Requests" o "Merge Requests" al menú del repositori.
	- **Crear un Nou Pull Request**:
		- Fes clic a "New Pull Request" o "Create Pull Request".
	- **Seleccionar la Branca de Destinació i la Branca de Comparació**:
		- Selecciona la branca principal (per exemple, `main` o `master`) com a branca de destinació.
		- Selecciona la teva nova branca com a branca de comparació.
	- **Afegir un Títol i una Descripció**:
		- Proporciona un títol descriptiu per al pull request.
		- Afegeix una descripció detallada del que has fet i per què.
	- **Enviar el Pull Request**:
		- Fes clic a "Create Pull Request" per enviar-lo.
	- **Fusió del Pull Request**:
   - Un cop el pull request ha estat revisat i aprovat, es pot fusionar a la branca principal. Normalment, això ho fa un membre de l'equip amb permisos adequats. Si tens permisos, 
pots fusionar-lo tu mateix des de la interfície de Gitea.
	- **Revisar Canvis i Resoldre Conflictes**:
		- Revisa les pull requests dels altres membres de l'equip, proporcionant comentaris constructius.
		- Si es produeixen conflictes durant la fusió, resol-los localment:
     ```bash
     git pull origin nom_de_la_brancha_principal
     # Resol conflictes als fitxers
     git add fitxer_resolt.txt
     git commit -m "Resolució de conflictes"
     git push origin nom_de_la_brancha
     ```
	 
### Recursos Addicionals

- [Documentació oficial de Git](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

