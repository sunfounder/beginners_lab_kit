.. note::

    Ciao, benvenuto nella community di appassionati di SunFounder Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci Raspberry Pi, Arduino ed ESP32 con altri appassionati.

    **Perché unirsi?**

    - **Supporto tecnico**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaways**: Partecipa a concorsi e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

19. Sistema di Allarme per Parcheggio in Retromarcia
=========================================================

.. image:: img/19_packing.png
    :width: 600
    :align: center

Quando si parcheggia in retromarcia, è fondamentale essere consapevoli degli ostacoli dietro al veicolo, specialmente in situazioni di visibilità ridotta. 
Per aumentare la sicurezza, molti veicoli moderni sono dotati di sistemi di avviso per la retromarcia. 

In questo progetto, utilizzeremo un Arduino, un sensore a ultrasuoni e un buzzer attivo per simulare un tale sistema. 
Il sensore a ultrasuoni aiuta a rilevare la distanza dagli ostacoli dietro al veicolo e, quando questa distanza diventa troppo breve, il buzzer attivo emetterà un segnale per avvisare il conducente. 

Questo progetto non solo ci permette di comprendere meglio il funzionamento dei sensori a ultrasuoni, ma ci insegna anche come programmare e controllare Arduino per implementare una pratica funzione di avviso per la retromarcia.

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/19_reverse_parking_system.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
  

**Modulo Ultrasuoni**


Immagina di trovarti in una stanza buia e di non poter vedere gli oggetti intorno a te. In questa situazione, potresti battere le mani per produrre un suono che si propaga verso l'esterno. Quando questo suono colpisce un muro o un altro oggetto, rimbalza come un eco. Se ascolti attentamente, puoi sentire questo eco. Calcolando il tempo che impiega il suono a viaggiare verso l'esterno e a tornare indietro, puoi stimare approssimativamente a che distanza si trova il muro o l'oggetto. I sensori a ultrasuoni funzionano in modo simile per "vedere" il mondo circostante.

.. image:: img/19_ultrasonic_pic.png
    :width: 400
    :align: center

I sensori a ultrasuoni sono composti principalmente da due parti: un trasmettitore e un ricevitore, proprio come la tua bocca e le tue orecchie.

1. Emissione di Onde Sonore:

Quando il sensore a ultrasuoni è attivato, il trasmettitore emette una serie di onde sonore rapide, simili a un battito di mani. Queste onde sonore hanno una frequenza così alta che le nostre orecchie non possono sentirle.

2. Propagazione e Ritorno del Suono:

Le onde sonore si propagano fino a colpire qualcosa, come un muro o un tavolo, per poi rimbalzare indietro.

3. Ricezione delle Onde Sonore:

Il ricevitore del sensore a ultrasuoni è responsabile di "ascoltare" questi echi, proprio come le tue orecchie catturano le onde sonore riflesse dagli oggetti.

4. Calcolo della Distanza:

Il sensore registra il tempo impiegato dalle onde sonore per viaggiare verso 
l'oggetto e tornare indietro. Poiché la velocità del suono è nota (circa 340 
metri al secondo nell'aria), moltiplicando questo tempo per la velocità del 
suono otteniamo la distanza totale percorsa dalle onde sonore. Poiché abbiamo 
bisogno solo della distanza di andata verso l'oggetto, dividiamo la distanza 
totale per 2 per ottenere il risultato finale.
Questa tecnologia rende i sensori a ultrasuoni molto utili in molte situazioni, 
come aiutare i robot a evitare ostacoli o assistere i conducenti indicando la 
distanza dagli oggetti durante le manovre in retromarcia.

.. image:: img/19_ultrasonic_ms.png
    :width: 500
    :align: center


**Temporizzazione Ultrasuoni**

Il diagramma di temporizzazione è mostrato di seguito. 
È necessario fornire un breve impulso di 10us per l'ingresso di trigger per avviare il rilevamento della distanza, 
e successivamente il modulo emetterà una raffica di 8 cicli di ultrasuoni a 40 kHz e alzerà il segnale di eco. 
Puoi calcolare la distanza tramite l'intervallo di tempo tra l'invio del segnale di trigger e la ricezione del segnale di eco.

