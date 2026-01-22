.. note::

    Ciao, benvenuto nella Community di SunFounder per appassionati di Raspberry Pi, Arduino e ESP32 su Facebook! Esplora più a fondo Raspberry Pi, Arduino ed ESP32 con altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e concorsi**: Partecipa a giveaway e promozioni durante le festività.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

25. Mostrare numeri con 74HC595
==================================

Nella lezione precedente, potresti aver notato che il 74HC595 e il display a 7 segmenti formano una coppia perfetta. Il 74HC595 può emettere simultaneamente segnali a 8 bit, mentre il display a 7 segmenti è controllato da 8 segnali elettrici (incluso il segmento LED del punto decimale, ossia il segmento dp).

Quindi, è possibile utilizzare il 74HC595 per controllare il display a 7 segmenti? La risposta è sì.

In questa lezione, utilizzeremo il 74HC595 per controllare il display a 7 segmenti e farlo mostrare numeri diversi.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/25_show_number.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In questa lezione, sarai in grado di:

* Capire come utilizzare il registro a scorrimento 74HC595 per pilotare un display a 7 segmenti.
* Imparare le rappresentazioni binarie delle cifre da 0 a 9 e come convertirle nei formati decimale e esadecimale.
* Comprendere come utilizzare il Serial Monitor per inserire dati e visualizzarli sul display a 7 segmenti.

Costruzione del circuito
--------------------------------

**Componenti necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Display a 7 segmenti
     - 1 * Resistenza da 220Ω
     - 1 * 74HC595
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_74hc595| 
   * - 1 * Breadboard
     - Cavi jumper
     - 1 * Cavo USB
     - 
   * - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
     - 

**Costruzione passo passo**

Segui lo schema di cablaggio o i passaggi qui sotto per costruire il tuo circuito.

.. image:: img/25_show_number.png
    :width: 500
    :align: center

1. Inserisci il display a 7 segmenti nella breadboard con il punto decimale nell'angolo in basso a destra.

.. image:: img/25_show_number_7segment.png
    :width: 500
    :align: center

2. Collega il terminale negativo (-) del display a 7 segmenti alla barra del GND della breadboard utilizzando un cavo jumper.

.. image:: img/25_show_number_resistor.png
    :width: 500
    :align: center

3. Posiziona il chip 74HC595 nella breadboard. Assicurati che il chip copra la parte centrale della breadboard.

.. image:: img/25_show_number_74hc595.png
    :width: 500
    :align: center

4. Collega i pin VCC e MR del 74HC595 alla barra positiva della breadboard.

.. image:: img/25_show_number_vcc.png
    :width: 500
    :align: center

5. Collega i pin CE e GND del 74HC595 alla barra negativa della breadboard.

.. image:: img/25_show_number_gnd.png
    :width: 500
    :align: center

6. Collega Q0 del 74HC595 al pin 'a' del display a 7 segmenti, Q1 al pin 'b', Q2 al pin 'c', Q3 al pin 'd' e Q4 al pin 'e'.

.. image:: img/25_show_number_q0_q4.png
    :width: 500
    :align: center

7. Collega Q5 del 74HC595 al pin 'f' del display a 7 segmenti, Q6 al pin 'g', e Q7 al pin 'dp'.

.. image:: img/25_show_number_q5_q7.png
    :width: 500
    :align: center

8. Collega il pin DS del 74HC595 al pin 11 dell'Arduino Uno R3.

.. image:: img/25_show_number_pin11.png
    :width: 500
    :align: center

9. Collega il pin ST_CP del 74HC595 al pin 12 dell'Arduino Uno R3.

.. image:: img/25_show_number_pin12.png
    :width: 500
    :align: center

10. Collega il pin SH_CP del 74HC595 al pin 8 dell'Arduino Uno R3.

.. image:: img/25_show_number_pin8.png
    :width: 500
    :align: center

11. Infine, collega i pin GND e 5V dell'Arduino Uno R3 rispettivamente alle barre negative e positive sulla breadboard.

.. image:: img/25_show_number.png
    :width: 500
    :align: center

12. Le seguenti tabelle mostrano le connessioni tra il 74HC595, l'Arduino Uno R3 e il Display a 7 segmenti.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - Arduino UNO R3
    *   - VCC
        - 5V
    *   - DS
        - 11
    *   - CE
        - GND
    *   - ST_CP
        - 12
    *   - SH_CP
        - 8
    *   - MR
        - 5V
    *   - GND
        - GND

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - Display a 7 segmenti
    *   - Q0
        - a
    *   - Q1
        - b 
    *   - Q2
        - c
    *   - Q3
        - d
    *   - Q4
        - e
    *   - Q5
        - f
    *   - Q6
        - g
    *   - Q7
        - dp

