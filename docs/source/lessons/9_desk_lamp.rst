.. note::

    Ciao, benvenuto nella Community di appassionati di SunFounder Raspberry Pi, Arduino e ESP32 su Facebook! Approfondisci la tua conoscenza su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime.
    - **Sconti Esclusivi**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Omaggi**: Partecipa a omaggi e promozioni festive.

    👉 Sei pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi stesso!

9. Lampada da Scrivania Dimmerabile
=============================================

Immagina tutte le lampade da scrivania a casa, che diffondono dolcemente la luce sulle tue letture serali o sui progetti notturni. Ti sei mai chiesto come queste lampade riescano a regolare la loro luminosità in modo così fluido? In questa lezione, esploreremo la meccanica e l'elettronica dietro una lampada da scrivania, trasformando la curiosità in conoscenza mentre ne costruiremo una da zero utilizzando Arduino.

.. .. immagine:: img/9_desk_lamp_pot.jpg
..     :larghezza: 500
..     :allinea: centro
    
.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/9_dimmble_led.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Preparati a:

* Decifrare il ruolo delle variabili nell'archiviazione e manipolazione dei dati all'interno degli sketch Arduino.
* Padroneggiare la lettura dei segnali analogici con ``analogRead()``.
* Esplorare il PWM attraverso ``analogWrite()`` per regolare la luminosità del LED.

Alla fine di questa lezione, non solo avrai costruito una lampada da scrivania elettronica completamente funzionante, ma avrai anche approfondito la comprensione di come il software interagisca con l'hardware per dare vita agli oggetti di tutti i giorni. Illuminiamo la nostra conoscenza costruendo una lampada da scrivania che risponde al tuo tocco.


Costruzione del Circuito
------------------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rosso
     - 1 * Resistenza da 220Ω
     - 1 * Potenziometro
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Cavo USB
     - 1 * Breadboard
     - Cavi di Collegamento
     - 1 * Multimetro
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_meter|

**Fasi di Costruzione**

1. Trova un Potenziometro.

Un potenziometro, spesso chiamato pot, funziona come un resistore variabile, il che significa che può regolare la sua resistenza da quasi zero al suo limite massimo. La maggior parte dei potenziometri è marcata con il proprio intervallo. Quello incluso nel tuo kit è designato come un potenziometro 103 (10K), che equivale a 10 kilo-ohm o 10.000 ohm.

.. image:: img/9_dimmer_pot.png
    :width: 200
    :align: center

All'interno del potenziometro c'è una striscia di materiale resistivo con un cursore che si muove lungo di essa. Ogni estremità del materiale resistivo è collegata a un terminale o pin, mostrati di seguito come pin A e B. La resistenza tra i pin A e B è fissa e rappresenta la resistenza massima che il potenziometro può offrire. Per quelli nel tuo kit, la resistenza massima è di 10 kilo-ohm.

.. image:: img/9_dimmer_pot_2.png
    :width: 400
    :align: center

* **A**: Connetti all'alimentazione
* **B**: Connetti a terra
* **C**: Connetti al pin analogico
* **D**: Cursore
* **E**: Striscia resistiva

Il Pin C è collegato al cursore. La resistenza attraverso il cursore, o Pin C, dipende dalla posizione del cursore lungo il materiale resistivo.

.. image:: img/9_dimmer_pot_3.png
    :width: 400
    :align: center

Nei diagrammi schematici, il simbolo per un potenziometro appare tipicamente come un resistore con una freccia attraverso il centro.

.. image:: img/9_dimmer_pot_4.png
    :width: 200
    :align: center


Ora esploriamo come il potenziometro regola la resistenza in un circuito.

2. Collega un potenziometro alla breadboard. Inserisci i suoi tre pin nei fori 30G, 29F, 28G.

.. note::
    Il potenziometro ha un'etichetta "P 103", che indica il suo intervallo di resistenza. Inserisci il potenziometro nella breadboard come mostrato, con il lato etichettato rivolto verso di te.

