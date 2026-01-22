.. note::

    Ciao, benvenuto nella community SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperti**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotti e anteprime esclusive.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri nuovi prodotti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni festive e giveaway.

    👉 Sei pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

23. Dado Cibernetico
=======================

In questa lezione, intraprenderemo un entusiasmante viaggio attraverso due progetti che coinvolgono l'elettronica digitale e la programmazione.

.. image:: img/23_dice.jpg
    :align: center
    :width: 500

Inizialmente, esploreremo il funzionamento di un display a 7 segmenti, imparando a controllarlo per mostrare i numeri passo dopo passo. Successivamente, creeremo un dado elettronico! Premendo semplicemente un pulsante, apparirà un numero casuale compreso tra 1 e 6 sul display a 7 segmenti, offrendo una svolta digitale ai dadi tradizionali.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/23_cycle_dice.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Durante questa lezione imparerai:

* I principi del funzionamento di un display a 7 segmenti e come farlo funzionare.
* L'uso delle istruzioni switch-case per semplificare la logica del codice.
* Come utilizzare un ciclo while per mantenere lo stato corrente fino a quando non è necessario un cambiamento.
* Come costruire il progetto Dado Cibernetico, integrando elettronica semplice con programmazione interattiva per un'applicazione pratica.

L'origine dei Dadi
-----------------------

I dadi sono tra gli strumenti di gioco d'azzardo più antichi al mondo, con una storia che risale a migliaia di anni prima dell'era comune. Sono stati originati intorno al 3000 a.C. nell'antico Egitto, tipicamente realizzati con ossa, avorio o altri materiali naturali. Questi primi dadi erano spesso irregolari nella forma e talvolta non del tutto simmetrici.

.. image:: img/23_dice.png
    :width: 500
    :align: center

I dadi sono stati trovati anche nell'antica Mesopotamia (l'attuale Iraq) all'incirca nello stesso periodo. Gli antichi indovini e leader religiosi usavano i dadi per prendere decisioni o prevedere il futuro, sottolineando la loro importanza nei riti religiosi e mistici.

Col tempo, la forma e le tecniche di produzione dei dadi si sono standardizzate. Entro il I secolo a.C., i dadi erano ampiamente utilizzati nell'Impero Romano, non solo per il gioco d'azzardo, ma anche per scopi sociali e di intrattenimento.

In Asia, in particolare in India, l'uso dei dadi è documentato nell'antico poema epico, il Mahabharata, in cui una partita di dadi gioca un ruolo cruciale nella trama.

Durante il Rinascimento, la produzione di dadi divenne più raffinata e i materiali si diversificarono includendo legno, osso, avorio e persino metallo. Oggi, i dadi non sono solo strumenti per l'intrattenimento e il gioco d'azzardo, ma vengono utilizzati anche nell'educazione, nel supporto alle decisioni e in vari giochi da tavolo. La loro storia e diversità riflettono l'evoluzione della cultura e della tecnologia umana, offrendo una finestra affascinante sull'esplorazione del caso e della fortuna.



Comprensione del Display a 7 Segmenti
--------------------------------------------

1. Trova un display a 7 segmenti.

Un display a 7 segmenti è un componente a forma di 8 che racchiude 7 LED. Ognuno dei LED nel display è collegato a un segmento posizionale con uno dei suoi pin di connessione che esce dal pacchetto di plastica rettangolare. Questi pin LED sono etichettati da "a" a "g", rappresentando ogni singolo LED.
Un ulteriore ottavo LED è utilizzato all'interno dello stesso pacchetto, consentendo così l'indicazione di un punto decimale (DP) quando due o più display a 7 segmenti sono collegati insieme per mostrare numeri maggiori di dieci.

.. image:: img/23_7_segment.png
    :width: 300
    :align: center

Il pin comune del display solitamente ne indica il tipo. Esistono due tipi di connessioni: una con i catodi collegati e un'altra con gli anodi collegati, indicando Catodo Comune (CC) e Anodo Comune (CA). Come suggerisce il nome, un display CC ha tutti i catodi dei 7 LED collegati, mentre un display CA ha tutti gli anodi dei 7 segmenti collegati.

