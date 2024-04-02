A part dels recursos que aporten altres institucions con l'IBSalut i l'IdISBa, la PRISIB compta amb alguns recursos "propis" en la mesura en que son d'ús més o menys exclusiu per la plataforma. 
Aquests recursos i la informació asociada a ells es detalla a continuació:

### Portàtil EHDEN
Per poder fer servir les eines d'OHDSI per harmonitzar les dades a que té accés la PRISIB al model de dades OMOP, es va adquirir un portàtil a càrrec de l'acord amb EHDEN signat amb aquesta finalitat.
(Informació Portàtil)

### Servidor PRISIB
Aquest servidor es va adquirir amb els fons de l'acord signat amb EHDEN per crear un node de dades harmonitzades al model OMOP amb les eines d'OHDSI instal·lades. 
A més, s'hi han instal·lat altres eines necessàries per a la PRISIB.

#### PostgreSQL
Sistema gestor de base de dades necessari per al funcionament de les eines d'OHDSI i que també s'ha fet servir com a repositori de dades primari per a les dades harmonitzade a OMOP. 
Les dades provinents de les [fonts de dades](./Fonts-de-dades.ms) es carreguen a la base de dades primària mitjançant el [procés ETL](./PRISIBOMOPETL.md) desenvolupat a tal efecte
A més, té un schema dedicat als serveis de Gitea.

#### PgAdmin 4
Interficie gràfica per a la gestió de bases de dades Postgresql

#### OHDSI WebAPI
API que permet la interacció entre les eines web d'OHDSI i la base de dades. Té el sey propi schema a la base de dades de postgresql.

#### OHDSI Atlas

#### Gitea

#### R

#### RStudio
Windows Subsystem for Linus
OS: Ubuntu server ¿?


### Monitors extra
En realitat aquests monitors els ha proveit l'IdISBa i els té al seu inventari, però crec necessari esmentar-los en alguna part. 
S'han instal·lat 3 monitors HD de 27 polzades a 3 de les estacions de treball de la PRISIB per fer feina amb doble pantalla. 
