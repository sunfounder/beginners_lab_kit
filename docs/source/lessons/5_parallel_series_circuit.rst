.. note::

    Ciao, benvenuto nella SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 con altri appassionati.

    **Perché unirti a noi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima a nuovi annunci di prodotti.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a omaggi e promozioni speciali.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi stesso!


5. Circuito in Serie vs. Circuito in Parallelo
====================================================

In questa lezione, ti cimenterai nella costruzione e nell'analisi di circuiti in serie e in parallelo, imparando a misurare e comprendere come si comporta la tensione in diverse configurazioni di circuiti. Utilizzando un multimetro, misurerai la tensione e la resistenza dei circuiti che costruirai, acquisendo conoscenze pratiche sulla dinamica dei circuiti.

In questa lezione entusiasmante, imparerai a:

* Collegare i diagrammi schematici ai circuiti reali.
* Usare un multimetro per misurare resistenza e tensione.
* Costruire circuiti in serie e in parallelo usando una breadboard.
* Confrontare il comportamento della tensione nei circuiti in serie e in parallelo.

Questi obiettivi ti permetteranno di colmare il divario tra conoscenza teorica e applicazione pratica, arricchendo la tua comprensione dell'elettronica attraverso l'esperienza diretta.


Circuito in Serie vs. Circuito in Parallelo
------------------------------------------------

Nelle lezioni precedenti, abbiamo costruito con successo un semplice circuito con un Arduino Uno R3, un resistore e un LED. La corrente in questa configurazione scorre in serie: dal Pin 13 della scheda, attraverso il LED, il resistore e torna al pin GND. Questo è un esempio semplice di circuito in serie.

Ma addentrandoci nel mondo dell'elettronica, incontriamo circuiti più complessi, con componenti disposti in serie o in parallelo. Per comprendere queste configurazioni e le loro implicazioni sulla corrente e sulla tensione, dobbiamo familiarizzare con i diagrammi dei circuiti, noti anche come schemi elettrici.

**Diagrammi di Cablaggio vs. Schemi Elettrici**

Abbiamo usato diagrammi di cablaggio—rappresentazioni pittoriche che imitano la disposizione fisica dei componenti del circuito. Questi diagrammi sono intuitivi e utili per scopi di assemblaggio:

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

Tuttavia, per comprendere la funzionalità e la logica del design di un circuito, gli schemi elettrici sono indispensabili. Gli schemi elettrici distillano i circuiti alla loro essenza, utilizzando simboli standardizzati per rappresentare ogni componente. Mostrano le relazioni elettriche tra i componenti senza la complessità delle disposizioni fisiche.

Ecco i simboli per un LED, un resistore e una batteria che troverai spesso negli schemi elettrici:

.. image:: img/5_led_resistor_symbol.png
  :align: center

Un diagramma schematico basato sul nostro cablaggio precedente apparirebbe così, con l'intero Arduino Uno R3 che agisce come una batteria per alimentare il circuito. Da questo schema, puoi chiaramente indicare il flusso e la direzione della corrente, semplificando la complessità dei collegamenti fisici.

.. image:: img/5_serial_circuit_1led.png
  :align: center

**Configurazioni in Serie vs. in Parallelo**

In un circuito in serie, i componenti sono allineati in fila, quindi la corrente ha un unico percorso da seguire. Se un componente si guasta, l'intero circuito si interrompe—un po' come una vecchia catena di luci natalizie, dove una lampadina bruciata spegne l'intera fila.

.. image:: img/5_serial_circuit_2led.png
  :align: center

Un circuito in parallelo, d'altra parte, divide la corrente in percorsi multipli. Ogni componente funziona in modo indipendente, quindi se un percorso si interrompe, gli altri continuano a funzionare. Pensa al sistema elettrico di casa: se spegni una luce, la TV può comunque rimanere accesa.

.. image:: img/5_parallel_circuit.png
  :align: center