.. image:: img/9_dimmer_test_pot.png
    :width: 500
    :align: center


3. Per misurare la resistenza del potenziometro, devi inserire un filo in 29J e poi toccarlo con il puntale rosso, e inserire un altro filo in 28J e toccarlo con il puntale nero.

.. image:: img/9_dimmer_test_wore.png
    :width: 500
    :align: center

4. Imposta il multimetro per misurare la resistenza nell'intervallo di 20 kilo-ohm (20K).

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

5. Ruota il potenziometro verso la posizione "1" indicata nel diagramma.

.. image:: img/9_pot_direction.png
    :width: 300
    :align: center
    
6. Registra i valori di resistenza misurati nella tabella.

.. note::
    I valori nella tabella sono le mie misurazioni; i tuoi risultati potrebbero variare. Compilali in base ai tuoi effettivi riscontri.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Punto di Misura
     - Resistenza (kilohm)
   * - 1
     - *1.52*
   * - 2
     - 
   * - 3
     - 

7. Ruota il potenziometro in senso orario verso le posizioni 2 e 3 per misurare la resistenza in ciascun punto e registra i risultati nella tabella.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Measurement Point
     - Resistance (kilohm)
   * - 1
     - *1.52*
   * - 2
     - *5.48*
   * - 3
     - *9.01*

Dai risultati delle misurazioni:

* Ruotando il potenziometro **in senso orario** dalla posizione 1 alla 3, la resistenza tra la posizione 2 e la posizione 1 aumenta.
* Al contrario, ruotando **in senso antiorario** dalla posizione 3 alla 1, la resistenza tra la posizione 2 e la posizione 1 diminuisce.

8. Inserisci l'altra estremità del filo jumper da 28J nel terminale negativo della breadboard.

.. image:: img/9_dimmer_led1_pot_gnd.png
    :width: 500
    :align: center

9. Successivamente, inserisci l'altra estremità del filo jumper da 29J nel pin A0 dell'Arduino Uno R3.

.. image:: img/9_dimmer_led1_pot_a0.png
    :width: 500
    :align: center

10. Infine, collega il potenziometro a 5V inserendo un filo jumper tra il foro 30J della breadboard e il pin 5V dell'Arduino Uno R3.

.. image:: img/9_dimmer_led1_pot_5v.png
    :width: 500
    :align: center


11. Collega il pin GND dell'Arduino Uno R3 al terminale negativo della breadboard utilizzando un lungo filo jumper.

.. image:: img/9_dimmer_led1_gnd.png
    :width: 500
    :align: center

12. Prendi un LED. Inserisci il suo anodo (il pin più lungo) nel foro 13A e il suo catodo (il pin più corto) nel terminale negativo della breadboard.

.. image:: img/9_dimmer_led1_led.png
    :width: 500
    :align: center

13. Inserisci una resistenza da 220 ohm tra i fori 13E e 13G.

.. image:: img/9_dimmer_led1_resistor.png
    :width: 500
    :align: center

14. Collega il foro 13J della breadboard al pin 9 dell'Arduino Uno R3 con un filo.

.. image:: img/9_dimmer_led1_pin9.png
    :width: 500
    :align: center

**Domanda**:

Come pensi che cambierà la tensione su A0 quando il potenziometro viene ruotato in senso orario e antiorario?

Creazione del Codice
-------------------------------------

In questa lezione, l'obiettivo è regolare la luminosità del LED in base alla rotazione del potenziometro.

Ecco come potrebbe apparire il pseudocodice:

.. code-block::

    Crea una variabile per memorizzare le informazioni di input.
    Imposta un pin come output.
    Inizia il ciclo principale:
        Memorizza il valore del potenziometro in una variabile.
        Imposta la luminosità del LED in base alla variabile del potenziometro.
    Termina il ciclo principale.