.. note::

    Solitamente, c'è un'etichetta sul lato del display a 7 segmenti, xxxAx o xxxBx. In generale, xxxAx sta per catodo comune e xxxBx per anodo comune. I display nel nostro kit sono a catodo comune.

.. image:: img/23_segment_cathode_1.png
    :align: center
    :width: 600

Per determinare se un display a 7 segmenti è a catodo comune o anodo comune, puoi utilizzare un multimetro. Puoi anche utilizzare un multimetro per testare se ogni segmento del display funziona correttamente, come segue:

1. Imposta il multimetro in modalità test diodi. Il test diodi è una funzione del multimetro utilizzata per controllare la conduzione diretta dei diodi o di dispositivi semiconduttori simili (come i LED). Il multimetro fa passare una piccola corrente attraverso il diodo. Se il diodo è intatto, permetterà il passaggio della corrente.

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. Inserisci il display a 7 segmenti in una breadboard, notando che il punto decimale è in basso a destra e assicurati che attraversi la fessura centrale. Inserisci un filo nella stessa fila del pin 1 del display e toccalo con il cavo rosso del multimetro. Inserisci un altro filo nella stessa fila di qualsiasi pin "-" del display e toccalo con il cavo nero.

.. image:: img/23_7_segment_test.png
    :align: center
    :width: 500

3. Osserva se si accende un segmento LED. In tal caso, indica che il display è a catodo comune. In caso contrario, scambia i cavi rosso e nero; se un segmento si accende dopo lo scambio, significa che il display è ad anodo comune.

4. Se un segmento si accende, fai riferimento a questo diagramma per annotare il numero del pin del segmento e la posizione approssimativa nella tabella del Manuale.

.. image:: img/23_segment_2.png
    :align: center

.. list-table::
    :widths: 20 20 40
    :header-rows: 1

    *   - Pin
        - Numero del Segmento
        - Posizione
    *   - 1
        - a
        - Il segmento superiore
    *   - 2
        -
        - 
    *   - 3
        -
        - 
    *   - 4
        -
        - 
    *   - 5
        -
        - 
    *   - 6
        -
        - 
    *   - 7
        -
        - 
    *   - 8
        -
        -     

5. Ripeti i passaggi precedenti, mantenendo il cavo nero sul pin "-", e collega il cavo rosso agli altri pin per scoprire i pin di controllo corrispondenti ai segmenti LED del display.

**Domanda**

Dai test precedenti, si sa che il display nel kit è a catodo comune, il che significa che è sufficiente collegare il pin comune a GND e fornire una tensione alta agli altri pin per accendere i segmenti corrispondenti. Se vuoi che il display mostri il numero 2, quali pin dovrebbero ricevere una tensione alta? Perché?

.. image:: img/23_segment_2.png
    :align: center



Costruzione del Circuito
--------------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Display a 7 segmenti
     - 1 * Resistenza da 220Ω
     - 1 * Resistenza da 10KΩ
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Pulsante
     - 1 * Breadboard
     - Fili di collegamento
     - 1 * Cavo USB
   * - |list_button| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
   * - 1 * Multimetro
     - 
     - 
     - 
   * - |list_meter| 
     - 
     - 
     - 



**Passaggi per la Costruzione**

Segui il diagramma di collegamento o i passaggi seguenti per costruire il tuo circuito.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

1. Inserisci il display a 7 segmenti nella breadboard con il punto decimale nell'angolo in basso a destra.

.. image:: img/23_segment_segment.png
    :align: center
    :width: 500

2. Inserisci un'estremità di una resistenza da 220Ω nel terminale negativo (“-”) del display a 7 segmenti, e l'altra estremità nel binario negativo della breadboard. Quindi collega il binario negativo della breadboard al pin GND dell'Arduino Uno R3 con un filo di collegamento.

.. image:: img/23_segment_resistor_gnd.png
    :align: center
    :width: 500

3. Collega i pin che controllano i segmenti a, b, c del LED ai pin 2, 3 e 4 dell'Arduino Uno R3.

.. image:: img/23_segment_abc.png
    :align: center
    :width: 500

4. Collega i pin che controllano i segmenti d, e, f, g del LED ai pin 5, 6, 7 e 8 dell'Arduino Uno R3.

.. image:: img/23_segment_defg.png
    :align: center
    :width: 500

5. Ora inserisci un pulsante nella breadboard.