Numeri binari per le cifre da 0 a 9
---------------------------------------

In questo progetto, utilizziamo il registro a scorrimento 74HC595 per controllare il display a 7 segmenti e visualizzare numeri diversi. Tuttavia, il 74HC595 riceve numeri binari, quindi prima di programmare dobbiamo conoscere i numeri binari corrispondenti alle cifre da 0 a 9.

Supponiamo di voler visualizzare il numero 2 sul display a 7 segmenti, dobbiamo spegnere i segmenti f e c e accendere i restanti segmenti.

.. image:: img/23_segment_2.png
    :align: center
    :width: 200

Secondo lo schema di cablaggio, i pin di uscita Q0 a Q7 del 74HC595 corrispondono ai rispettivi pin del display a 7 segmenti, come mostrato nello schema. In binario, 0 rappresenta spento (chiuso) e 1 rappresenta acceso (aperto). Per visualizzare il numero 2, dp, f e c devono essere 0, mentre gli altri segmenti devono essere 1, ottenendo così il numero binario ``B01011011``.

.. image:: img/25_display_2_binary.png
    :align: center
    :width: 600

.. note::

    Quando hai solo un display a 7 segmenti, il pin DP è sempre impostato a 0. Quando hai più display a 7 segmenti in configurazione a catena, puoi utilizzare il pin DP per indicare il punto decimale.

Per visualizzare il numero 0, dp e g devono essere 0 e tutti gli altri segmenti devono essere 1, ottenendo così il numero binario ``B00111111``.

**Domanda**

Ora che conosciamo le rappresentazioni binarie per le cifre 0 e 2, compila i numeri binari per le cifre rimanenti nella tabella sottostante.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - Numero
        - Binario
    *   - 0
        - B00111111
    *   - 1
        - 
    *   - 2
        - B01011011
    *   - 3
        - 
    *   - 4
        - 
    *   - 5
        - 
    *   - 6
        - 
    *   - 7
        - 
    *   - 8
        - 
    *   - 9
        - 

Creazione del Codice - Visualizzazione dei Numeri
------------------------------------------------------
1. Apri lo sketch che hai salvato precedentemente, ``Lesson24_Flowing_Light``.

2. Fai clic su “Salva con nome” dal menu “File” e rinominalo come ``Lesson25_Show_Number_Binary``. Fai clic su "Salva".

3. Modifica il ``datArray[]`` per visualizzare i numeri binari corrispondenti alle cifre da 0 a 9.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595
    // visualizzazione 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

4. Poiché l'array ``datArray[]`` contiene 10 elementi, modifica l'intervallo della variabile ``num`` in ``num <= 9``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // Mantenere ST_CP a bassa tensione durante la trasmissione
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Sposta i dati, MSB primo
            digitalWrite(STcp, HIGH);                     // Imposta ST_CP ad alto per salvare i dati
            delay(1000);                                  // Attendi un secondo
        }
    }

5. Il tuo codice completo dovrebbe essere simile al seguente. A questo punto, puoi caricare il codice sull'Arduino Uno R3 e vedrai il display a 7 segmenti scorrere tra le cifre da 0 a 9.

.. code-block:: Arduino

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595
    // visualizzazione 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

    void setup() {
        // imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // Mantenere ST_CP a bassa tensione durante la trasmissione
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Sposta i dati, MSB primo
            digitalWrite(STcp, HIGH);                     // Imposta ST_CP ad alto per salvare i dati
            delay(1000);                                  // Attendi un secondo
        }
    }

Conversione Binaria
------------------------

Nelle applicazioni pratiche, scrivere numeri binari può esprimere chiaramente lo stato di ciascun bit nei dati. Tuttavia, per la rappresentazione numerica generale, scrivere numeri decimali è più conveniente.

.. note::

    Scrivere numeri binari, decimali o anche esadecimali non influisce sul risultato del programma ma solo sulla leggibilità del codice. Ad esempio, scrivere il numero decimale ``91`` sarà internamente convertito nella forma binaria ``B01011011``.

Vediamo come convertire i numeri binari in decimali.

**Conversione in Decimale**