**Inizializzazione dei Pin**

1. Apri l'IDE di Arduino e inizia un nuovo progetto selezionando “New Sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson9_Desk_Lamp`` usando ``Ctrl + S`` o cliccando su “Salva”.

3. Il LED nel tuo circuito è collegato a un pin digitale sull'Arduino Uno R3, impostato come output. Ricorda di aggiungere un commento.


.. note::

    Il potenziometro è un dispositivo di input analogico collegato al pin analogico A0. Tutti i pin analogici su Arduino sono pin di input, il che significa che non devono essere dichiarati come INPUT come i pin digitali.
    
.. code-block:: Arduino
    :emphasize-lines: 3

    void setup() {
        // inserisci qui il codice di setup, eseguito una volta:
        pinMode(9, OUTPUT);  // Imposta il pin 9 come output
    }

    void loop() {
        // inserisci qui il codice principale, eseguito ripetutamente:
    }

**Dichiarazione delle Variabili**

Per controllare la dissolvenza del LED utilizzando un potenziometro, è necessaria una **variabile** per memorizzare il valore del potenziometro.

Approfondiamo il concetto di variabili nella programmazione. Una variabile funziona come un contenitore nel tuo programma, permettendoti di memorizzare e successivamente recuperare informazioni.

.. image:: img/9_variable_define.png
    :width: 400
    :align: center

Prima di utilizzare una variabile, deve essere dichiarata, processo noto come dichiarazione di variabile.

Per dichiarare una variabile, devi definirne il tipo e il nome. Non è necessario assegnare un valore alla variabile al momento della dichiarazione—puoi assegnarlo in seguito nel tuo sketch. Ecco come dichiarare una variabile:

.. code-block:: Arduino

    int var;

Qui, ``int`` è il tipo di dato utilizzato per i numeri interi, in grado di memorizzare valori da -32768 a 32767. Le variabili possono memorizzare vari tipi di dati, tra cui ``float``, ``byte``, ``boolean``, ``char`` e ``string``.

I nomi delle variabili possono essere qualsiasi cosa tu scelga, come ``i``, ``mela``, ``Bruce``, ``R2D2`` o ``Sectumsempra``. Tuttavia, ci sono delle regole per la loro denominazione:

* I nomi possono includere lettere, cifre e trattini bassi, ma non spazi o caratteri speciali come !, #, %, ecc.

  .. image:: img/9_variable_name1.png
    :width: 400
    :align: center

* I nomi devono iniziare con una lettera o un trattino basso (_). Non possono iniziare con un numero.

  .. image:: img/9_variable_name2.png
    :width: 400
    :align: center

* I nomi fanno distinzione tra maiuscole e minuscole. ``myCat`` e ``mycat`` sarebbero considerate variabili diverse.

* Evita di utilizzare parole chiave che l'IDE di Arduino riconosce e mette in evidenza, come ``int``, che viene colorata per indicarne il significato speciale. Se il nome diventa di un colore come arancione o blu, è una parola chiave e dovrebbe essere evitata come nome di variabile.


L'ambito di una variabile determina dove può essere utilizzata nel tuo sketch, in base a dove viene dichiarata.

* Una variabile dichiarata al di fuori di tutte le funzioni (cioè al di fuori di qualsiasi parentesi graffa) è una variabile globale e può essere utilizzata ovunque nel tuo sketch.
* Una variabile dichiarata all'interno di una funzione (all'interno di una coppia di parentesi graffe) è una variabile locale e può essere utilizzata solo all'interno di quella funzione.

.. code-block:: Arduino
    :emphasize-lines: 1,4,9

    int variabile_globale = 0; // Questa è una variabile globale

    void setup() {
        int variabile = 0; // Questa è una variabile locale
    }

    void loop() {
        int variabile = 0; // Questa è un'altra variabile locale
    }