Esplorare i Circuiti in Serie
----------------------------------

Basandoci sulla comprensione delle differenze tra i circuiti in serie e in parallelo, questa attività si concentra sulla costruzione di un circuito in serie con più LED. Ricorda, in un circuito in serie, la corrente elettrica scorre attraverso un unico percorso. Esploriamo le caratteristiche uniche dei circuiti in serie attraverso questo esercizio pratico.

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 3 * LED Rossi
     - 3 * Resistenza da 220Ω
     - Cavi di collegamento
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Cavo USB
     - 1 * Breadboard
     - 1 * Multimetro
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     - 

**Costruzione del Circuito**

1. Modifica il circuito del LED precedente rimuovendo il cavo tra 1J e il lato positivo della breadboard a destra. Quindi, prendi un altro LED rosso e inserisci il suo catodo (la gamba più corta) in 1J e l'anodo nel lato positivo della breadboard, in modo da collegare un altro LED in serie nel circuito.

.. image:: img/5_serial_circuit.png

Ora hai un circuito in serie con due LED. Segui il flusso della corrente attraverso il circuito:

* La corrente fluisce dal pin 5V sull'Arduino Uno R3, attraverso un lungo cavo di collegamento fino al terminale positivo della breadboard.
* Quindi la corrente fluisce attraverso il primo LED, illuminandolo grazie al passaggio della corrente.
* La corrente poi fluisce attraverso le clip metalliche della breadboard fino al secondo LED, che si illumina anch'esso.
* Dopo aver attraversato il secondo LED, la corrente entra nella resistenza da 220Ω, dove incontra una resistenza che riduce la quantità di corrente. Senza questa resistenza, la corrente che attraversa i LED sarebbe troppo alta e potrebbe bruciarli.
* Infine, la corrente torna al pin di terra dell'Arduino Uno R3, completando il circuito.

**Domanda:** 

In questo circuito in serie, cosa accade se rimuovi uno dei LED? Perché accade questo?

.. image:: img/5_serial_circuit_remove.png
    :width: 600
    :align: center


**Misurare la Tensione**

1. Imposta il multimetro sulla posizione 20 volt DC.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Usa il multimetro per misurare la tensione attraverso la resistenza.

    .. note::
        
        Misurare la tensione di un componente in un circuito significa controllare la tensione ai suoi capi. Essenzialmente, la tensione rappresenta la differenza di energia tra due punti. Quindi, quando misuri la tensione di un componente, stai valutando la differenza di energia da un lato all'altro.

.. image:: img/5_serial_circuit_voltage_resistor.png
    :width: 600
    :align: center

3. Registra la tensione attraverso la resistenza, unità di tensione: Volt (V).

.. note::

    * La mia lettura era di 1,13V, dovresti inserire il valore secondo la tua misurazione.

    * A causa di problemi di cablaggio e dell'instabilità della tua mano, potresti vedere la tensione fluttuare. Mantieni la mano ferma e osserva più volte per ottenere un valore di tensione abbastanza stabile.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Tensione Resistenza
     - Tensione LED1
     - Tensione LED2
     - Tensione Totale 
   * - 2 LED
     - *≈1,13 volt*
     - 
     - 
     - 

4. Ora, misura la tensione attraverso il LED 1 nel circuito.

.. image:: img/5_serial_circuit_voltage_led1.png
    :width: 600
    :align: center

5. Registra la tensione misurata attraverso il LED 1 nella tabella.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Tensione Resistenza
     - Tensione LED1
     - Tensione LED2
     - Tensione Totale 
   * - 2 LED
     - *≈1,13 volt*
     - *≈1,92 volt*
     - 
     - 

6. Misura la tensione attraverso il LED 2 nel circuito.

.. image:: img/5_serial_circuit_voltage_led2.png
    :width: 600
    :align: center

