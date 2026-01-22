.. note::

    Ciao, benvenuto nella comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché unirti?**

    - **Supporto Esperti**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotti e anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Omaggi**: Partecipa a omaggi e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi stesso!

10. LAMPADA DA SCRIVANIA ON/OFF
====================================

In questa lezione, amplierai il progetto precedente aggiungendo una funzione pratica alla tua lampada da scrivania regolabile: un pulsante per accendere e spegnere. Questo miglioramento simula uno scenario reale in cui le lampade da scrivania vengono accese o spente e poi regolate per la luminosità usando un dimmer, imitandone più da vicino la funzionalità quotidiana.

.. image:: img/10_desk_lamp_button.jpg
    :width: 500
    :align: center

* Impara a usare il Serial Monitor per la visualizzazione in tempo reale dei dati.
* Implementa la modalità ``INPUT_PULLUP`` per gestire in modo efficiente gli input dei pulsanti.
* Comprendi come rilevare i cambiamenti di stato.
* Esplora le caratteristiche dei segnali digitali e analogici.
* Utilizza istruzioni condizionali (``if else``).

Costruisci il Circuito
------------------------------------

**Componenti Necessari**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED Rosso
     - 1 * Resistenza 220Ω
     - 1 * Potenziometro
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Pulsante
     - 1 * Cavo USB
     - 1 * Breadboard
     - Fili di Collegamento
   * - |list_button| 
     - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 



**Fasi di Costruzione**

1. Inizia con il circuito della lampada da scrivania dalla lezione precedente.

.. image:: img/9_dimmer_led1_pin9.png
    :width: 500
    :align: center

2. Inserisci il pulsante nel breadboard attraverso il gap centrale, con i pin nei fori 6E, 8E, 6J e 8J.

.. note::

    Se non sei sicuro di come inserire il pulsante, prova entrambe le orientazioni. In un modo, la distanza tra i pin sarà leggermente troppo stretta per adattarsi.

.. image:: img/10_desk_lamp_button_button.png
    :width: 500
    :align: center

3. Collega il pin in basso a sinistra del pulsante al pin digitale 7 dell'Arduino Uno R3 con un lungo filo di collegamento, inserendo un'estremità nel foro 8J e l'altra nel pin 7.

.. image:: img/10_desk_lamp_button_p7.png
    :width: 500
    :align: center

4. Collega il pin in alto a destra del pulsante alla barra negativa del breadboard con un corto filo di collegamento, inserendo un'estremità nel foro 6A e l'altra nella barra negativa.

.. image:: img/10_desk_lamp_button_gnd.png
    :width: 500
    :align: center


Creazione del Codice
--------------------------

**Stampa dello Stato del Pulsante**

1. Apri lo sketch che hai salvato in precedenza, ``Lesson9_Desk_Lamp``. Fai clic su "Salva come..." dal menu "File" e rinominalo ``Lesson10_Desk_Lamp_Button``. Fai clic su "Salva".

2. Nella Lezione 8, abbiamo usato un pulsante con una resistenza pull-down da 10K collegata manualmente tra GND e il pulsante. Tuttavia, in questo circuito non abbiamo collegato una resistenza. Invece, possiamo utilizzare la funzione pull-up del software Arduino. Devi impostare il pin collegato al pulsante come input e allo stesso tempo attivare la modalità ``PULLUP``.

.. code-block:: Arduino
    :emphasize-lines: 6

    int potValue = 0;

    void setup() {
        // inserisci qui il tuo codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);        // Imposta il pin 9 come output
        pinMode(7, INPUT_PULLUP);  // Imposta il pin 7 come input con resistenza pull-up interna
    }

3. Per utilizzare il Serial Monitor, devi includere un comando che avvia la comunicazione seriale sull'Arduino Uno R3. 

Questo comando viene tipicamente inserito nella sezione ``void setup()`` dello sketch. Il comando ``Serial.begin(baud)`` avvia la comunicazione seriale, dove ``baud`` rappresenta la velocità di trasferimento dati al secondo tra il computer e l'Arduino Uno R3. Le velocità di trasmissione comuni sono 9600 e 115200 bit al secondo.

.. code-block:: Arduino
    :emphasize-lines: 7

    int potValue = 0;

    void setup() {
        // inserisci qui il tuo codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);        // Imposta il pin 9 come output
        pinMode(7, INPUT_PULLUP);  // Imposta il pin 7 come input con resistenza pull-up interna
        Serial.begin(9600);        // Configurazione della comunicazione seriale a 9600 baud
    }


