NIXP és el nom que reb el servidor de base de dades de l'IBSalut on es fan bolcats diaris de les taules de dades clíniques de diferents fonts.  


És un servidor que fa servir OracleDB com a motor de base de dades i al qual ens hi connectem fent servir l'sqldeveloper amb l'usuari s i les següents configuracions:
- Hostname: 
- Port: 1521
- Service name: SPHDW_SVC

La majoria de taules d'interés es troben sota l'schema atosdba. Està previst crear un schema propi de la PRISIB per a poder treballar en un espai comú.

## Fonts
### Atenció primària(eSIAP)
Taules atosdba.FZM_T_ESI_  
Emmagatzemen la base de dades del Sistema d'Informació d'Atenció Primària (SIAP) utilitzat en l'assitència primària. 
- FZM_T_ESI_FAGENDAS: Conté totes les cites pasades i futures a les agendes d'Atenció Primària.
- FZM_T_ESI_FUSUARIO: Conté la informació personal dels usuaris del Servei de Salut. Inclou dades identificatives (NHC, CIP_AUTONOMICO, DNI), l'adreça de l'usuari, el Centre de Salut que té assignat (COD_CENTRO) i el seu metge de capcelera (COD_CABECERA)
- FZM_T_ESI_FPERSONA: Conté la informació dels professionals de l'IBSalut
- FZM_T_ESI_HDIAGNOS: Conté tots els diagnòstics associats als diferent episodis del pacients. Utilitza 3 camps per codificar el diagnòstic (COD_1_ICD9, COD_2_ICD9, COD_3_ICD9) que fan referència a la taula FZM_T_ESI_TICD9.
- FZM_T_ESI_REC_PRESCR: Conté totes les prescripcions que s'han receptat amb la targeta sanitària. Conté codificat el fàrmac i el diagnòstic que justifica la prescripció, la durada, dosi i la posología de la recepta.

### Sophia
Taules atosdba.FIC_T_   
La Factoria d'Informació Corporativa és una iniciativa del Gabinet Tècnic-Assistencial del Servei de Salut per unificar tota la informació rellevant per la gestió en un portal web anomenat SOPHIA. Per alimentar aquest portal web es creen les taules FIC_T_ on es carrega part de la informació de l'Atenció Primària i hospitalària.
- FIC_T_CMBD
- FIC_T_CMBD_DIAG1
- FIC_T_CMBD_PROC1

### Hospitals
#### Son Espases (HSD)
atosdba.FZM_T_ESI_HSD2
#### Son Llàtzer (HSLL)
atosdba.FZM_T_ESI_HSLL2
#### Manacor (FHM)
atosdba.FZM_T_ESI_FHM2
#### Comarcal Inca i Menorca (HCIM)
atosdba.FZM_T_ESI_HCIM2
#### Can Misses (HCM) 
atosdba.FZM_T_ESI_HCM3

Les taules atosdba.FZM_T_SISN2 son un esforç en curs per unificar les taules de tots els hospitals. 