.. image:: img/23_segment_button.png
    :align: center
    :width: 500

6. Collega il pin in basso a destra del pulsante al pin 9 di R3 con un filo.

.. image:: img/23_segment_pin9.png
    :align: center
    :width: 500

7. Collega una resistenza pull-down da 10K al pulsante in modo che quando il pulsante non viene premuto, il pin 9 rimanga a un livello basso e non vi sia rimbalzo.

.. image:: img/23_segment_10k_resistor.png
    :align: center
    :width: 500

8. Collega il pin in basso a sinistra del pulsante al pin 5V sull'Arduino Uno R3.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 7-segment Display
        - Arduino UNO R3
    *   - a
        - 2
    *   - b
        - 3 
    *   - c
        - 4
    *   - d
        - 5
    *   - e
        - 6
    *   - f
        - 7
    *   - g
        - 8


Creazione del Codice - Visualizzazione dei Numeri
--------------------------------------------------------
1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando “New Sketch” dal menu “File”.
2. Salva il tuo sketch con il nome ``Lesson23_Show_Number`` utilizzando ``Ctrl + S`` o cliccando su “Save”.

3. Definisci i pin collegati al display a 7 segmenti e imposta tutti i pin come output.

.. code-block:: Arduino

    // Definizione dei pin collegati al display a 7 segmenti
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Imposta tutti i pin come output
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

4. Ora scrivi il codice per far visualizzare al display a 7 segmenti un numero, come il numero 2. Per visualizzare il numero 2, imposta i segmenti F e C su LOW (spenti), mentre gli altri segmenti su HIGH (accesi).

.. code-block:: Arduino
  :emphasize-lines: 22-29

    // Definizione dei pin collegati al display a 7 segmenti
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Imposta tutti i pin come output
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {
        // Imposta i segmenti F e C su LOW (spenti), gli altri su HIGH (accesi)
        digitalWrite(pinA, HIGH);
        digitalWrite(pinB, HIGH);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, HIGH);
        digitalWrite(pinE, HIGH);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, HIGH);
    }

5. Ora puoi caricare il codice sull'Arduino Uno R3 e vedrai il numero 2 visualizzato sul display a 7 segmenti.

6. Se hai bisogno di visualizzare altri numeri, ad esempio scorrendo da 1 a 6, utilizzare ``digitalWrite()`` per impostare ogni segmento renderebbe il codice molto lungo e la logica meno chiara. Qui utilizziamo invece un metodo di creazione di funzione.

7. Crea una funzione con un parametro - ``displayDigit()``, che prima spegne tutti i segmenti LED del display a 7 segmenti.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Spegne tutti i segmenti
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);
    }

8. Successivamente, controlla i vari segmenti LED per visualizzare i numeri. Qui potremmo usare istruzioni ``if-else``, ma ciò potrebbe risultare ingombrante. Pertanto, una dichiarazione ``switch`` fornisce un modo più chiaro e organizzato per scegliere tra più comportamenti diversi rispetto a molteplici istruzioni ``if-else``.

Nel linguaggio di programmazione, un'istruzione ``switch`` è una struttura di controllo utilizzata per eseguire diversi blocchi di codice in base al valore di una variabile.

La sintassi di base di una dichiarazione switch è la seguente:

.. code-block:: Arduino

    switch (espressione) {
        case valore1:
            // codice
            break;
        case valore2:
            // codice
            break;
        default:
            // codice
    }

* ``espressione``: Questa è un'espressione che in genere restituisce un intero o un carattere, in base al quale l'istruzione switch decide quale ``case`` eseguire.
* ``case``: Ogni parola chiave ``case`` è seguita da un valore che può corrispondere al risultato dell'espressione. Se la corrispondenza è corretta, il codice viene eseguito da questo punto fino al raggiungimento di un'istruzione ``break``.
* ``break``: L'istruzione ``break`` viene utilizzata per uscire dal blocco ``switch``. Senza ``break``, il programma continuerebbe a eseguire il codice del case successivo, indipendentemente dalla corrispondenza, questo è noto come "fall-through".
* ``default``: La parte ``default`` è opzionale e viene eseguita se nessun case corrisponde, simile a ``else`` in una struttura ``if-else``.

.. image:: img/23_flow_swtich.png
    :align: center
    :width: 600