Nel sistema binario, ogni bit rappresenta un valore posizionale corrispondente. Il valore posizionale è una potenza di 2, come 2^0, 2^1, 2^2…, ecc. Moltiplicando ciascun bit per il suo valore posizionale corrispondente e sommando tutti i risultati, otteniamo il numero decimale.

Ad esempio, il numero binario ``B01011011`` si converte nel numero decimale 91.

.. image:: img/25_binary_dec.png
    :align: center
    :width: 600

**Utilizzo di una Calcolatrice**

Nelle applicazioni pratiche, puoi utilizzare la calcolatrice del tuo computer. Passa alla modalità Programmatore e puoi facilmente convertire tra numeri binari, decimali ed esadecimali.

Cerca "Calcolatrice" sul tuo computer, quindi passa alla modalità **Programmatore**.

.. image:: img/25_calculator_programmer.png
    :align: center

2. Se conosci già il numero binario e vuoi convertirlo in un'altra base, seleziona **BIN**.

.. image:: img/25_calculator_binary.png
    :align: center

3. Ora puoi iniziare a inserire il numero binario.

* I bit efficaci in binario si riferiscono all'intervallo dal bit più significativo (bit non zero più a sinistra) al bit meno significativo (bit non zero più a destra).
* Quindi, per il numero binario ``B00111111``, i bit efficaci sono ``111111``.
* Ora, inserisci ``111111`` nella calcolatrice per ottenere i numeri decimali ed esadecimali corrispondenti.

.. image:: img/25_calculator_binary_0.png
    :align: center
    :width: 300

**Domanda**

Converti i numeri binari che rappresentano le cifre da 0 a 9 in numeri decimali ed esadecimali utilizzando una calcolatrice e compila la tabella. Questo ti fornirà una guida rapida per le conversioni di base.

.. list-table::
    :widths: 20 40 30 30
    :header-rows: 1

    *   - Number
        - Binary
        - Decimal
        - Hexadecimal
    *   - 0
        - B00111111
        - 63
        - 0x3F
    *   - 1
        - B00000110
        -
        -
    *   - 2
        - B01011011
        -
        -
    *   - 3
        - B01001111
        -
        -
    *   - 4
        - B01100110
        -
        -
    *   - 5
        - B01101101
        -
        -
    *   - 6
        - B01111101
        -
        -
    *   - 7
        - B00000111
        -
        -
    *   - 8
        - B01111111
        -
        -
    *   - 9
        - B01101111
        -
        -

**Modifica dello Sketch**

Ora, apri il tuo sketch ``Lesson25_Show_Number_Binary`` nell'IDE Arduino. Clicca su "File" -> "Salva con nome...", rinomina il file ``Lesson25_Show_Number_Decimal``. Clicca "Salva".

Modifica tutti gli elementi di ``datArray[]`` in decimale, come mostrato nel codice. Una volta modificato, puoi caricare il codice sull'Arduino Uno R3 per vedere l'effetto.

.. code-block:: Arduino

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595
    // visualizzazione 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        // imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // Mantieni ST_CP a bassa tensione durante la trasmissione
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Sposta i dati, MSB primo
            digitalWrite(STcp, HIGH);                     // Imposta ST_CP a livello alto per salvare i dati
            delay(1000);                                  // Attendi un secondo
        }
    }

Creazione del Codice - Input Seriali
-----------------------------------------

Il Serial Monitor è uno strumento potente fornito dall'IDE Arduino per comunicare con la scheda Arduino. Lo abbiamo utilizzato per monitorare l'output dei dati dall'Arduino, come la lettura dei valori analogici da un fotoresistore. Può anche essere utilizzato per inviare dati all'Arduino, permettendogli di eseguire azioni basate sui dati ricevuti.

In questa attività, scriveremo un numero compreso tra 0 e 9 nel Serial Monitor per visualizzarlo sul display a 7 segmenti.

1. Apri il tuo sketch ``Lesson25_Show_Number_Decimal`` nell'IDE Arduino. Clicca su "File" -> "Salva con nome...", rinomina il file ``Lesson25_Show_Number_Serial``. Clicca "Salva".

2. In ``void setup()``, avvia il monitor seriale e imposta il baud rate su 9600.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // Imposta la comunicazione seriale a 9600 baud
    }

3. Quando si utilizza il Serial Monitor, è possibile leggere i dati inseriti attraverso il codice Arduino. Qui, devi comprendere due funzioni:

