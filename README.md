| [italiano](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#acquisizione-dati-inquinanti-ambientali-arpa-puglia-in-home-assistant) | [inglese](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#arpa-puglia-environmental-pollutant-data-acquisition-in-home-assistant) |

![](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/HA%20logo2.png)  `          ` ![](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Node-RED%20logo.jpg)
---   
# Acquisizione dati inquinanti ambientali ARPA Puglia in Home Assistant

Una utility [Home Assistant](https://home-assistant.io/) che ti aiuta a visualizzare i dati dei principali indicatori ambientali pubblicati da ARPA Puglia utilizzando [Node-RED](https://nodered.org/).

<br>

## Tavola dei Contenuti

1. **[Descrizione del progetto](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#descrizione-del-progetto)**

2. **[Caratteristiche principali](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#caratteristiche-principali)**

3. **[Descrizione del funzionamento](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#descrizione-del-funzionamento)**

4. **[Installazione](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#installazione)**
   1. **[Prerequisiti](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#1---prerequisiti)**
   1. **[Configurazione dei dati da acquisire](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#2---configurazione-dei-dati-da-acquisire)**
   1. **[Configurazione Home Assistant](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#3---configurazione-home-assistant)**
   2. **[Configurazione di Node-RED](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#4---configurazione-di-node-red)**

5. **[Personalizzazione dei flussi di NodeRed](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#personalizzazione-ed-analisi-dei-flussi-nodered)**

6. **[Commento del codice](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED#commentiamolo)**  
 

 
<br>

## Descrizione del progetto

Scopo principale di queste righe è quello di automatizzare l`acquisizione giornaliera di dati ambientali pubblicati tramite API dalla Agenzia Regionale Protezione e Prevenzione Ambientale per la Puglia, la loro elaborazione tramite Node-RED e la diretta esposizione  in Home Assistant.

Tutte le info sono disponibili sul sito di [ARPA Puglia](https://www.arpa.puglia.it/pagina2795_aria.html) secondo al [mappa](https://dati.arpa.puglia.it/qaria?footer=false%EF%BB%BF)

---

## Caratteristiche principali

- **API Integration**: Collegamento diretto alle API di ARPA Puglia per il prelievo di dei seguenti parametri ambientali:
     1.  **PM10** (Polveri inalabili, Insieme di sostanze solide e liquide con diametro inferiore a 10 micron. Derivano  da emissioni di autoveicoli, processi industriali, fenomeni naturali)
     1.  **PM2.5** (Polveri respirabili, Insieme di sostanze solide e liquide con diametro inferiore a 2.5 micron. Derivano  da processi industriali, processi di combustione, emissioni di autoveicoli, fenomeni naturali)
     3.  **NO2** (Biossido di azoto, Gas tossico che si forma nelle combustioni ad alta temperatura. Sue principali sorgenti sono i motori a scoppio, gli impianti termici, le centrali termoelettriche)
     4.  **SO2** (Biossido di zolfo, Gas irritante, si forma soprattutto in seguito all`utilizzo di combustibili (carbone, petrolio, gasolio) contenenti impurezze di zolfo)
     5.  **CO** (Monossido di Carbonio, Sostanza gassosa, si forma per combustione incompleta di materiale organico, ad esempio nei motori degli autoveicoli e nei processi industriali)
     6.  **C6H6** (Benzene, Liquido volatile e dall`odore dolciastro. Deriva dalla combustione incompleta del carbone e del petrolio, dai gas esausti dei veicoli a motore, dal fumo di tabacco)
     7.  **IPA** (Idrocarburi Policiclici Aromatici, Classe di composti organici semi-volatili, con 2 o più da anelli benzenici condensati tra loro, generati dalla combustione incompleta di materiale organico. Il dato fornito si riferisce agli IPA adsorbiti su particelle carboniose con un diametro aerodinamico tra 0.01 e 1 micron)
     8.  **H2S** (Idrogeno solforato, Gas incolore dal caratteristico odore di uova marce, caratterizzato da una soglia olfattiva bassa.  E` generato nella produzione di carbon coke, nella lavorazione del petrolio,  di fertilizzanti, dei rifiuti e di altri procedimenti industriali)
     9.  **O3** (Ozono, Sostanza non emessa direttamente in atmosfera, si forma per reazione tra altri inquinanti, principalmente NO2 e idrocarburi, in presenza di radiazione solare)
     10.  **BLACK CARB** (Black Carbon, Prodotto della combustione incompleta di combustibili fossili e biomassa; può essere emesso da sorgenti naturali ed antropiche sotto forma di fuliggine)
     11. **Qualità dell`aria**

**Disclaimer**: Non tutte le centraline espongono tutti i dati, pertanto, ho deciso di pubblicare due flussi di node-red da porter poi integrare con i dati eventualmente recuperati direttamente dal sito ARPA di accesso alle loro API: 

[API_Regione_Puglia](https://dati.arpa.puglia.it/openapi/index.html)

- **Workflow Node-RED**: Flusso configurato per interrogare giornalmente le API, processare i dati (formattazione, validazione) e inviarli direttamente ad HA tramite sensori che si autogenerano tramite l'app Companion di NodeRED.
- **Automazione Giornaliera**: Schedulazione degli aggiornamenti per garantire dati sempre aggiornati senza intervento manuale.

---

## Descrizione del Funzionamento

1. **Acquisizione Dati**:  
   Node-RED effettua chiamate API periodiche ad ARPA Puglia e filtra i dati rilevanti.

2. **ELABORAZIONE ED INVIO IN HOME Assistant**:  
   I dati vengono convertiti in sensori esposti direttamente in HA (es. JSON strutturato).

3. **Visualizzazione**:  
   Integrazione in dashboard per monitoraggio ambientale centralizzato.

---

## Installazione

### 1 - Prerequisiti

- Node-RED installato e configurato con nodi:
  - `node-red-contrib-http-request`
- Home Assistant installato con le seguenti dipendenze HACS:
  - Custom `flex-table-card` scaricabile (Se volete utilizzare la tabella di visualizzazione come ho fatto io)
  - Node-RED Companion installata (componente aggintivo scaricabile da HACS).


### 2 - Configurazione dei dati da acquisire

1.Come già anticipato i dati sono acquisiti tramite le API pubbliche messe a disposizione dall`ARPA. Le centraline disponibili (dato aggiornato al 29.1.2025) sono le seguenti:

|id_station|             denominazione                                |                       comune    | indirizzo               |rete   |interesse_rete|provincia    |   paese   |paese_esteso  |  Latitude    |Longitude     |    sorgente  |
| -------- | -------------------------------------------------------- | ------------------------------- | ----------------------- | ----- | ------------ | ----------- | --------- | ------------ | ------------ | ------------ | ------------ |
|8|Monte S. Angelo - Ciuffreda|Monte Sant Angelo|Suolo Ciuffreda|RRQA|PUBBLICO|Foggia|IT|Italy|15.945254|41.666109|ARPAP
|10|Manfredonia - Mandorli|Manfredonia|Via dei Mandorli|RRQA|PUBBLICO|Foggia|IT|Italy|15.909638|41.629333|ARPAP
|14|Molfetta - Verdi|Molfetta|P.zza Verdi|RRQA|PUBBLICO|Bari|IT|Italy|16.605253|41.201101|ARPAP
|17|Bari - Caldarola|Bari|Via Caldarola|RRQA|PUBBLICO|Bari|IT|Italy|16.888064|41.113542|ARPAP
|18|Statte - Sorgenti|Statte|Via Delle Sorgenti|RRQA|PUBBLICO|Taranto|IT|Italy|17.203325|40.562499|ARPAP
|19|Taranto - Archimede|Taranto|Via Archimede|RRQA|PUBBLICO|Taranto|IT|Italy|17.233048|40.494441|ARPAP
|20|Taranto - Machiavelli|Taranto|Via Machiavelli|RRQA|PUBBLICO|Taranto|IT|Italy|17.225823|40.488608|ARPAP
|21|Taranto - San Vito|Taranto|presso Colonia Marina|RRQA|PUBBLICO|Taranto|IT|Italy|17.225272|40.423328|ARPAP
|22|Taranto - Alto Adige|Taranto|Via Alto Adige| presso scuola XX Circolo|RRQA|PUBBLICO|Taranto|IT|Italy|17.263602|40.460553|ARPAP
|23|Mesagne - Via Udine|Mesagne|Via Udine|RRQA|PUBBLICO|Brindisi|IT|Italy|17.807998|40.565995|ARPAP
|24|Brindisi - Via Taranto|Brindisi|Via Taranto|RRQA|PUBBLICO|Brindisi|IT|Italy|17.947777|40.634166|ARPAP
|25|San Pancrazio|San Pancrazio Salentino|null|RRQA|PUBBLICO|Brindisi|IT|Italy|17.845999|40.422993|ARPAP
|26|San Pietro Vernotico|San Pietro Vernotico|null|RRQA|PUBBLICO|Brindisi|IT|Italy|18.005994|40.485998|ARPAP
|27|Torchiarolo - Don Minzoni|Torchiarolo|P.za Don Minzoni|RRQA|PUBBLICO|Brindisi|IT|Italy|18.053991|40.487999|ARPAP
|28|Guagnano - Villa Baldassarri|Guagnano|Villa Baldassarri|RRQA|PUBBLICO|Lecce|IT|Italy|17.964477|40.418525|ARPAP
|29|Lecce - Cerrate|Lecce|S. Maria Cerrate|RRQA|PUBBLICO|Lecce|IT|Italy|18.116386|40.459696|ARPAP
|31|Arnesano - Riesci|Arnesano|Zona Riesci|RRQA|PUBBLICO|Lecce|IT|Italy|18.095074|40.346270|ARPAP
|33|Brindisi - Via dei Mille|Brindisi|Via dei Mille|RRQA|PUBBLICO|Brindisi|IT|Italy|17.938152|40.638748|ARPAP
|35|Brindisi - Casale|Brindisi|Via San Giusto|RRQA|PUBBLICO|Brindisi|IT|Italy|17.942569|40.650083|ARPAP
|36|Brindisi - SISRI|Brindisi|Via Curie|RRQA|PUBBLICO|Brindisi|IT|Italy|17.975041|40.624738|ARPAP
|37|Taranto - CISI|Taranto|q.re Paolo VI - presso CISI Puglia|RRQA|PUBBLICO|Taranto|IT|Italy|17.253416|40.520934|ARPAP
|38|Taranto - Talsano|Taranto|Talsano - presso scuola U.Foscolo|RRQA|PUBBLICO|Taranto|IT|Italy|17.283879|40.411943|ARPAP
|40|Statte - Wind|Statte|ss.7 presso il ponte radio wind|RRQA|PUBBLICO|Taranto|IT|Italy|17.173611|40.526111|ARPAP
|41|Grottaglie|Grottaglie|via XXV luglio|RRQA|PUBBLICO|Taranto|IT|Italy|17.423879|40.537776|ARPAP
|42|Martina Franca|Martina Franca|Via della Stazione|RRQA|PUBBLICO|Taranto|IT|Italy|17.331939|40.700826|ARPAP
|47|Lecce - Garigliano|Lecce|null|RRQA|PUBBLICO|Lecce|IT|Italy|18.174327|40.364457|ARPAP
|49|Maglie|Maglie|Via Don. L. Sturzo| 4|IL|PUBBLICO|Lecce|IT|Italy|18.294098|40.123636|ARPAP
|50|Galatina - I.T.C.  La Porta |Galatina|Viale degli studenti|RRQA|PUBBLICO|Lecce|IT|Italy|18.174725|40.166947|ARPAP
|51|Campi Salentina|Campi Salentina|Via Napoli|RRQA|PUBBLICO|Lecce|IT|Italy|18.026509|40.397507|ARPAP
|54|Bari - Cavour|Bari|Corso Cavour|RRQA|PUBBLICO|Bari|IT|Italy|16.872552|41.122269|ARPAP
|55|Bari - Kennedy|Bari|Piazza R. Kennedy|RRQA|PUBBLICO|Bari|IT|Italy|16.858905|41.099593|ARPAP
|62|Lecce - Libertini|Lecce|Piazza Libertini| Lecce|RRQA|PUBBLICO|Lecce|IT|Italy|18.176667|40.351945|ARPAP
|63|Andria - Vaccina|Andria|Via Vaccina|RRQA|PUBBLICO|BAT|IT|Italy|16.303939|41.233278|ARPAP
|64|Altamura - Via Santeramo|Altamura|Via Golgota| Altamura|RRQA|PUBBLICO|Bari|IT|Italy|16.561015|40.828848|ARPAP
|65|Casamassima - LaPenna|Casamassima|Via Lapenna|RRQA|PUBBLICO|Bari|IT|Italy|16.920731|40.953154|ARPAP
|66|Monopoli - Aldo Moro|Monopoli|Viale Aldo Moro|RRQA|PUBBLICO|Bari|IT|Italy|17.290285|40.951167|ARPAP
|67|Brindisi - Terminal Passeggeri|Brindisi|presso Terninal Passeggeri sulla banchina portuale di Costa Morena|RRQA|PUBBLICO|Brindisi|IT|Italy|17.961687|40.647432|ARPAP
|71|Barletta - Casardi|Barletta|via Casardi|RRQA|PUBBLICO|BAT|IT|Italy|16.286111|41.316666|ARPAP
|72|Francavilla Fontana|Francavilla Fontana|Via Fabio Filzi|RRQA|PUBBLICO|Brindisi|IT|Italy|17.588331|40.529163|ARPAP
|75|Massafra|Massafra|Via Frappietri|RRQA|PUBBLICO|Taranto|IT|Italy|17.116690|40.593761|ARPAP
|76|Foggia - Rosati|Foggia|Via Giuseppe Rosati| 139|RRQA|PUBBLICO|Foggia|IT|Italy|15.548611|41.455555|ARPAP
|77|Brindisi - Perrino|Brindisi|Via Crati|RRQA|PUBBLICO|Brindisi|IT|Italy|17.954778|40.631361|ARPAP
|78|Brindisi - Cappuccini|Brindisi|Via Cappuccini|IL|PUBBLICO|Brindisi|IT|Italy|17.921778|40.630917|ARPAP
|81|Bari - Carbonara|Bari|via Loguercio|RRQA|PUBBLICO|Bari|IT|Italy|16.866944|41.076666|ARPAP
|85|San Severo - Azienda Russo|San Severo|Localita` Palmori|RRQA|PUBBLICO|Foggia|IT|Italy|15.440833|41.546666|ARPAP
|90|Bari - CUS|Bari|Lungomare Starita presso CUS BARI|RRQA|PUBBLICO|Bari|IT|Italy|16.845277|41.134722|ARPAP
|92|Monopoli - Liceo Artistico Russo|Monopoli|Via Cosimo Pisonio|RRQA|PUBBLICO|Bari|IT|Italy|17.284267|40.961578|ARPAP
|93|Torchiarolo - Fanin     |Torchiarolo|Via FANIN SN - 72020 TORCHIAROLO      |RRQA|PUBBLICO|Brindisi|IT|Italy|18.047226|40.489447|ARPAP
|94|Torchiarolo-Lendinuso|Torchiarolo|C.da MONTEVACCARO SN - 72020 TORCHIAROLO      |IL|PUBBLICO|Brindisi|IT|Italy|18.078880|40.517502|ARPAP
|95|Surbo - Croce |Surbo|Via B. Croce  S.N. - 73010 SURBO    |RRQA|PUBBLICO|Lecce|IT|Italy|18.120835|40.411940|ARPAP
|96|Ceglie Messapica|Ceglie Messapica|via Martina  (Scuola Elementare Papa Giovanni XXIII )|RRQA|PUBBLICO|Brindisi|IT|Italy|17.512500|40.649166|ARPAP
|97|Modugno - EN02|Modugno|Viale delle Magnolie| 6|RRQA|PUBBLICO|Bari|IT|Italy|16.766111|41.107777|ARPAP
|98|Modugno - EN03|Modugno|Via Maranda|RRQA|PUBBLICO|Bari|IT|Italy|16.781672|41.087222|ARPAP
|99|Modugno - EN04|Modugno|Via Ancona|RRQA|PUBBLICO|Bari|IT|Italy|16.787777|41.114444|ARPAP
|100|Cokeria|Taranto|null|ADI|PRIVATO|ILVA|IT|Italy|17.217630|40.502050|ARPAP
|101|Tamburi - Via Orsini|Taranto|null|ADI|PRIVATO|ILVA|IT|Italy|17.225830|40.494510|ARPAP
|102|Riv1|Taranto|null|ADI|PRIVATO|ILVA|IT|Italy|17.216900|40.518570|ARPAP
|103|Direzione|Taranto|null|ADI|PRIVATO|ILVA|IT|Italy|17.200550|40.501980|ARPAP
|104|Meteo Parchi|Taranto|null|ADI|PRIVATO|ILVA|IT|Italy|17.222180|40.496730|ARPAP
|105|Portineria C|Taranto|null|ADI|PRIVATO|ILVA|IT|Italy|17.186560|40.518900|ARPAP
|106|Bitonto - EN01|Bitonto|Agro Di Bitonto|IL|PRIVATO|Bari|IT|Italy|16.745277|41.079166|ARPAP
|107|Palo del Colle - EN05|Palo del Colle|Via Ungaretti|IL|PRIVATO|Bari|IT|Italy|16.700830|41.061388|ARPAP
|108|Cisternino|Cisternino|via Benedetto Croce|RRQA|PUBBLICO|Brindisi|IT|Italy|17.415833|40.742777|ARPAP
|109|Barletta - Mezzo Mobile Via Trani|Barletta|null|IL|PRIVATO|BAT|IT|Italy|16.293055|41.318333|ARPAP
|110|Candela - Scuola|Candela|null|IL|PRIVATO|Foggia|IT|Italy|15.519444|41.133055|ARPAP
|111|Candela - Ex Comes|Candela|null|IL|PRIVATO|Foggia|IT|Italy|15.523055|41.173055|ARPAP
|112|San Severo  - Municipio|San Severo|null|RRQA|PUBBLICO|Foggia|IT|Italy|15.379722|41.696944|ARPAP
|113|Galatina-Colacem|Galatina|Contrada Piani|IL|PUBBLICO|Lecce|IT|Italy|18.192856|40.163964|ARPAP
|114|C1 - Lato sud ovest impianti| Area imprese|Brindisi|Zona industriale| Via Leonardo da Vinci|VERSALIS|PRIVATO|Brindisi|IT|Italy|17.990417|40.628028|ARPAP
|115|C2 - Area bacino idrico|Brindisi|Zona industriale| Via Giuseppe Verdi|VERSALIS|PRIVATO|Brindisi|IT|Italy|17.988500|40.638889|ARPAP
|116|C3 - Area impianto P1CR Cracking|Brindisi|Zona industriale| Via Aldo Moro|VERSALIS|PRIVATO|Brindisi|IT|Italy|17.998139|40.638139|ARPAP
|117|C4 - Area impianto Butadiene|Brindisi|Zona industriale| Via Enrico Fermi|VERSALIS|PRIVATO|Brindisi|IT|Italy|18.002444|40.634444|ARPAP
|118|C5 - Area Pontile|Brindisi|Zona industriale| Via Galileo Galilei|VERSALIS|PRIVATO|Brindisi|IT|Italy|17.989981|40.645450|ARPAP
|119|C6 - Area PE1/2 lato sud impianti|Brindisi|Zona industriale| Via Alessandro Volta|VERSALIS|PRIVATO|Brindisi|IT|Italy|18.001614|40.623753|ARPAP

1. Particolare importanza assume l`individuazione dell``id_station` perchè sarà, di fatto, l`unico dato da modificare nella stringa di lettura dei dati.
1. La stringa di lettura è la seguente:

   https://dati.arpa.puglia.it/api/v1/measurements?language=ITA&format=CSV&network=RRQA&id_station=26&debugMode=false

   può essere utilizzare anche nel normale browser. La sua consultazione genererà il download di un file che potrete leggere ed apprezzare soprattutto perchè per la centralina che avrete individuato, vi consentirà di sapere quali sono i dati pubblicati da ARPA.

1. Sostituire l``id_station` con quello della stazione desiderata:

      `https://dati.arpa.puglia.it/api/v1/measurements?language=ITA&format=CSV&network=RRQA&`**id_station=26**`&debugMode=false`

1. Provate la stringa e se la risposta è giusta (sarà di facile lettura) conservartela per inserirla nel giusto nodo NodeRED. 


    
### 3 - Configurazione Home Assistant

1. Scaricare tutti i files;
1. La seguente configurazione esporrà i sensori in HA come vedete di seguito:

![lovelace1](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Esposizione%20sensori%20in%20HA.png)


1. Nella _Dashbord_ della _lovelace_, dove preferite, aprite una nuova scheda ed incollate il codice del file `HA lovelace.txt`. Sostanzialmente basta elencarli all'nterno della scheda ed il risultato sarà il seguente:

![lovelace2](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Lovelace%20Visualizzazione%20HA.jpg)

codice:
```yaml
type: custom:flex-table-card
title: Valori Ambientali San Pietro Vernotico
entities:
  include:
    - sensor.pm10
    - sensor.pm25
    - sensor.no2
    - sensor.so2
    - sensor.co
    - sensor.c6h6
    - sensor.ipa
  sort_by: name
columns:
  - name: Inquinante
    data: inquinante
  - name: Valore
    data: state
  - name: Unita
    data: unita
  - name: Limite
    data: limite
  - name: Superamenti
    data: superamenti
  - name: Indice qualità
    data: indice_qualita
  - name: Classe qualità
    data: classe_qualita
```

### 4 - Configurazione di Node-RED

1. Copiate ed incollate il contenuto del file `Flusso Node-RED completo.json` in un flow di NodeRED:

`Flusso Node-RED completo.json`:

![nodered1](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Flusso%20Node-RED%20centralina%20completa.jpg)


codice:
```json
[{"id":"83ae842a038866d3","type":"tab","label":"Flow 1","disabled":false,"info":"","env":[]},{"id":"bccfd7c9f2db270f","type":"csv","z":"83ae842a038866d3","name":"","spec":"rfc","sep":",","hdrin":true,"hdrout":"none","multi":"mult","ret":"\\r\\n","temp":"","skip":"0","strings":true,"include_empty_strings":"","include_null_values":"","x":370,"y":380,"wires":[["2324c1401af40bd2"]]},{"id":"2324c1401af40bd2","type":"function","z":"83ae842a038866d3","name":"Estrae i dati delle misurazioni","func":"// Ottieni l'array dal payload\nlet misurazioni = msg.payload;\n\n// Crea un array per memorizzare i risultati\nlet risultati = [];\n\n// Itera su ogni oggetto nell'array\nmisurazioni.forEach((misurazione, index) => {\n    // Estrai i campi che ti interessano\n    let risultato = {\n        data: misurazione.data_di_misurazione,\n        inquinante: misurazione.inquinante_misurato,\n        valore: misurazione.valore_inquinante_misurato,\n        limite: misurazione.limite,\n        unita: misurazione.unita_misura,\n        indice_qualita: misurazione.indice_qualita,\n        classe_qualita: misurazione.classe_qualita,\n        superamenti:misurazione.superamenti\n    };\n\n    // Aggiungi il risultato all'array\n    risultati.push(risultato);\n});\n\n// Imposta il nuovo payload con i risultati\nmsg.payload = risultati;\n\n// Restituisci il messaggio\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":580,"y":380,"wires":[["10c547891c3baf9e"]]},{"id":"10c547891c3baf9e","type":"function","z":"83ae842a038866d3","name":"divide i messaggi per ogni inquinante","func":"// Ottieni l'array dal payload\nlet misurazioni = msg.payload;\n\n// Verifica che ci siano almeno due elementi nell'array\nif (misurazioni.length >= 9) {\n    // Crea due messaggi separati\n    let msg1 = { payload: misurazioni[0] }; // Primo oggetto\n    let msg2 = { payload: misurazioni[1] }; // Secondo oggetto\n    let msg3 = { payload: misurazioni[2] }; // Terzo oggetto\n    let msg4 = { payload: misurazioni[3] }; // Quarto oggetto\n    let msg5 = { payload: misurazioni[4] }; // Quinto oggetto\n    let msg6 = { payload: misurazioni[5] }; // Sesto oggetto\n    let msg7 = { payload: misurazioni[6] }; // settimo oggetto\n    let msg8 = { payload: misurazioni[7] }; // ottavo oggetto\n    let msg9 = { payload: misurazioni[8] }; // nono oggetto\n\n    // Restituisci entrambi i messaggi\n    return [msg1, msg2, msg3, msg4, msg5, msg6, msg7, msg8, msg9];\n} else {\n    // Se non ci sono abbastanza elementi, restituisci un messaggio di errore\n    msg.payload = \"Errore: Il payload non contiene abbastanza elementi.\";\n    return msg;\n}","outputs":9,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":870,"y":380,"wires":[["c78bf7f00a9df94f"],["a92129cd90dbb91c"],["baacb7b203c98073"],["2019bc966017df5c"],["9f95695360a832b5"],["bd3b68228abce048"],["6a89ae6b2939c5f3"],["919b7562c0f30678"],["82a6fa3f55689262"]],"info":"### ## # "},{"id":"2019bc966017df5c","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":320,"wires":[["964487613157f7ea"]]},{"id":"9f95695360a832b5","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":380,"wires":[["2e3d23d81fa8b021"]]},{"id":"82a6fa3f55689262","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":620,"wires":[["2c426179c7e34e13"]]},{"id":"a92129cd90dbb91c","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":200,"wires":[["5d698ec4e9d032aa"]]},{"id":"c78bf7f00a9df94f","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":140,"wires":[["b99287792d0d5571"]]},{"id":"baacb7b203c98073","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":260,"wires":[["5f7a8b7a21430005"]]},{"id":"bd3b68228abce048","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":440,"wires":[["ed56b628a9e49a91"]]},{"id":"6a89ae6b2939c5f3","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":500,"wires":[["25180d3bf051c8e2"]]},{"id":"919b7562c0f30678","type":"function","z":"83ae842a038866d3","name":"formatta in valore \"valore\" in caso di errore","func":"\n    if (msg.payload.valore === \"null\") \n{\n    msg.payload.valore = \"0\";\n}\n\nif (msg.payload.indice_qualita === \"null\") \n{\n    msg.payload.indice_qualita = \"0\";\n}\n\nif (msg.payload.classe_qualita === \"null\") \n{\n    msg.payload.classe_qualita = \"0\";\n}\n\nif (msg.payload.superamenti === \"null\") \n{\n    msg.payload.superamenti = \"0\";\n}\n\nif (msg.payload.limite === \"null\") \n{\n    msg.payload.limite = \"0\";\n}\nreturn msg;","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1350,"y":560,"wires":[["12fc43b684253b6b"]]},{"id":"8e1d2d5c56127fd9","type":"http request","z":"83ae842a038866d3","name":"","method":"GET","ret":"txt","paytoqs":"ignore","url":"https://dati.arpa.puglia.it/api/v1/measurements?language=ITA&format=CSV&id_station=104&debugMode=false","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":230,"y":380,"wires":[["bccfd7c9f2db270f"]]},{"id":"ce883c9ded520944","type":"inject","z":"83ae842a038866d3","name":"12.00","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"00 12 * * *","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":90,"y":380,"wires":[["8e1d2d5c56127fd9"]]},{"id":"b99287792d0d5571","type":"ha-sensor","z":"83ae842a038866d3","name":"PM10","entityConfig":"070b0ec7eda914a4","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":140,"wires":[[]]},{"id":"5d698ec4e9d032aa","type":"ha-sensor","z":"83ae842a038866d3","name":"PM25","entityConfig":"c0818e7cfbb10fe5","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":200,"wires":[[]]},{"id":"5f7a8b7a21430005","type":"ha-sensor","z":"83ae842a038866d3","name":"NO2","entityConfig":"4935b7f1b2b13c1d","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":260,"wires":[[]]},{"id":"964487613157f7ea","type":"ha-sensor","z":"83ae842a038866d3","name":"C6H6","entityConfig":"a048268fc0daaabd","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":320,"wires":[[]]},{"id":"2e3d23d81fa8b021","type":"ha-sensor","z":"83ae842a038866d3","name":"CO","entityConfig":"3442011582531981","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":380,"wires":[[]]},{"id":"ed56b628a9e49a91","type":"ha-sensor","z":"83ae842a038866d3","name":"SO2","entityConfig":"2910e3bdb3d20869","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":440,"wires":[[]]},{"id":"25180d3bf051c8e2","type":"ha-sensor","z":"83ae842a038866d3","name":"H2S","entityConfig":"bffe097716e334ea","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":500,"wires":[[]]},{"id":"12fc43b684253b6b","type":"ha-sensor","z":"83ae842a038866d3","name":"BLACK CARB","entityConfig":"b0fd7353e19107be","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1620,"y":560,"wires":[[]]},{"id":"2c426179c7e34e13","type":"ha-sensor","z":"83ae842a038866d3","name":"IPA","entityConfig":"66e9e5207df39439","version":0,"state":"payload.valore","stateType":"msg","attributes":[{"property":"data","value":"payload.data","valueType":"msg"},{"property":"inquinante","value":"payload.inquinante","valueType":"msg"},{"property":"limite","value":"payload.limite","valueType":"msg"},{"property":"unita","value":"payload.unita","valueType":"msg"},{"property":"indice_qualita","value":"payload.indice_qualita","valueType":"msg"},{"property":"classe_qualita","value":"payload.classe_qualita","valueType":"msg"},{"property":"superamenti","value":"payload.superamenti","valueType":"msg"}],"inputOverride":"allow","outputProperties":[],"x":1590,"y":620,"wires":[[]]},{"id":"070b0ec7eda914a4","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"PM10","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"PM10"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":"measurement"}],"resend":false,"debugEnabled":true},{"id":"c0818e7cfbb10fe5","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"PM25","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"PM25"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm25"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":"measurement"}],"resend":false,"debugEnabled":false},{"id":"4935b7f1b2b13c1d","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"NO2","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"NO2"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":""}],"resend":false,"debugEnabled":false},{"id":"a048268fc0daaabd","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"C6H6","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"C6H6"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":""}],"resend":false,"debugEnabled":false},{"id":"3442011582531981","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"CO","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"CO"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":""}],"resend":false,"debugEnabled":false},{"id":"2910e3bdb3d20869","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"SO2","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"SO2"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":""}],"resend":false,"debugEnabled":false},{"id":"bffe097716e334ea","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"H2S","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"H2S"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":""}],"resend":false,"debugEnabled":false},{"id":"b0fd7353e19107be","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"BLACK CARB","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"BLACK CARB"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":""}],"resend":false,"debugEnabled":false},{"id":"66e9e5207df39439","type":"ha-entity-config","server":"5d1c0eb6.fa674","deviceConfig":"502c0a918e764ed3","name":"IPA","version":6,"entityType":"sensor","haConfig":[{"property":"name","value":"IPA"},{"property":"icon","value":""},{"property":"entity_picture","value":""},{"property":"entity_category","value":""},{"property":"device_class","value":"pm10"},{"property":"unit_of_measurement","value":"µg/m³"},{"property":"state_class","value":""}],"resend":false,"debugEnabled":false},{"id":"5d1c0eb6.fa674","type":"server","name":"Home Assistant","addon":true,"rejectUnauthorizedCerts":true,"ha_boolean":"","connectionDelay":false,"cacheJson":true,"heartbeat":false,"heartbeatInterval":"","areaSelector":"id","deviceSelector":"id","entitySelector":"id","statusSeparator":"","enableGlobalContextStore":true},{"id":"502c0a918e764ed3","type":"ha-device-config","name":"Node-RED","hwVersion":"","manufacturer":"Node-RED","model":"","swVersion":""}]
```


1. Aprite il nodo denominato `http request` e nel campo `URL` copiate ed incollate la stringa ottenuta prima;
1. Riavviate il tutto! Il gioco è fatto!

---

## Personalizzazione ed analisi dei flussi NodeRED

I flussi da me illustrati sono ovviamente meritevoli di sviluppo. Personalmente mi sono occupato di raccogliere i dati esposti dalle centraline vicine alle zone in cui abito ma ciò non toglie che si possano utilizzare tutti i valori a disposizione, ovvero quelli esposti nella tabella "Caratteristiche principali" sopra riportata. 

---

**Commentiamolo:**
--

1. Tramite una chiamata giornaliera alle ore 12.00 lancio l'aggiornamento dei sensori (le rilevazioni sono aggiornate al giorno precedente, quindi non ha senso ripeterla più volte al giorno) tramite il nodo `inject`;
2. Il successivo nodo `http request` è il nodo che invia la stringa per la chiamata dei dati, personalizzabile come detto prima;
3. Il nodo `csv` riceve i dati e li interpreta suddividendoli all'interno di un _array_;
4. Il nodo `function` che segue, denominato `Estrae i dati delle misurazioni`, suddivide l'_array_ ricevuto in stringhe separate producendo più _payload_ per quante sono le righe trasmesse dalla centralina.
     Qui interviene l`ulteriore personalizzazione, come faccio a sapere quali inquinanti espone una centralina? La risposta non è complessa:
     1. andare sul sito dei [dati ARPA](https://dati.arpa.puglia.it/openapi/index.html)
     2. scorrere fino alla Sezione `Misurazioni`
     3. cliccare sul successivo tasto `GET`
     4. poi cliccare sulla destra sul tasto `TRY IT OUT`
     5. inserite nel campo `format` il formato dei dati, vi consiglio `csv` per una maggiore intellegibilità
     6. inserite nel campo `id-station` il numero identificativo della centralina che vi interessa, ad esempio `104`
     7. cliccare su `debug-mode` ed impostare a `true` così da avere la risposta a video (non cambia nulla, se lasciate l`impostazione si  `false` vi scaricherà un file di testo con i dati)
     8. quindi cliccare si `Execute`
     9. dopo pochi secondi otterrete diverse risposte:
        -il link per ottenere i dati, nel caso che ci occupa, sarà:

            https://dati.arpa.puglia.it/api/v1/measurements?language=ITA&format=CSV&id_station=104&debugMode=true

        -Nella successiva sezione `Response body` potremo leggere i seguenti dati:
```yaml
         <pre>=== measurements/executeQuery ===
formatParam: CSV
=== measurements/executeQuery ===
<pre>data_di_misurazione,id_station,denominazione,comune,provincia,Longitude,Latitude,tipologia_di_area,tipologia_di_stazione,rete,interesse_rete,id_pollutant,inquinante_misurato,valore_inquinante_misurato,limite,unita_misura,superamenti,indice_qualita,classe_qualita
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","13","PM10",null,null,"µg/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","12","PM2.5",null,null,"µg/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","4","NO2",null,null,"µg/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","2","C6H6",null,null,"µg/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","1","CO",null,null,"mg/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","6","SO2",null,null,"µg/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","8","H2S",null,null,"µg/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","10","BLACK CARB",null,null,"ng/m³",null,null,null
2025-01-28,104,"Meteo Parchi","Taranto","Taranto",17.222180,40.496730,null,null,"ADI","PRIVATO","11","IPA",null,null,"ng/m³",null,null,null
```

   
5. Il nodo `function` che segue, denominato `divide i messaggi per ogni inquinante`, è dotato di tante uscite quante sono le righe dell'_array_ ricevuto. Quindi se una centralina espone 6 inquinanti, bisognerà modificarlo come segue:
   Nella Scheda `setup` va modificato il numero delle uscite che sarà uguale al numero degli inquinanti acquisiti;
   Nella Scheda `on message` va:
   - modificata la riga `if (misurazioni.length >= 9) {` ed inserito il numero dei valori da acquisire, quelli esposti sopra, esclusa la prima riga, quindi se ci sono righe di dati inseriremo 8;
   -inserita una striga `let msg1 = { payload: misurazioni[0] };` per ogni inquinante esposto, partendo da `misurazioni[0]`, così ad esempio:
```yaml
              let msg1 = { payload: misurazioni[0] }; // Primo oggetto
              let msg2 = { payload: misurazioni[1] }; // Secondo oggetto
              let msg3 = { payload: misurazioni[2] }; // Terzo oggetto
              let msg4 = { payload: misurazioni[3] }; // Quarto oggetto
              let msg5 = { payload: misurazioni[4] }; // Quinto oggetto
              let msg6 = { payload: misurazioni[5] }; // Sesto oggetto
              let msg7 = { payload: misurazioni[6] }; // settimo oggetto
              let msg8 = { payload: misurazioni[7] }; // ottavo oggetto
              let msg9 = { payload: misurazioni[8] }; // nono oggetto
```

ovviamente poi modificheremo anche il successivo messaggio di  `return` del _payload_, inserirendo o eliminando i `msgx` che servono o meno, ottenendo quindi, ad esempio:

```yaml 
          return [msg1, msg2, msg3, msg4, msg5, msg6, msg7, msg8, msg9];` 
```

in questo modo avremo una uscita per ogni inquinante a cui collegheremo, nello stesso ordine mostrato dall'API, il nodo sensore che ritroveremo poi direttamente in HA. I nodi sensore, per maggiore chiarezza e celerità, li ho denominati così come previsto dalla sigla breve utilizzata nella stessa API regionale. La loro configurazione in Node-RED è la seguente:

![NR1](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Configurazione%20nodo%20sensore.png)

con le seguenti proprietà:

![NR2](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Configurazione%20nodo%20sensore%20-%20proprieta.png)


6. Prima di arrivare alla pubblicazione del dato ho dovuto inserire un nuovo nodo `function` denominato `formatta in valore "valore" in caso di errore` che ha lo scopo di sostituire i dati non pervenuti, esposti dalle API con la dicitura `null`, modificandoli in `0`. Questo si è reso necessario perchè altrimenti Home Assistant non è in grado di interpetrare il dato restituendo così un errore generale del sensore che non esporrà nulla.
7. Al primo lancio dell'automazione creata, potremo recarci in HA, e tra le entitá presenti nella scheda `impostazioni/Dispositivi/Node-RED Companion`potremo notare i nostri sensori appena creati. La struttura sará identica per tutti, cambierà solo il nome del sensore. Avremo quindi la seguente visualizzazione:

![HA1](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Esposizione%20sensori%20in%20HA.png) 

con le seguenti caratteristiche individuali:

![HA2](https://github.com/kapkirk/Dati-ambientali-ARPA-Puglia-via-Home-Assistant-e-NodeRED/blob/main/images/Caratteristiche%20del%20sensore%20in%20HA.png) 




8. null`altro! Lavoro finito e buon divertimento a tutti!



---