9. Usa lo ``switch-case`` nella funzione ``displayDigit()`` per completare la visualizzazione dei numeri sul display a 7 segmenti. Ad esempio, per visualizzare 1, solo i segmenti B e C devono essere impostati su HIGH; per visualizzare 2, i segmenti F e C devono essere impostati su LOW, mentre gli altri su HIGH.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Spegne tutti i segmenti
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Imposta su HIGH i segmenti necessari per visualizzare il numero desiderato
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }

10. Ora puoi chiamare ``displayDigit()`` all'interno di ``void loop()`` per visualizzare numeri specifici, come alternare tra il 3 e il 6 con un intervallo di un secondo.

.. code-block:: Arduino

    void loop() {

        displayDigit(3);  // Visualizza il numero 3 sul display a 7 segmenti
        delay(1000);
        displayDigit(6);  // Visualizza il numero 6 sul display a 7 segmenti
        delay(1000);
    }

11. Di seguito è riportato il tuo codice completo. Ora puoi caricare il codice sull'Arduino Uno R3 e vedrai il display a 7 segmenti alternare la visualizzazione tra il numero 3 e il numero 6.

.. code-block:: Arduino

    // Definizione dei pin collegati al display a 7 segmenti
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Imposta tutti i pin come output
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {

        displayDigit(3);  // Visualizza il numero 3 sul display a 7 segmenti
        delay(1000);
        displayDigit(6);  // Visualizza il numero 6 sul display a 7 segmenti
        delay(1000);
    }

    void displayDigit(int digit) {
        // Spegne tutti i segmenti
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Accende i segmenti necessari per visualizzare il numero desiderato (HIGH accende i segmenti per catodo comune)
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }



Creazione del Codice - Cyber Dice
-------------------------------------
Ora che sappiamo come visualizzare i numeri da 1 a 6 sul display a 7 segmenti, come possiamo ottenere l'effetto di un Cyber Dice?

Questo coinvolge la pressione di un pulsante per far ciclicare il display attraverso i numeri da 1 a 6 e il rilascio del pulsante per mostrare un numero stabile. Vediamo come possiamo ottenere questo effetto con il codice.

1. Apri lo sketch salvato in precedenza, ``Lesson23_Show_Number``. 

2. Clicca su “Salva come...” dal menu “File” e rinominalo in ``Lesson23_Cyber_Dice``. Clicca su "Salva".

3. Definisci il pin del pulsante e impostalo come input.

.. code-block:: Arduino
    :emphasize-lines: 10-11,23-24

    // Definisci i pin collegati ai segmenti del display a 7 segmenti
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Definisci il pin collegato al pulsante
    int buttonPin = 9;

    void setup() {
        // Imposta tutti i pin come output
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Imposta il pin del pulsante come input
        pinMode(buttonPin, INPUT);
    }

4. Verifica se il pulsante è premuto nel momento in cui viene eseguita la funzione ``void loop()``. Se il pulsante non è premuto, il codice all'interno del blocco ``if`` viene saltato.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // Verifica se il pulsante è premuto
        if (digitalRead(buttonPin) == HIGH) {
        }
    }

5. In Arduino o in programmazione su microcontrollori simili, un problema comune quando si lavora con input da pulsante è assicurarsi che ogni pressione generi una sola azione, soprattutto quando si generano eventi o comandi (come generare un numero casuale). Per risolvere questo, possiamo usare una tecnica chiamata "attendere il rilascio".

**attendere il rilascio**

L'idea principale di questo metodo è che, dopo che il pulsante è stato premuto e un'azione è stata eseguita, il programma entra in un ciclo che continua a monitorare lo stato del pulsante fino al suo rilascio. Questo serve per garantire che non vengano attivate ulteriori azioni a causa di rimbalzi del pulsante o perché l'utente lo tiene premuto.

Possiamo implementare questo comportamento con un ciclo ``while`` nel codice.

.. image:: img/while_loop.png
    :width: 400
    :align: center

.. code-block:: Arduino
    :emphasize-lines: 4-6

    void loop() {
        // Verifica se il pulsante è premuto
        if (digitalRead(buttonPin) == HIGH) {
            // Attendi che il pulsante venga rilasciato prima di continuare
            while (digitalRead(buttonPin) == HIGH) {
            }
        }
    }