7. Registra la tensione misurata attraverso il LED 2 nella tabella.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Tensione Resistenza
     - Tensione LED1
     - Tensione LED2
     - Tensione Totale 
   * - 2 LED
     - *≈1,13 volt*
     - *≈1,92 volt*
     - *≈1,92 volt*
     - 

8. Ora misura la tensione totale nel circuito.

.. image:: img/5_serial_circuit_voltage.png
    :width: 600
    :align: center

9. Inserisci la tensione totale misurata nella colonna della tabella.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Tensione Resistenza
     - Tensione LED1
     - Tensione LED2
     - Tensione Totale 
   * - 2 LED
     - *≈1,13 volt*
     - *≈1,92 volt*
     - *≈1,92 volt*
     - *≈4,97 volt*


Attraverso le nostre misurazioni, scoprirai:

.. code-block::

  4,97 volt ≈ 1,13 volt + 1,92 volt + 1,92 volt

  Tensione Totale = Tensione Resistenza + Tensione LED 1 + Tensione LED 2

Puoi anche calcolare se i risultati delle tue misurazioni corrispondono a questa equazione.

.. note::
    
    A causa della stabilità del cablaggio o di lievi differenze di fabbricazione nei LED e nella resistenza, la somma delle tensioni della resistenza e dei due LED potrebbe non corrispondere esattamente alla tensione totale misurata. Va bene lo stesso, purché la differenza rientri in un intervallo ragionevole.


Questa è una caratteristica di un circuito in serie, dove la tensione totale attraverso il circuito è la somma delle tensioni attraverso ciascun componente.

**Misurare la Corrente**

Dopo aver compreso le caratteristiche della tensione nei circuiti in serie, esploriamo ora la corrente nel circuito utilizzando un multimetro.

1. Imposta il multimetro sulla posizione 20 milliampere. La corrente non supererà i 20mA, quindi questa impostazione è appropriata. Se non sei sicuro, si consiglia di iniziare con l'impostazione a 200mA.

.. image:: img/multimeter_20a.png
  :width: 300
  :align: center

2. Per misurare la corrente, il multimetro deve essere integrato nel percorso del flusso del circuito. Mantieni l'anodo del LED nel foro 1F e sposta il catodo (la gamba più corta) da 1E a 3E.

.. image:: img/5_serial_circuit_led1_current.png
    :width: 600
    :align: center

3. Misura la corrente attraverso il LED 1 nel circuito.

.. image:: img/5_serial_circuit_led1_current1.png
    :width: 600
    :align: center

4. Registra la corrente misurata nella tabella.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Corrente LED1
     - Corrente LED2
   * - 2 LED
     - *≈4,43 milliampere*
     - 

5. Sposta il catodo del primo LED nella sua posizione originale e sposta il catodo del secondo LED (la gamba più corta) dal foro 1J al foro 2J.

.. image:: img/5_serial_circuit_led2_current.png
    :width: 600
    :align: center

6. Misura la corrente attraverso il LED 2 nel circuito.

.. image:: img/5_serial_circuit_led2_current1.png
    :width: 600
    :align: center

7. Registra la corrente misurata nella tabella.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Corrente LED1
     - Corrente LED2
   * - 2 LED
     - *≈4,43 milliampere*
     - *≈4,43 milliampere*

Le nostre misurazioni hanno illustrato un principio fondamentale dei circuiti in serie: la corrente che scorre attraverso ciascun componente è identica. Questo flusso costante sottolinea l'interconnessione dei componenti in serie, dove l'interruzione di corrente in una parte influenza l'intero circuito.

L'esplorazione della tensione, della corrente e della resistenza non solo arricchisce la nostra comprensione dei circuiti in serie, ma getta anche le basi per concetti di ingegneria elettrica più complessi. Attraverso questi esperimenti pratici, colmiamo il divario tra teoria e applicazione pratica, rendendo il processo di apprendimento sia coinvolgente che informativo.

**Domanda**