4. Prima di entrare nella ``void loop()``, dobbiamo anche creare due variabili per inizializzare gli stati del pulsante e del LED. Il LED deve essere spento quando non c'è interazione, quindi impostalo su LOW. Poiché il pulsante utilizza una resistenza pull-up interna, leggerà HIGH quando non viene premuto.

.. code-block:: Arduino
    :emphasize-lines: 2,3

    int potValue = 0;  // Variabile per memorizzare il valore letto dal potenziometro
    int ledState = LOW;          // Stato iniziale del LED
    int lastButtonState = HIGH;  // Lettura precedente dal pin di input

    void setup() {
        pinMode(9, OUTPUT);        // Imposta il pin 9 come output
        pinMode(7, INPUT_PULLUP);  // Imposta il pin 7 come input con resistenza pull-up interna
        Serial.begin(9600);        // Configurazione della comunicazione seriale a 9600 baud
    }

5. Ora, nella ``void loop()``, leggi prima lo stato del pulsante utilizzando ``digitalRead()`` e memorizzalo nella variabile ``buttonState``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
    }

6. Ora sei pronto per utilizzare il Serial Monitor per stampare i dati. Utilizzerai ``Serial.print()`` per visualizzare dati e altri testi.

Ecco come usarlo:


    * ``Serial.print(val)`` o ``Serial.print(val, format)``: Stampa dati sulla porta seriale come testo ASCII leggibile dall'uomo. 

    **Parametri**
        - ``Serial``: oggetto della porta seriale.
        - ``val``: il valore da stampare. Tipi di dati consentiti: qualsiasi tipo di dato.

    **Ritorna**
        ``print()`` restituisce il numero di byte scritti, anche se leggere quel numero è opzionale. Tipo di dato: size_t.

Questo comando può rappresentare vari tipi di dati e formati, inclusi numeri, virgola mobile, byte e stringhe. Per esempio:

.. code-block:: Arduino

    Serial.print(78);                // stampa "78"
    Serial.print(78, BIN);           // stampa "1001110"
    Serial.print(1.23456);           // stampa "1.23"
    Serial.print(1.23456, 0);        // stampa "1"
    Serial.print('N');               // stampa "N"
    Serial.print("Hello world.");    // stampa "Hello world."


7. Ora, utilizza questo comando per stampare un messaggio che indichi i dati che verranno stampati. Questo è utile quando si differenziano più stampe di dati contemporaneamente.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
        Serial.print("Button State: ");
    }

8. Ora stampa il valore memorizzato nella variabile ``buttonState``. Per assicurarti che ogni output appaia su una nuova riga nel Serial Monitor, utilizza ``Serial.println()``, che aggiunge un carattere di nuova riga alla fine dell'istruzione di stampa.
    
.. note::

    Nota la differenza tra la stampa di caratteri o stringhe (che devono essere racchiusi tra virgolette) e variabili che vengono inserite direttamente.
    
.. code-block:: Arduino
    :emphasize-lines: 14

    int potValue = 0;  // Variabile per memorizzare il valore letto dal potenziometro
    int ledState = LOW;          // Stato iniziale del LED
    int lastButtonState = HIGH;  // La lettura precedente dal pin di input

    void setup() {
        pinMode(9, OUTPUT);        // Imposta il pin 9 come output
        pinMode(7, INPUT_PULLUP);  // Imposta il pin 7 come input con resistenza pull-up interna
        Serial.begin(9600);        // Configurazione della comunicazione seriale a 9600 baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Stampa lo stato attuale del pulsante
    }

9. A questo punto, il codice è essenzialmente completo. Fai clic su "Carica" per caricare il codice sull'Arduino Uno R3.

    .. note::

        Ogni volta che vengono trasmessi dati dalla scheda al computer, dovresti vedere lampeggiare il LED TX sull'Arduino Uno R3.

10. Successivamente, fai clic sul pulsante "Serial Monitor" nell'angolo in alto a destra dell'IDE di Arduino.

    .. image:: img/10_dimmer_led_serial.png
        :align: center

11. Se vedi dati incomprensibili visualizzati, sarà necessario regolare il baud rate per farlo corrispondere a quello impostato nel codice.

    .. image:: img/10_dimmer_led_serial_baud.png
        :align: center

12. Noterai che quando il pulsante non è premuto, stampa continuamente "1", e quando il pulsante è premuto, stampa continuamente "0". Questa è la caratteristica di un segnale digitale, che ha solo due stati: "0" e "1".

**Rilevare i Cambiamenti di Stato del Pulsante**