Formula: us / 58 = centimetri oppure us / 148 = pollici; oppure: la distanza = tempo ad alto livello * velocità (340 m/s) / 2; 
è consigliato utilizzare un ciclo di misurazione superiore a 60ms per evitare collisioni di segnale tra il segnale di trigger e il segnale di eco.

.. image:: img/19_ultrasonic_timing.png
    :width: 600
    :align: center


Assemblaggio del Circuito
--------------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Ultrasonic Module
     - 1 * Active Buzzer
     - Jumper Wires
   * - |list_uno_r3| 
     - |list_ultrasonic| 
     - |list_active_buzzer| 
     - |list_wire| 
   * - 1 * USB Cable
     - 1 * Breadboard
     - 1 * Multimeter
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     - 



**Fase di Assemblaggio**

Segui il diagramma di collegamento o i passaggi qui sotto per costruire il tuo circuito.

.. image:: img/19_reversing_aid_bb.png
    :width: 600
    :align: center


Creazione del Codice
------------------------

1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando “New Sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson19_reversin_alarm`` utilizzando ``Ctrl + S`` o cliccando su “Save”.

3. Per prima cosa, dobbiamo definire i pin dell'Arduino collegati al sensore a ultrasuoni e al buzzer. Questo passaggio è cruciale poiché stabilisce la base per l'interfaccia hardware.

* **TRIGGER_PIN** e **ECHO_PIN** vengono utilizzati per attivare e ricevere echi dal sensore a ultrasuoni.
* **BUZZER_PIN** è il pin collegato al buzzer.

.. code-block:: Arduino

  #define TRIGGER_PIN  10
  #define ECHO_PIN     9
  #define BUZZER_PIN   2


4. Nella funzione setup(), impostiamo la modalità per ogni pin. Il pin Trig deve essere impostato come output (poiché invia il segnale), il pin Echo è impostato come input (poiché riceve il segnale) e il pin del buzzer è impostato anch'esso come output (poiché deve emettere un suono).

.. code-block:: Arduino

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);
    pinMode(ECHO_PIN, INPUT);
    pinMode(BUZZER_PIN, OUTPUT);
    Serial.begin(9600); // Avvia la comunicazione seriale per il debug e la visualizzazione delle distanze
  }

5. Scrivere la Funzione measureDistance():

La funzione measureDistance() incapsula la logica necessaria per attivare il sensore a ultrasuoni e leggere la distanza basata sull'eco ricevuto:

a. Attivazione dell'Impulso Ultrasuoni

  * Imposta il TRIGGER_PIN su LOW inizialmente per garantire un impulso pulito.
  * Un breve ritardo di 2 microsecondi garantisce che la linea sia libera.
  * Invia un impulso HIGH di 10 microsecondi al TRIGGER_PIN. Questo impulso dice al sensore di emettere un'onda sonora ultrasonica.
  * Imposta il TRIGGER_PIN su LOW per terminare l'impulso.

  .. code-block:: Arduino

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Assicura che il pin Trig sia su LOW prima di un impulso
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Invia un impulso HIGH
      delayMicroseconds(10);           // Durata dell'impulso di 10 microsecondi
      digitalWrite(TRIGGER_PIN, LOW);  // Termina l'impulso HIGH
    }

.. note::

  Nelle lezioni precedenti, abbiamo lavorato con variabili di tipo ``int`` e ``float``. Ora, cerchiamo di capire cosa sono le variabili ``long`` e ``unsigned long``:

  * ``long``: Un intero di tipo ``long`` è una versione estesa di un ``int``. Viene utilizzato per memorizzare valori interi più grandi che superano la capacità di un ``int`` standard. Un ``long`` occupa tipicamente 32 o 64 bit di memoria, il che gli consente di contenere valori molto più grandi, sia positivi che negativi.
  * ``unsigned long``: Un ``unsigned long`` è simile a un ``long`` ma può rappresentare solo valori non negativi. Utilizza il bit normalmente riservato per il segno per estendere l'intervallo dei valori possibili, ma solo nello spettro positivo.