* ``Serial.available()``: Ottieni il numero di byte (caratteri) disponibili per la lettura dalla porta seriale. Questi sono dati già arrivati e memorizzati nel buffer di ricezione seriale (che contiene 64 byte).
* ``Serial.read()``: Restituisce il codice ASCII del carattere ricevuto tramite l'input seriale.

Ora, utilizza una dichiarazione ``if`` in ``loop()`` per verificare se i dati sono stati letti dalla porta e stampali.

.. note::

    Temporaneamente, commenta il ciclo for in ``void loop()`` che visualizza i caratteri sul display a 7 segmenti per evitare di influenzare il processo di stampa.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    void loop() {
        if (Serial.available() > 0) {
            // Stampa il carattere ricevuto dalla porta seriale
            Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // Mantieni ST_CP a bassa tensione durante la trasmissione
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Sposta i dati, MSB primo
        //   digitalWrite(STcp, HIGH);                     // Imposta ST_CP a livello alto per salvare i dati
        //   delay(1000);                                  // Attendi un secondo
        // }
    }

4. Ecco il tuo codice completo. A questo punto, puoi caricare il codice sull'Arduino Uno R3.

.. code-block:: Arduino

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595
    // visualizza 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        // imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // Imposta la comunicazione seriale a 9600 baud
    }

    void loop() {
        if (Serial.available() > 0) {
            // Stampa il carattere ricevuto dalla porta seriale
            Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // Mantieni ST_CP a bassa tensione durante la trasmissione
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Sposta i dati, MSB primo
        //   digitalWrite(STcp, HIGH);                     // Imposta ST_CP a livello alto per salvare i dati
        //   delay(1000);                                  // Attendi un secondo
        // }
    }

5. Dopo aver caricato il codice, apri il Serial Monitor. Nella casella di input, inserisci il numero ``0`` (o qualsiasi cifra compresa tra 0 e 9) e premi invio. A questo punto, vedrai che il Serial restituisce il numero ``48``.

.. note::

    * Se l'opzione "Newline" è selezionata nel campo di terminazione linea del monitor seriale, vedrai anche un ``10``. 
    * ``10`` è il codice ASCII per il carattere di nuova linea (chiamato anche LF - Line Feed).


.. image:: img/25_serial_read.png
    :align: center
    :width: 600

Dunque, dove è andato il nostro input ``0``? Da dove arriva questo ``48``? È possibile che ``0`` sia uguale a ``48``?

Questo succede perché il ``0`` che abbiamo inserito nel Serial Monitor è considerato un "carattere," non un "numero."

Il trasferimento del carattere segue uno standard di codifica noto come ASCII (American Standard Code for Information Interchange).

L'ASCII include caratteri comuni come lettere maiuscole (A-Z), lettere minuscole (a-z), cifre (0-9) e segni di punteggiatura (come punti, virgole, punti esclamativi, ecc.). Definisce anche alcuni caratteri di controllo utilizzati per controllare dispositivi e protocolli di comunicazione. Questi caratteri di controllo solitamente non vengono visualizzati sullo schermo ma vengono utilizzati per controllare il comportamento di dispositivi come stampanti, terminali, ecc., come il ritorno a capo, il backspace, il carriage return, ecc.

Ecco una tabella ASCII:

.. image:: img/25_ascii_table.png
    :align: center
    :width: 800

Quando digiti il carattere ``0`` nel Serial Monitor, il codice ASCII per il carattere ``0`` viene inviato all'Arduino.
In ASCII, il codice per il carattere ``0`` è ``48`` in decimale.

6. Prima di continuare con la codifica, devi commentare il codice precedente che stampa il codice ASCII per evitare conflitti con il codice successivo.

.. code-block:: Arduino
    :emphasize-lines: 4

    void loop() {
        if (Serial.available() > 0) {
            // Stampa il carattere ricevuto dalla porta seriale
            // Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // Mantieni ST_CP a bassa tensione durante la trasmissione
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Sposta i dati, MSB primo
        //   digitalWrite(STcp, HIGH);                     // Imposta ST_CP a livello alto per salvare i dati
        //   delay(1000);                                  // Attendi un secondo
        // }
    }

7. È necessario creare una nuova variabile di tipo ``char`` per memorizzare il carattere letto dal Serial Monitor.

.. code-block:: Arduino
    :emphasize-lines: 6,7

    void loop() {
        if (Serial.available() > 0) {
            // Stampa il carattere ricevuto dalla porta seriale
            // Serial.println(Serial.read());

            // Leggi il carattere ricevuto dalla porta seriale
            char receivedChar = Serial.read();
        }
    }

8. Ora, converti il carattere in un numero. In ASCII, il valore del carattere ``'0'`` è ``48``, ``'1'`` è ``49``, e così via. Pertanto, sottraendo il codice ASCII di ``'0'``, possiamo ottenere il valore numerico corrispondente.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        if (Serial.available() > 0) {
            // Stampa il carattere ricevuto dalla porta seriale
            Serial.println(Serial.read());

            // Leggi il carattere ricevuto dalla porta seriale
            char receivedChar = Serial.read();
            // Converti il carattere in un numero
            int digit = receivedChar - '0';
        }
    }

9. In questo esempio, si presume che l'input sia composto da caratteri numerici ``'0'`` a ``'9'``. Quindi, è necessario verificare se il carattere di input rientra in questo intervallo. Per farlo, occorre controllare se il numero è all'interno dell'intervallo valido:

* Seleziona il ciclo ``for`` precedentemente commentato e premi ``Ctrl + /`` per decommentarlo.
* Poi modifica l'istruzione ``for`` in un'istruzione ``if`` per verificare se il carattere di input rientra nell'intervallo da ``'0'`` a ``'9'``. Se lo è, fai sì che il display a 7 segmenti mostri il numero corrispondente.

.. code-block:: Arduino
    :emphasize-lines: 9

    void loop() {
        if (Serial.available() > 0) {
            // Stampa il carattere ricevuto dalla porta seriale
            // Serial.println(Serial.read());

            // Leggi il carattere ricevuto dalla porta seriale
            char receivedChar = Serial.read();
            // Converti il carattere in un numero
            int digit = receivedChar - '0';

            if (digit >= 0 && digit <= 9) {
                digitalWrite(STcp, LOW);                        // Mantieni ST_CP a livello basso durante la trasmissione
                shiftOut(DS, SHcp, MSBFIRST, datArray[digit]);  // Sposta i dati, MSB primo
                digitalWrite(STcp, HIGH);                       // Imposta ST_CP a livello alto per salvare i dati
                delay(1000);                                    // Attendi un secondo
            }
        }
    }

10. Il tuo codice completo dovrebbe essere il seguente. Ora puoi caricare il codice sull'Arduino Uno R3 e aprire il Serial Monitor. Inserisci un numero tra 0 e 9 per vedere se il display a 7 segmenti mostra il numero corrispondente.

.. code-block:: Arduino

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595
    // visualizza 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        // Imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // Configura la comunicazione seriale a 9600 baud
    }   

    void loop() {
        if (Serial.available() > 0) {
            // Stampa il carattere ricevuto dalla porta seriale
            // Serial.println(Serial.read());

            // Leggi il carattere ricevuto dalla porta seriale
            char receivedChar = Serial.read();
            // Converti il carattere in un numero
            int digit = receivedChar - '0';

            if (digit >= 0 && digit <= 9) {
                digitalWrite(STcp, LOW);                        // Mantieni ST_CP a livello basso durante la trasmissione
                shiftOut(DS, SHcp, MSBFIRST, datArray[digit]);  // Sposta i dati, MSB primo
                digitalWrite(STcp, HIGH);                       // Imposta ST_CP a livello alto per salvare i dati
                delay(1000);                                    // Attendi un secondo
            }
        }
    }

11. Infine, ricordati di salvare il tuo codice e di sistemare il tuo spazio di lavoro.

**Riepilogo**

In questa lezione, hai imparato come utilizzare il registro a scorrimento 74HC595 per pilotare un display a 7 segmenti e ridurre il numero di pin necessari sull'Arduino Uno R3. Hai anche esplorato le rappresentazioni binarie dei numeri da visualizzare e hai appreso come convertire i numeri binari in formato decimale ed esadecimale, migliorando la leggibilità del codice.

Inoltre, hai imparato a utilizzare il Serial Monitor per l'input seriale e come i caratteri di input vengono convertiti internamente in codici ASCII. Capendo questa conversione, sei stato in grado di mappare i caratteri ai loro equivalenti numerici, consentendo una visualizzazione accurata sul display a 7 segmenti.

Nel complesso, questa lezione ha fornito una comprensione completa dell'uso dei registri a scorrimento, del controllo dei display a 7 segmenti e della gestione della comunicazione seriale per progetti interattivi.


