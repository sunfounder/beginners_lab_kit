.. note::

    Ciao, benvenuto nella comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché unirti?**

    - **Supporto Esperti**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotti e anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Omaggi**: Partecipa a omaggi e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi stesso!

12. I Colori dell'Arcobaleno
=======================================
Immagina di poter dipingere con la luce, mescolando rosso, verde e blu per creare ogni sfumatura immaginabile, proprio come mescolare i colori su una tavolozza ma con fasci di luce.

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

Benvenuto in questa lezione, dove esplorerai il mondo affascinante dei LED RGB e scoprirai come la combinazione dei colori primari possa creare uno spettro vibrante di tonalità. Questo corso pratico ti guiderà attraverso i principi di funzionamento dei LED RGB e ti introdurrà alle applicazioni pratiche della programmazione e della costruzione di circuiti.

In questa lezione imparerai a:

* Comprendere i principi operativi dei LED RGB.
* Creare e utilizzare funzioni nel tuo codice per semplificare i compiti e migliorare la leggibilità.
* Esplorare l'impatto delle diverse combinazioni di colori manipolando il LED RGB.


Costruzione del Circuito
----------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Resistenze da 220Ω
     - Fili di Collegamento
   * - |list_uno_r3| 
     - |list_rgb_led| 
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
     
**Istruzioni per la Costruzione Passo-Passo**

Segui il diagramma di cablaggio o questi passaggi per costruire il circuito.

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

1. Inizia con un LED RGB.

I LED RGB emettono luce in vari colori integrando LED rossi, verdi e blu all'interno di un singolo pacchetto. Variando l'ingresso di tensione sui tre pin, questi LED possono combinarsi per produrre fino a 16.777.216 colori diversi.

.. image:: img/12_mix_color_rgb.png
    :width: 400
    :align: center

A seconda del loro design, i LED RGB possono essere ad anodo comune o catodo comune. Per questo progetto, utilizziamo un LED RGB a **catodo comune**, dove tutti e tre i LED condividono una connessione negativa.

* I LED RGB a catodo comune hanno una connessione negativa condivisa.
* I LED RGB ad anodo comune hanno una connessione positiva condivisa.

.. image:: img/12_rgb_cc_ca.jpg
    :width: 600
    :align: center

Un LED RGB ha tipicamente 4 pin; il più lungo è il negativo. Quando posizioni il LED RGB, assicurati che il pin più lungo sia il secondo da sinistra, configurando i pin come Rosso, GND, Verde e Blu da sinistra a destra.

.. image:: img/12_mix_color_rgb_1.jpg
    :width: 200
    :align: center

Puoi anche utilizzare un multimetro in modalità test diodi per identificare quale colore emette ogni pin.

Imposta il multimetro sulla modalità **Continuità** per la misurazione della resistenza.

.. image:: img/multimeter_diode_measure.png
    :width: 300
    :align: center

Tocca il puntale nero del multimetro al pin più lungo del LED RGB e il puntale rosso agli altri pin singolarmente. Vedrai il LED RGB accendersi in rosso, verde o blu di conseguenza.

.. image:: img/12_mix_color_measure_pin.png
    :width: 500
    :align: center

2. Inserisci il LED RGB nel breadboard con il pin più lungo che va nel foro 17D e gli altri tre pin rispettivamente nei fori 18C, 16C e 15C.

.. image:: img/12_mix_color_bb_1.png
    :width: 500
    :align: center

3. Inserisci tre resistenze da 220 ohm come mostrato dai fori 15E a 15G, 16E a 16G e 18E a 18G.

.. image:: img/12_mix_color_bb_2.png
    :width: 500
    :align: center

4. Collega queste resistenze ai pin 9, 10 e 11 dell'Arduino Uno R3 con fili di collegamento come illustrato.

.. image:: img/12_mix_color_bb_3.png
    :width: 500
    :align: center

5. Collega il pin più lungo del LED RGB al GND utilizzando un filo di collegamento.

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

Creazione del Codice - Accendere un LED RGB
--------------------------------------------------

1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando "New Sketch" dal menu "File".
2. Salva il tuo sketch come ``Lesson12_Rainbow_Color`` usando ``Ctrl + S`` o facendo clic su "Salva".

