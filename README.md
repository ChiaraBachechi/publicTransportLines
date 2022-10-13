# publicTransportLines

Affinchè i layer siano fruibili per il progetto, modificare eventualmente la sorgente dati di ognuno; quindi per ogni layer selezionare il corrispondente presente nella cartella "File sorgente". 
É possibile la visualizzazione a piacimento del layer desiderato. 
I layer "q_fer_m2" e "q_fer_mt_strada" presentano una visualizzazione categorizzata nella colorazione, per ogni elemento del layer considerato.

Per poter ottenere i layer è stato necessario creare un database locale su PostgreSQL; il database è stato denominato "modena".

Le tabelle contenute nel database sono le seguenti:

-fer: tabella che contiene tutte le fermate degli autobus della città di Modena.

-strade: tabella che contiene tutte le strade della città di Modena (tra le quali primarie, secondarie, terziarie, etc).

-linee: tabella che contiene tutte le linee del trasporto pubblico della città di Modena.

-linee_strade: tabella che contiene tutte le associazioni tra linee e strade che le percorrono (composizione tra linee e strade)

-linee_fer_orario: tabella che contiene tutte le associazioni tra linee e fermate di competenza, con relativo orario e sequenza di percorrenza (composizione di fer, linee a cui sono stati integrati dati ottenuti dal sito web SETA).

-quartieri_intersect_t: tabella che contiene dei record in cui è presente un attributo (count) che esprime l'associazione tra quartieri e linee (in particolare associa il numero di linee per ogni quartiere).

-q_fer_mt_strada: tabella che contiene dei record in cui è presente un attributo (fer_per_mt_strada) che esprime l'associazione tra quartieri, fermate e strade (in particolare associa il numero di fermate, per metro di strada, per ogni quartiere).

-q_fer_m2: tabella che contiene dei record in cui è presente un attributo (fer_per_m2) che esprime l'associazione tra quartieri e fermate (in particolare associa il numero di fermate, al metro quadro, per ogni quartiere).


Struttura delle tabelle:
-fer: id, geom, name, latitude, longitude, strada_id, l_array
-strade: id, geom, name, highway, lanes, maxspeed, psv
-linee: id, geom, name, from, to, network, operator
-linee_strade: id, strada_id
-linee_fer_orario: id, stop_id, corsa, sequenza
-quartieri_intersect_t: id, interseca, count
-q_fer_mt_strada: id, count, sum, fer_per_mt_strada, geom
-q_fer_m2: id, count, area, fer_per_m2, geom

Primary Key:
-fer: id
-strade: id
-linee: id
-linee_strade: id, strada_id
-linee_fer_orario: id, stop_id
-quartieri_intersect_t: id
-q_fer_mt_strada: id
-q_fer_m2: id

Foreign Key:
-linee_strada:
(id) -> (linee.id)
(strada_id) -> (strade.id)

-linee_fer_orario:
(id) -> (linee.id)
(stop_id) -> (fer.id)

-quartieri_intersect_t:
(id) -> (quartieri.id)

-q_fer_mt_strada:
(id) -> (quartieri.id)

-q_fer_m2:
(id) -> (quartieri.id)