Se viene aggiunto un altro LED a questo circuito, risultando in tre LED, come cambia la luminosità dei LED? Perché? Come cambiano le tensioni attraverso i tre LED?




Esplorando i Circuiti Paralleli
---------------------------------------

**Componenti Necessari**

* 1 * Arduino Uno R3
* 3 * LED Rossi
* 3 * Resistenze da 220Ω
* Diversi Cavi Jumper
* 1 * Cavo USB
* 1 * Breadboard
* 1 * Multimetro con Sonde

**Costruzione del Circuito**

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center
  
1. Collega una resistenza da 220Ω alla breadboard. Un'estremità dovrebbe essere nel terminale negativo, e l'altra estremità nel foro 1B.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Aggiungi un LED rosso alla breadboard. L'anodo (gamba lunga) del LED dovrebbe essere nel foro 1F. Il catodo (gamba corta) dovrebbe essere nel foro 1E.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Usa un cavo jumper corto per collegare il LED e la fonte di alimentazione. Un'estremità del cavo jumper dovrebbe essere nel foro 1J. L'altra estremità dovrebbe essere nel terminale positivo.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Collega il cavo jumper lungo collegato al terminale positivo della breadboard al pin 5V dell'Arduino Uno R3. Il LED dovrebbe accendersi e rimanere acceso. Il pin 5V fornisce una tensione costante di 5 volt DC al circuito. Questo è diverso dal pin 13, che può essere programmato tramite il software Arduino IDE per accendersi e spegnersi.

.. image:: img/5_parallel_circuit_5v.png
    :width: 600
    :align: center

5. Collega il terminale negativo della breadboard a uno dei pin di terra dell'Arduino Uno R3. I pin di terra sono contrassegnati come "GND".

.. image:: img/5_parallel_circuit_gnd.png
    :width: 600
    :align: center

6. Prendi un'altra resistenza da 220Ω, collega un'estremità al terminale negativo e l'altra estremità al foro 6B.

.. image:: img/5_parallel_circuit_resistor.png
    :width: 600
    :align: center

7. Prendi un altro LED rosso. L'anodo (gamba lunga) del LED dovrebbe essere nel foro 6F. Il catodo (gamba corta) dovrebbe essere nel foro 6E.

.. image:: img/5_parallel_circuit_led.png
    :width: 600
    :align: center

8. Infine, posiziona un'estremità di un cavo jumper corto nel foro 6J e l'altra estremità nel terminale positivo. Questo completa il circuito parallelo.

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center


Ora, questo circuito ha due LED in una configurazione parallela. Ci sono due percorsi per il flusso della corrente:

* Nel primo percorso: la corrente entra nel primo LED dal cavo jumper, scorre attraverso la resistenza limitatrice di corrente, e poi nel lato negativo della breadboard.
* Nel secondo percorso: la corrente entra nel secondo LED dal cavo jumper, scorre attraverso la resistenza limitatrice di corrente, e poi nel lato negativo della breadboard.
* Nel lato negativo, i due percorsi si convergono di nuovo e poi scorrono attraverso il cavo di alimentazione nero per raggiungere il pin di terra dell'Arduino Uno R3.

**Domanda:**

In questo circuito parallelo, cosa succede se viene rimosso un LED? Perché accade questo?

.. image:: img/5_parallel_circuit_remove.png
    :width: 600
    :align: center


**Passaggi per la Misurazione della Tensione**

1. Imposta il multimetro sulla modalità 20 volt DC.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Ricorda che in un circuito parallelo ogni ramo riceve l'intera tensione dalla sorgente di alimentazione. Pertanto, ogni ramo nel tuo circuito dovrebbe mostrare circa 5 volt. Inizia misurando la tensione lungo il primo percorso.

.. image:: img/5_parallel_circuit_voltage1.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Tensione Percorso 1
     - Tensione Percorso 2
   * - 2 LED
     - *≈5.00 volt*
     - 