3. Il LED nel tuo circuito è collegato ai pin digitali dell'Arduino Uno R3. Poiché il LED è un dispositivo di output, dovrai impostare i pin digitali 9, 10 e 11 come ``OUTPUT``.

.. code-block:: Arduino
    :emphasize-lines: 3-5


    void setup() {
        // Inserisci qui il codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // Inserisci qui il codice principale da eseguire ripetutamente:
    }

4. Ora, nella funzione ``void loop()``, imposta il pin rosso del LED RGB su ``HIGH`` e gli altri due pin su ``LOW``.
.. note::

    Poiché stiamo utilizzando i pin PWM 9, 10 e 11, hai la possibilità di utilizzare sia ``digitalWrite()`` che ``analogWrite()`` per impostare un livello alto o basso.

    In questa lezione, poiché ci limiteremo a impostare i pin su alto o basso, utilizzeremo ``digitalWrite()``.


.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
    }

5. Salva il codice e clicca su “Carica” per inviarlo al tuo Arduino Uno R3. Vediamo cosa succede.

6. Vedrai il LED RGB accendersi di rosso. Ma se volessi accendere anche il verde e il blu? Come dovresti modificare il codice?

Ora copia i tre comandi ``digitalWrite()`` altre due volte. Imposta il pin che vuoi accendere su ``HIGH`` e gli altri su ``LOW``. Ogni colore deve essere visibile per un secondo.

.. code-block:: Arduino
    :emphasize-lines: 14-21

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
        delay(1000);              // Attendi 1 secondo
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, LOW);   // Spegni il pin Rosso del LED RGB
        delay(1000);              // Attendi 1 secondo
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, LOW);   // Spegni il pin Rosso del LED RGB
        delay(1000);              // Attendi 1 secondo
    }

7. Carica di nuovo il codice per vedere gli effetti. Vedrai il LED RGB alternare il rosso, il verde e il blu.

**Domande**:

1. Se volessi altri colori, cosa dovresti fare? Consulta il diagramma qui sotto e riporta le tue idee nel tuo manuale.

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

.. list-table::
   :widths: 20 20 20 20
   :header-rows: 1

   * - Colore
     - Pin Rosso
     - Pin Verde
     - Pin Blu
   * - Rosso
     - *HIGH*
     - *LOW*
     - *LOW*
   * - Verde
     - *LOW*
     - *HIGH*
     - *LOW*
   * - Blu
     - *LOW*
     - *LOW*
     - *HIGH*
   * - Giallo
     - 
     - 
     - 
   * - Rosa
     - 
     - 
     - 
   * - Ciano
     - 
     - 
     - 
   * - Bianco
     - 
     - 
     - 

Creazione del Codice - Creare Funzioni
-------------------------------------------

Potresti aver notato che, per mostrare colori diversi in sequenza sul LED RGB, finisci per scrivere molte righe di codice simili. Ad esempio, per mostrare sette colori diversi sul LED RGB, potresti scrivere qualcosa del genere:

.. code-block:: Arduino

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, LOW);   // Spegni il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, LOW);   // Spegni il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, LOW);   // Spegni il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
    }

Potresti aver notato che il tuo ``void loop()`` è diventato piuttosto lungo e la logica difficile da seguire. Questo è il momento perfetto per introdurre il concetto di funzioni.

Durante il tuo percorso di programmazione, hai già utilizzato funzioni predefinite di Arduino come ``pinMode()``, ``digitalWrite()`` e ``delay()``. Ora, introdurremo la creazione di funzioni personalizzate. Le funzioni personalizzate ti permettono di semplificare il codice, rendendolo più logico e gestibile.

Per creare una funzione, aggiungila semplicemente in fondo al tuo sketch dopo la chiusura di ``void loop()``. Come ``void setup()`` e ``void loop()``, le funzioni iniziano con void seguito da un nome scelto da te. Le regole di denominazione per le funzioni sono simili a quelle per le variabili o le costanti. Puoi dare alla funzione un nome qualsiasi che non sia una parola chiave dell'IDE di Arduino, e racchiudi i comandi all'interno di parentesi graffe.