6. Ora, usa la funzione ``random()`` per generare un numero casuale tra 1 e 6, e usa ``displayDigit()`` per visualizzare questo numero sul display a 7 segmenti. Vedrai il display scorrere rapidamente tra numeri diversi mentre il pulsante è tenuto premuto.

.. code-block:: Arduino
    :emphasize-lines: 6-12

    void loop() {
        // Verifica se il pulsante è premuto
        if (digitalRead(buttonPin) == HIGH) {
            // Attendi che il pulsante venga rilasciato prima di continuare
            while (digitalRead(buttonPin) == HIGH) {
                // Genera un numero casuale tra 1 e 6
                int num = random(1, 7);
                
                // Visualizza il numero casuale sul display a 7 segmenti
                displayDigit(num);
                // Ritardo per permettere aggiornamenti visibili del display
                delay(100);
            }
        }
    }

7. Infine, aggiungi un ritardo per evitare il rimbalzo del pulsante e prevenire ingressi multipli rapidi.

.. code-block:: Arduino
    :emphasize-lines: 15

    void loop() {
        // Verifica se il pulsante è premuto
        if (digitalRead(buttonPin) == HIGH) {
            // Attendi che il pulsante venga rilasciato prima di continuare
            while (digitalRead(buttonPin) == HIGH) {
                // Genera un numero casuale tra 1 e 6
                int num = random(1, 7);
                
                // Visualizza il numero casuale sul display a 7 segmenti
                displayDigit(num);
                // Ritardo per consentire aggiornamenti visibili del display
                delay(100);
            }
            // Aggiungi un ritardo per evitare il rimbalzo del pulsante e prevenire ingressi multipli rapidi
            delay(500);
        }
    }


8. Il codice completo dovrebbe essere simile a questo, e ora puoi caricare il codice sull'Arduino Uno R3. Una volta caricato, se tieni premuto il pulsante, i numeri sul display scorreranno rapidamente, e al rilascio verrà mostrato un numero.

.. code-block:: Arduino

    // Definisci i pin collegati ai segmenti del display a 7 segmenti
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Definisci il pin collegato al pulsante
    int buttonPin = 9;

    void setup() {
        // Imposta tutti i pin come output
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Imposta il pin del pulsante come input
        pinMode(buttonPin, INPUT);
    }

    void loop() {
        // Verifica se il pulsante è premuto
        if (digitalRead(buttonPin) == HIGH) {
            // Attendi che il pulsante venga rilasciato prima di continuare
            while (digitalRead(buttonPin) == HIGH) {
                // Genera un numero casuale tra 1 e 6
                int num = random(1, 7);

                // Visualizza il numero casuale sul display a 7 segmenti
                displayDigit(num);
                // Ritardo per consentire aggiornamenti visibili del display
                delay(100);
            }
            // Aggiungi un ritardo per evitare il rimbalzo del pulsante e prevenire ingressi multipli rapidi
            delay(500);
        }
    }


    void displayDigit(int digit) {
        // Spegni tutti i segmenti
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Accendi i segmenti necessari per il numero desiderato (LOW accende i segmenti per catodo comune)
        switch (digit) {
            case 1:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            break;
            case 2:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 3:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 4:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 5:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 6:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
        }
    }

9. Infine, ricorda di salvare il codice e di riordinare la tua area di lavoro.

**Riepilogo**

In questa lezione, abbiamo completato con successo il progetto del Cyber Dice, permettendoti di partecipare a competizioni amichevoli con i tuoi amici per vedere chi riesce a ottenere il numero più alto. Durante questa lezione, abbiamo esplorato il funzionamento di un display a 7 segmenti, imparando a controllarlo efficacemente. Abbiamo semplificato il nostro codice utilizzando dichiarazioni switch-case, migliorando la leggibilità e l'efficienza.

Inoltre, abbiamo implementato la logica per controllare la visualizzazione di numeri casuali sul display a 7 segmenti in base allo stato di pressione di un pulsante, aggiungendo un'interazione dinamica al nostro progetto. Questa esperienza pratica non solo ti ha familiarizzato con i componenti elettronici di base e le strategie di codifica, ma ha anche illustrato le applicazioni pratiche di queste competenze nella creazione di progetti coinvolgenti e interattivi.