In questa sezione, impareremo come un semplice pulsante può controllare un LED alternando il suo stato da ACCESO a SPENTO e viceversa. Questo comporta il rilevamento del momento preciso in cui il pulsante cambia da non premuto a premuto.

1. Iniziamo con la funzione principale che monitora la pressione del pulsante.

In precedenza, abbiamo imparato come determinare se un pulsante è premuto leggendo il suo stato come ``HIGH`` o ``LOW``. Tuttavia, questa lezione mira a rispondere a una singola pressione senza la necessità di mantenere premuto il pulsante. Questo richiede di rilevare un cambiamento nello stato del pulsante.

Per ottenere questo, utilizziamo un'istruzione ``if`` che confronta lo stato precedente del pulsante (``lastButtonState``) con il suo stato attuale (``buttonState``). L'operatore logico ``&&`` viene utilizzato qui, il che significa che entrambe le condizioni devono essere vere affinché il blocco di codice all'interno dell'istruzione ``if`` venga eseguito.

.. code-block:: Arduino
    :emphasize-lines: 7,8

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
        Serial.print("Stato del Pulsante: ");
        Serial.println(buttonState);  // Stampa lo stato attuale del pulsante
            
        // Verifica se lo stato del pulsante è cambiato dall'ultima iterazione del ciclo
        if (lastButtonState == HIGH && buttonState == LOW) {  // Rilevata pressione del pulsante
        }
    }

2. Quando il pulsante viene rilevato come premuto, alterniamo lo stato del LED. Questo significa che se il LED era spento, si accende, e se era acceso, si spegne. L'operatore ``!`` viene utilizzato per invertire lo stato della variabile ledState.


.. code-block:: Arduino
    :emphasize-lines: 8

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
        Serial.print("Stato del Pulsante: ");
        Serial.println(buttonState);  // Stampa lo stato attuale del pulsante
            
        // Verifica se lo stato del pulsante è cambiato dall'ultima iterazione del ciclo
        if (lastButtonState == HIGH && buttonState == LOW) {  // Rilevata pressione del pulsante
            ledState = !ledState;                               // Alterna lo stato del LED
        }
    }

3. Dopo aver controllato lo stato del pulsante e aggiornato di conseguenza il LED, dobbiamo registrare lo stato attuale del pulsante come il nuovo 'ultimo stato conosciuto'. Questo passaggio è cruciale per rilevare il prossimo cambiamento di stato.

.. code-block:: Arduino
    :emphasize-lines: 10,11

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Stampa lo stato attuale del pulsante
        
        // Verifica se lo stato del pulsante è cambiato dall'ultima iterazione del ciclo
        if (lastButtonState == HIGH && buttonState == LOW) {  // Rilevata pressione del pulsante
            ledState = !ledState;                               // Alterna lo stato del LED
        }
        lastButtonState = buttonState;  // Aggiorna lastButtonState allo stato corrente
        delay(200);                     // Opzionale: Debouncing software semplice
    }

**Regolare la Luminosità con un Potenziometro**

In situazioni in cui ``ledState`` è ``HIGH``, vogliamo che il LED non solo si accenda, ma che la sua luminosità possa essere regolata da un potenziometro. Ecco come implementare questa funzionalità:


1. Subito dopo l'istruzione ``if`` che alterna lo stato del LED alla pressione del pulsante, aggiungi un'altra istruzione ``if`` per verificare se ``ledState`` è ``HIGH``. Se lo è, qui è dove regoleremo la luminosità del LED in base al valore del potenziometro.


.. code-block:: Arduino
    :emphasize-lines: 10,12

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Stampa lo stato attuale del pulsante
        
        // Verifica se lo stato del pulsante è cambiato dall'ultima iterazione del ciclo
        if (lastButtonState == HIGH && buttonState == LOW) {  // Rilevata pressione del pulsante
            ledState = !ledState;                               // Alterna lo stato del LED
        }
        if (ledState == HIGH) {

        }
        lastButtonState = buttonState;  // Aggiorna lastButtonState allo stato corrente
        delay(200);                     // Opzionale: Debouncing software semplice
    }

2. All'interno del blocco ``if (ledState == HIGH)``, leggi il valore del potenziometro per determinare il livello di luminosità. Quindi, applica questo valore per regolare la luminosità del LED utilizzando ``analogWrite()``. Stampa anche questo valore sul Serial Monitor per ottenere un feedback in tempo reale.