.. code-block:: Arduino
    :emphasize-lines: 9-11

    void setup() {
        ...
    }

    void loop() {
        ...
    }

    void lightRed(){
    
    }

1. Alla fine del tuo sketch, subito dopo la chiusura della funzione ``void loop()``, aggiungeremo sette nuove funzioni. Ogni funzione conterrà il codice per visualizzare un colore specifico sul LED RGB.

.. code-block:: Arduino
    :emphasize-lines: 10-22

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
        delay(1000);             // Attendi 1 secondo
        ...
    }

    void lightRed(){
    
    }

    void lightGreen(){
    
    }

    ...

    void lightWhite(){
    
    }

2. Successivamente, taglia i frammenti di codice specifici per i colori dal ``void loop()`` e incollali nelle rispettive funzioni. Questo lascerà solo sette chiamate ``delay()`` nella funzione ``loop()``.

.. code-block:: Arduino

    ...

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:

        delay(1000);  // Attendi 1 secondo
        delay(1000);  // Attendi 1 secondo
        delay(1000);  // Attendi 1 secondo
        delay(1000);  // Attendi 1 secondo
        delay(1000);  // Attendi 1 secondo
        delay(1000);  // Attendi 1 secondo
        delay(1000);  // Attendi 1 secondo
    }

    void lightRed() {
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
    }
    ...

    void lightWhite() {
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
    }

3. Ora che le funzioni sono impostate, è il momento di chiamarle all'interno di ``void loop()``. Per chiamare una funzione, scrivi semplicemente il suo nome seguito da due parentesi e termina la riga con un punto e virgola.

.. code-block:: Arduino
    :emphasize-lines: 7-22

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        lightRed();
        delay(1000);  // Attendi 1 secondo
        lightGreen();
        delay(1000);  // Attendi 1 secondo
        lightBlue();
        delay(1000);  // Attendi 1 secondo
        lightYellow();
        delay(1000);  // Attendi 1 secondo
        lightPink();
        delay(1000);  // Attendi 1 secondo
        lightCyan();
        delay(1000);  // Attendi 1 secondo
        lightWhite();
        delay(1000);  // Attendi 1 secondo
    }

    void lightRed() {
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
    }

    void lightGreen() {
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, LOW);   // Spegni il pin Rosso del LED RGB
    }
    void lightBlue() {
        digitalWrite(9, HIGH);  // Accendi il pin Blu del LED RGB
        digitalWrite(10, LOW);  // Spegni il pin Verde del LED RGB
        digitalWrite(11, LOW);  // Spegni il pin Rosso del LED RGB
    }
    void lightYellow() {
        digitalWrite(9, LOW);    // Spegni il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
    }
    void lightPink() {
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, LOW);   // Spegni il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
    }
    void lightCyan() {
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, LOW);   // Spegni il pin Rosso del LED RGB
    }
    void lightWhite() {
        digitalWrite(9, HIGH);   // Accendi il pin Blu del LED RGB
        digitalWrite(10, HIGH);  // Accendi il pin Verde del LED RGB
        digitalWrite(11, HIGH);  // Accendi il pin Rosso del LED RGB
    }


4. Con tutte le funzioni impostate e chiamate nel loop(), il tuo codice è ora completo. Clicca sul pulsante "Carica" per trasferire il codice sull'Arduino Uno R3. Vedrai il LED RGB alternare rosso, verde, blu, giallo, rosa, ciano e bianco.

.. note::

    La luminosità del LED RGB può essere piuttosto intensa, quindi evita di fissarlo direttamente per lunghi periodi per prevenire l'affaticamento degli occhi.

    Potresti anche considerare di diffondere la luce con un fazzoletto o un materiale opaco per attenuare la luminosità.

**Riepilogo**

Attraverso una serie di esercizi di programmazione, scriverai sketch che cambiano dinamicamente il colore del LED. Iniziando con comandi di base per controllare ogni colore, successivamente ristrutturerai il codice utilizzando funzioni, rendendo il tuo setup più modulare e facile da gestire. Questo approccio non solo rende il codice più pulito, ma ti insegna anche l'importanza delle funzioni nella programmazione.