3. Ora controlla la caduta di tensione lungo il secondo percorso. Anche qui, attenditi circa 5 volt.

.. image:: img/5_parallel_circuit_voltage2.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Tensione Percorso 1
     - Tensione Percorso 2
   * - 2 LED
     - *≈5.00 volt*
     - *≈5.00 volt*

Il nostro esercizio di misurazione della tensione in un circuito parallelo dimostra chiaramente che ogni ramo riceve una porzione uguale della tensione totale dalla sorgente, circa 5 volt in questo caso. Questa coerenza tra i percorsi conferma la natura fondamentale dei circuiti paralleli, in cui la tensione rimane costante su ciascun ramo, nonostante piccole variazioni dovute a differenze di fabbricazione nei componenti come LED e resistenze.

**Passaggi per la Misurazione della Corrente**

Dalle misurazioni precedenti abbiamo appreso che ogni ramo in un circuito parallelo riceve la tensione completa dalla sorgente. Ma che dire della corrente? Ora andiamo a misurarla.

1. Imposta il multimetro sulla modalità 200 milliampere.

.. image:: img/multimeter_200ma.png
    :width: 300
    :align: center

2. Per misurare la corrente, il multimetro deve essere integrato nel percorso del flusso del circuito. Lascia un'estremità della resistenza collegata al terminale negativo della breadboard e sposta l'altra estremità nel foro 3B.

.. note::
    
    Questo passaggio farà spegnere il LED 1 mentre il LED 2 rimarrà acceso. Questo dimostra una caratteristica dei circuiti paralleli: la disconnessione di un percorso non influisce sugli altri.

.. image:: img/5_parallel_circuit_led1_current.png
    :width: 600
    :align: center

3. Posiziona i cavi rosso e nero del multimetro tra il LED e la resistenza, e vedrai che il LED1 si riaccenderà.

.. image:: img/5_parallel_circuit_led1_current1.png
    :width: 600
    :align: center

4. Registra la corrente misurata nella tabella.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Corrente LED1
     - Corrente LED2
     - Corrente Totale
   * - 2 LED
     - *≈12,6 milliampere*
     - 
     - 

5. Riporta la prima resistenza nella sua posizione originale e lascia un'estremità della seconda resistenza nel terminale negativo della breadboard, spostando l'altra estremità nel foro 9B.

.. image:: img/5_parallel_circuit_led2_current.png
    :width: 600
    :align: center

6. Ora misura la corrente attraverso il LED 2 nel circuito.

.. image:: img/5_parallel_circuit_led2_current1.png
    :width: 600
    :align: center

7. Registra la corrente misurata nella tabella.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Corrente LED1
     - Corrente LED2
     - Corrente Totale
   * - 2 LED
     - *≈12,6 milliampere*
     - *≈12,6 milliampere*
     - 

8. Dopo aver misurato la corrente in entrambi i percorsi, qual è la corrente totale quando i percorsi convergono? Ora, sposta il cavo jumper dal terminale negativo della breadboard al foro 25C.

.. image:: img/5_parallel_circuit_total_current.png
    :width: 600
    :align: center

9. Misura ora la corrente totale del circuito.

.. image:: img/5_parallel_circuit_total_current1.png
    :width: 600
    :align: center

10. Inserisci i risultati misurati nella tabella.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Corrente LED1
     - Corrente LED2
     - Corrente Totale
   * - 2 LED
     - *≈12,6 milliampere*
     - *≈12,6 milliampere*
     - *≈25,3 milliampere*

La nostra esplorazione dei circuiti paralleli ha illuminato un aspetto fondamentale: la corrente totale rispecchia la somma delle correnti individuali di ciascun ramo, seguendo i principi fondamentali dei circuiti elettrici. Questa attività pratica non solo rafforza la nostra comprensione dei circuiti paralleli, ma evidenzia anche il comportamento distinto rispetto ai circuiti in serie, offrendo un quadro chiaro di come i componenti in parallelo condividano il carico elettrico. Mentre proseguiamo nel nostro viaggio nel mondo dell'elettronica, queste intuizioni gettano le basi per indagini più approfondite sul design e sulla funzionalità dei circuiti.