.. note::

    Le variabili locali possono essere utilizzate solo all'interno delle funzioni in cui sono dichiarate, il che significa che puoi dichiarare variabili con lo stesso nome in diverse funzioni senza problemi. Tuttavia, evita di usare lo stesso nome sia per le variabili locali che globali per evitare confusione.

Tipicamente, uno sketch di Arduino dovrebbe seguire un modello coerente: dichiarare prima le variabili globali, quindi definire la funzione ``void setup()`` e infine la funzione ``void loop()``.

4. Vai all'inizio del tuo sketch, prima della funzione ``void setup()``. Qui dichiarerai la variabile per memorizzare il valore del potenziometro.

.. code-block:: Arduino
    :emphasize-lines: 1

    int potValue = 0;

    void setup() {
        // inserisci qui il codice di setup, eseguito una volta:
        pinMode(9, OUTPUT);  // Imposta il pin 9 come output
    }

    void loop() {
        // inserisci qui il codice principale, eseguito ripetutamente:
    }

Hai appena dichiarato una variabile intera chiamata ``potValue`` e l'hai impostata a zero. Questa variabile verrà utilizzata successivamente nel tuo sketch per memorizzare l'output del potenziometro.

**Lettura di Valori Analogici**

Ora sei pronto per entrare nel ciclo principale del programma. La prima cosa che farai nella funzione ``void loop()`` è determinare il valore del potenziometro.

Il potenziometro è collegato a un pin di alimentazione da 5 volt, consentendo alla tensione sul pin A0 di variare da 0 a 5 volt. Questa tensione viene quindi convertita dal microprocessore dell'Arduino Uno R3 in un valore analogico compreso tra 0 e 1023, grazie alla risoluzione a 10 bit del microprocessore.

Una volta convertiti, questi valori analogici possono essere utilizzati all'interno del programma.

Per ottenere il valore analogico dal potenziometro, utilizza il comando ``analogRead(pin)``. Questo comando legge la tensione che entra in un pin analogico e la mappa su un valore compreso tra 0 e 1023:

- Se non c'è tensione, il valore analogico è 0.
- Se la tensione è di 5 volt pieni, il valore analogico sarà 1023.

Ecco come utilizzarlo:

    * ``analogRead(pin)``: Legge il valore dal pin analogico specificato.

    **Parametri**
        - ``pin``: il nome del pin di ingresso analogico da cui leggere.

    **Ritorna**
        Il valore analogico sul pin. Anche se è limitato alla risoluzione del convertitore da analogico a digitale (0-1023 per 10 bit o 0-4095 per 12 bit). Tipo di dato: int.

5. Inserisci il seguente comando all'interno della funzione ``void loop()`` per memorizzare il valore analogico del potenziometro nella variabile ``potValue`` dichiarata all'inizio del tuo sketch:

.. code-block:: Arduino
    :emphasize-lines: 10

    int potValue = 0;

    void setup() {
        // inserisci qui il codice di setup, eseguito una volta:
        pinMode(9, OUTPUT);  // Imposta il pin 9 come output
    }

    void loop() {
        // inserisci qui il codice principale, eseguito ripetutamente:
        potValue = analogRead(A0);        // Leggi il valore dal potenziometro
    }

Assicurati di salvare e verificare il tuo codice per correggere eventuali errori.

**Scrittura di Valori Analogici**

I pin digitali sull'Arduino Uno R3 possono assumere solo stati ON o OFF, il che significa che non possono emettere veri valori analogici. Per simulare un comportamento analogico per applicazioni come il controllo della luminosità di un LED, utilizziamo una tecnica chiamata modulazione di larghezza di impulso (PWM). I pin PWM, contrassegnati da una tilde (~) sulla scheda, possono variare l'output percepito regolando il ciclo di lavoro del segnale.

.. image:: img/9_dimmer_pwm_pin.png
    :width: 500
    :align: center