b. Lettura dell'Eco

  * La funzione pulseIn() viene utilizzata sul pin ECHO_PIN per misurare la durata dell'impulso in arrivo. Questa funzione attende che il pin diventi HIGH, misura per quanto tempo rimane su HIGH e quindi restituisce la durata in microsecondi.
  * Questa durata è il tempo impiegato dall'impulso ultrasonico per viaggiare verso l'oggetto e tornare indietro.

  .. code-block:: Arduino
    :emphasize-lines: 7

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Assicura che il pin Trig sia su LOW prima di un impulso
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Invia un impulso HIGH
      delayMicroseconds(10);           // Durata dell'impulso di 10 microsecondi
      digitalWrite(TRIGGER_PIN, LOW);  // Termina l'impulso HIGH
      long duration = pulseIn(ECHO_PIN, HIGH);  // Misura la durata del segnale HIGH sul pin Echo
    }

c. Calcolo della Distanza

  * La velocità del suono nell'aria (circa 340 m/s) viene utilizzata qui. La formula per calcolare la distanza è (durata * velocità del suono) / 2. Dividiamo per 2 perché l'onda sonora viaggia verso l'oggetto e torna indietro, quindi abbiamo bisogno solo della metà della distanza per una misurazione a senso unico.
  * Nel nostro codice, viene utilizzato 0,034 cm/us (velocità del suono in cm/microsecondo) come fattore di conversione.

  .. code-block:: Arduino
    :emphasize-lines: 8,9

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Assicura che il pin Trig sia su LOW prima di un impulso
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Invia un impulso HIGH
      delayMicroseconds(10);           // Durata dell'impulso di 10 microsecondi
      digitalWrite(TRIGGER_PIN, LOW);  // Termina l'impulso HIGH
      long duration = pulseIn(ECHO_PIN, HIGH);  // Misura la durata del segnale HIGH sul pin Echo
      long distance = duration * 0.034 / 2;     // Calcola la distanza (in cm)
      return distance;
    }


6. Implementare il Ciclo Principale
Nella funzione loop(), la distanza viene misurata frequentemente utilizzando la funzione measureDistance(). 
Vengono prese decisioni in base a questa distanza, come ad esempio se attivare il buzzer.

.. code-block:: Arduino

  void loop() {
    long distance = measureDistance(); // Misura la distanza
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance > 0 && distance <= 50) {
      digitalWrite(BUZZER_PIN, HIGH);  // Attiva il buzzer se vicino
      delay(100);                      // Il buzzer suona per 100 millisecondi
      digitalWrite(BUZZER_PIN, LOW);   // Spegne il buzzer
    } else {
      digitalWrite(BUZZER_PIN, LOW);   // Mantiene il buzzer spento
    }

    delay(100);  // Ritardo tra le misurazioni per prevenire il sovraccarico del sensore
  }


7. Ecco il codice completo. Ora puoi cliccare su "Upload" per caricare il codice su Arduino Uno R3.

.. code-block:: Arduino

  #define TRIGGER_PIN  10
  #define ECHO_PIN     9
  #define BUZZER_PIN   2

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Imposta il pin Trig come output
    pinMode(ECHO_PIN, INPUT);      // Imposta il pin Echo come input
    pinMode(BUZZER_PIN, OUTPUT);   // Imposta il pin del buzzer come output
    Serial.begin(9600);            // Avvia la comunicazione seriale per il debug
  }

  void loop() {
    long distance = measureDistance(); // Chiama la funzione per misurare la distanza
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance > 0 && distance <= 50) { // Se la distanza è entro 50 centimetri
      digitalWrite(BUZZER_PIN, HIGH);     // Accendi il buzzer
      delay(100);                         // Il buzzer suona per 100 millisecondi
      digitalWrite(BUZZER_PIN, LOW);      // Spegni il buzzer
    } else {
      digitalWrite(BUZZER_PIN, LOW);      // Mantieni il buzzer spento
    }

    delay(100);  // Ritardo tra le misurazioni
  }

  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Assicura che il pin Trig sia su LOW prima di un impulso
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH); // Invia un impulso HIGH
    delayMicroseconds(10);           // Durata dell'impulso di 10 microsecondi
    digitalWrite(TRIGGER_PIN, LOW);  // Termina l'impulso HIGH

    long duration = pulseIn(ECHO_PIN, HIGH);  // Misura la durata del segnale HIGH sul pin Echo
    long distance = duration * 0.034 / 2;     // Calcola la distanza (in cm)
    return distance;
  }

8. Infine, ricorda di salvare il codice e riordinare il tuo spazio di lavoro.

**Domanda**

Se vuoi che la distanza rilevata da questo dispositivo sia più accurata con i decimali, come dovresti modificare il codice?