**Domanda**:

1. Se aggiungi un altro LED a questo circuito, cosa accade alla luminosità dei LED? Perché? Annota la tua risposta nel manuale.

.. image:: img/5_parallel_circuit_3led.png
    :width: 600
    :align: center

Riepilogo dei Circuiti in Serie e in Parallelo
-----------------------------------------------------

**Circuiti in Serie**

* **Vantaggi**: Poiché la corrente è la stessa in tutto il circuito, è facile controllare la corrente. Se un componente si guasta, la corrente si interrompe. Il cablaggio è più semplice, riducendo i costi per costruire circuiti di grandi dimensioni.
* **Svantaggi**: Se una parte del circuito si danneggia, l'intero circuito smette di funzionare. Dato che la corrente nel circuito è costante, non puoi usare componenti che richiedono correnti diverse.

**Circuiti in Parallelo**

* **Vantaggi**: Se un percorso del circuito viene scollegato, non influisce sugli altri rami del circuito. Un dispositivo in un ramo può funzionare indipendentemente dagli altri dispositivi. Si possono aggiungere facilmente altri rami al circuito in qualsiasi momento.
* **Svantaggi**: Man mano che vengono aggiunti più dispositivi al circuito, viene assorbita più corrente. Questo può diventare pericoloso poiché il circuito si surriscalda, potenzialmente portando a incendi. Fusibili o interruttori vengono utilizzati per scollegare il circuito quando la corrente è troppo alta per evitare il surriscaldamento. Il cablaggio è più complesso, aumentando i costi di costruzione di grandi circuiti.

**Regole dei Circuiti in Serie e in Parallelo**

Ecco le regole per i circuiti in serie e in parallelo, che puoi continuare a verificare con un multimetro:

.. .. list-table::
..    :widths: 10 25 25 25
..    :header-rows: 1

..    * - Circuit
..      - Voltage
..      - Current
..      - Resistance  
..    * - Series
..      - The total voltage of the circuit equals the sum of the voltages used by each component (Total voltage = V1 + V2 + V3 + ...).
..      - The current at any point in the circuit is the same (Total current = I1 = I2 = I3 = ...).
..      - The total resistance of a circuit equals the sum of the resistances of each component (Total resistance = R1 + R2 + R3 + ...).
..    * - Parallel
..      - The voltage used by each load equals the total voltage used by the circuit (Total voltage = V1 = V2 = V3 = ...)
..      - The total current of the circuit equals the sum of the currents used by each component (Total current = I1 + I2 + I3 + ...).
..      - The reciprocal of the total resistance equals the sum of the reciprocals of each component's resistance (1/ Total resistance = 1/R1 + 1/R2 + 1/R3 + ...)   


**Serie**

  - La tensione totale del circuito è uguale alla somma delle tensioni utilizzate da ciascun componente (Tensione totale = V1 + V2 + V3 + ...).
  - La corrente in qualsiasi punto del circuito è la stessa (Corrente totale = I1 = I2 = I3 = ...).
  - La resistenza totale di un circuito è uguale alla somma delle resistenze di ciascun componente (Resistenza totale = R1 + R2 + R3 + ...).

**Parallelo**

  - La tensione utilizzata da ciascun carico è uguale alla tensione totale utilizzata dal circuito (Tensione totale = V1 = V2 = V3 + ...).
  - La corrente totale del circuito è uguale alla somma delle correnti utilizzate da ciascun componente (Corrente totale = I1 + I2 + I3 + ...).
  - Il reciproco della resistenza totale è uguale alla somma dei reciproci delle resistenze di ciascun componente (1/Resistenza totale = 1/R1 + 1/R2 + 1/R3 + ...).