.. code-block:: Arduino
    :emphasize-lines: 6-9

    // Verifica se lo stato del pulsante è cambiato dall'ultima iterazione del ciclo
    if (lastButtonState == HIGH && buttonState == LOW) {  // Rilevata pressione del pulsante
        ledState = !ledState;                               // Alterna lo stato del LED
    }
    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Leggi continuamente il valore del potenziometro quando il LED è acceso
        analogWrite(9, potValue / 4);  // Regola la luminosità in modo continuo
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    }
    lastButtonState = buttonState;  // Aggiorna lastButtonState allo stato corrente
    delay(200);                     // Opzionale: Debouncing software semplice

3. Per garantire che il LED si spenga quando ``ledState`` è ``LOW``, aggiungi una dichiarazione ``else`` subito dopo il blocco ``if``. Questo gestirà lo spegnimento completo del LED quando le condizioni all'interno del blocco ``if`` non vengono soddisfatte.

.. image:: img/if_else.png
    :width: 400
    :align: center


.. code-block:: Arduino
    :emphasize-lines: 6-8

    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Leggi continuamente il valore del potenziometro quando il LED è acceso
        analogWrite(9, potValue / 4);  // Regola la luminosità in modo continuo
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    } else {
        analogWrite(9, 0);  // Spegne il LED
    }

**Esecuzione del Codice**

Ora che il codice è completo, l'elenco completo è il seguente:

.. code-block:: Arduino

    int potValue = 0;            // Variabile per memorizzare il valore letto dal potenziometro
    int ledState = LOW;          // Stato iniziale del LED
    int lastButtonState = HIGH;  // La lettura precedente dal pin di input

    void setup() {
        pinMode(9, OUTPUT);        // Imposta il pin 9 come output
        pinMode(7, INPUT_PULLUP);  // Imposta il pin 7 come input con resistenza pull-up interna
        Serial.begin(9600);        // Configurazione della comunicazione seriale a 9600 baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Leggi lo stato del pulsante
        Serial.print("Button State: ");
        Serial.println(buttonState);

        // Verifica se lo stato del pulsante è cambiato dall'ultima iterazione del ciclo
        if (lastButtonState == HIGH && buttonState == LOW) {  // Rilevata pressione del pulsante
            ledState = !ledState;                               // Alterna lo stato del LED
        }

        if (ledState == HIGH) {
            potValue = analogRead(A0);  // Leggi continuamente il valore del potenziometro quando il LED è acceso
            analogWrite(9, potValue / 4);  // Regola la luminosità in modo continuo
            Serial.print("Valore Potenziometro: ");
            Serial.println(potValue);
        } else {
            analogWrite(9, 0);  // Spegne il LED
        }

        lastButtonState = buttonState;  // Aggiorna lastButtonState allo stato corrente
        delay(200);                     // Opzionale: Debouncing software semplice
    }

1. Dopo aver selezionato la scheda e la porta corrette, fai clic su "Carica" per caricare il codice sul tuo Arduino.

2. Apri il Serial Monitor per visualizzare i dati in uscita. Noterai che lo stato del pulsante stampa "1" continuamente quando non è premuto e "0" nel momento in cui il pulsante viene premuto. Allo stesso tempo, verrà stampato anche il valore del potenziometro. Man mano che ruoti il potenziometro, noterai nel Serial Monitor che più alto è il valore, più luminoso diventa il LED, e viceversa.
    
.. image:: img/10_dimmer_led_serial_tool.png
    :align: center

.. note::

    Da questo, dovresti capire chiaramente:

    - I segnali digitali hanno solo due stati: 0 e 1.
    - I segnali analogici, invece, hanno un intervallo, che in questo caso va da 0 a 1023.

3. Infine, ricorda di salvare il tuo codice e di riordinare il tuo spazio di lavoro.

**Domande**

1. Cosa succederebbe se impostassi il pin digitale 7 solo su INPUT? Perché?

.. code-block::
    :emphasize-lines: 3

    void setup() {
        pinMode(9, OUTPUT);        // Imposta il pin 9 come output
        pinMode(7, INPUT);  // Imposta il pin 7 come input con resistenza pull-up interna
        Serial.begin(9600);        // Configurazione della comunicazione seriale a 9600 baud
    }

2. Se il pin 7 è impostato solo su ``INPUT``, quali aggiustamenti dovrebbero essere fatti al circuito?

**Riassunto**

Alla fine di questa lezione, avrai una lampada da scrivania ON/OFF completamente funzionante controllata tramite una semplice interfaccia utente. Avrai imparato come integrare e manipolare vari componenti elettronici e tecniche di programmazione Arduino per creare un dispositivo elettronico pratico e interattivo. Questo progetto non solo rafforza i concetti fondamentali di elettronica e programmazione, ma ti offre anche un pezzo funzionante da aggiungere alla tua collezione di progetti fai-da-te.