Per controllare la luminosità di un LED, utilizziamo il comando ``analogWrite(pin, value)``. Questo regola la luminosità del LED cambiando il ciclo di lavoro del segnale PWM inviato al pin.

    * ``analogWrite(pin, value)``: Scrive un valore analogico (onda PWM) su un pin. Può essere utilizzato per accendere un LED con luminosità variabile o per guidare un motore a velocità variabili. 

    **Parametri**
        - ``pin``: il pin Arduino su cui scrivere. Tipi di dato consentiti: int.
        - ``value``: il ciclo di lavoro: tra 0 (sempre spento) e 255 (sempre acceso). Tipi di dato consentiti: int.
    
    **Ritorna**
        Nessun valore

Pensa al ciclo di lavoro come al flusso di un rubinetto che controlla l'acqua che entra in un secchio, rappresentando la luminosità del LED. Ecco una semplice spiegazione:

* ``analogWrite(255)`` significa che il rubinetto è completamente aperto tutto il tempo, riempiendo completamente il secchio e rendendo il LED più luminoso.
* ``analogWrite(191)`` significa che il rubinetto è aperto al 75% del tempo, riempiendo il secchio parzialmente e rendendo il LED meno luminoso.
* ``analogWrite(0)`` significa che il rubinetto è completamente chiuso, lasciando il secchio vuoto e il LED spento.

.. image:: img/9_pwm_signal.png
    :width: 400
    :align: center

6. Aggiungi un comando ``analogWrite()`` nella funzione ``void loop()`` e commenta ogni riga per chiarezza:

.. note::

    * Poiché l'intervallo di input del potenziometro è da 0 a 1023, ma l'intervallo di output per i LED è da 0 a 255, puoi ridurre il valore del potenziometro dividendo per 4:

    * Sebbene il risultato della divisione potrebbe non essere sempre un numero intero, solo la parte intera viene memorizzata poiché le variabili sono dichiarate come interi (int).


.. code-block:: Arduino
    :emphasize-lines: 11

    int potValue = 0;

    void setup() {
        // inserisci qui il codice di setup, eseguito una volta:
        pinMode(9, OUTPUT);  // Imposta il pin 9 come output
    }

    void loop() {
        // inserisci qui il codice principale, eseguito ripetutamente:
        potValue = analogRead(A0);        // Leggi il valore dal potenziometro
        analogWrite(9, potValue / 4);       // Applica la luminosità al LED sul pin 9
    }

7. Una volta caricato il codice sull'Arduino Uno R3, ruotando il potenziometro cambierà la luminosità dei LED. Secondo la nostra configurazione, ruotando il potenziometro in senso orario dovrebbe aumentare la luminosità, mentre ruotandolo in senso antiorario dovrebbe diminuirla.

.. note::

    Il debug spesso richiede di controllare sia il codice che il circuito per rilevare eventuali errori. Se il codice viene compilato correttamente o sembra corretto, ma i LED non cambiano come previsto, il problema potrebbe risiedere nel circuito. Controlla tutte le connessioni e i componenti sulla breadboard per assicurarti che siano ben collegati.

8. Infine, ricordati di salvare il tuo codice e di sistemare il tuo spazio di lavoro.

**Domanda**

Se colleghi il LED a un pin diverso, come il pin 8, e ruoti il potenziometro, la luminosità del LED cambierà ancora? Perché o perché no?

**Riepilogo**

In questa lezione, abbiamo esplorato come lavorare con i segnali analogici nei progetti Arduino. Abbiamo imparato a leggere i valori analogici da un potenziometro, come elaborare questi valori nello sketch Arduino e come controllare la luminosità del LED utilizzando la modulazione di larghezza di impulso (PWM). Abbiamo anche approfondito l'uso delle variabili per memorizzare e manipolare i dati nei nostri sketch. Integrando questi elementi, abbiamo dimostrato il controllo dinamico dei componenti elettronici, colmando il divario tra semplici output digitali e un controllo più sfumato dell'hardware tramite letture di input analogici.
