.. note::

    Ciao, benvenuto nella SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a promozioni e omaggi durante le festività.

    👉 Sei pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

22. Suona "Twinkle, Twinkle, Little Star"
==============================================

In questa lezione, ci addentreremo nell'affascinante connubio tra musica e tecnologia. Imparerai come vengono prodotti i diversi suoni musicali attraverso le variazioni di frequenza, e come questo principio possa essere applicato utilizzando un microcontrollore come Arduino per controllare un buzzer. Al termine di questa lezione, non solo capirai le basi delle frequenze musicali, ma sarai anche in grado di programmare un Arduino per riprodurre una semplice melodia.

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/22_little_star.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Alla fine di questa lezione sarai in grado di:

* Imparare come i suoni musicali corrispondono a frequenze specifiche.
* Semplificare la programmazione utilizzando array per memorizzare e gestire le note musicali.
* Scrivere ed eseguire un programma che controlla un buzzer passivo per suonare "Twinkle, Twinkle, Little Star".

Frequenze Musicali e Produzione del Suono
----------------------------------------------

.. image:: img/7_sound.png
  :width: 400
  :align: center

I vari strumenti musicali producono suoni diversi modificando la frequenza. 
Ad esempio, su un pianoforte, colpire i tasti fa vibrare rapidamente le corde corrispondenti, producendo specifiche note. 
Scienziati e musicisti hanno sviluppato vari metodi di accordatura e standard di intonazione musicale misurando con precisione queste frequenze di vibrazione.

Quando controlli un Arduino o un altro microcontrollore per inviare un segnale elettrico a un buzzer, il diaframma del buzzer vibra rapidamente in base alla frequenza del segnale, 
producendo così il suono. Ad esempio, un segnale impostato su 440 Hz produrrà il tono musicale standard "A4", che è un punto di riferimento per l'accordatura musicale. 
Man mano che la frequenza aumenta o diminuisce, anche il tono prodotto sale o scende, ottenendo così una gamma di suoni dal più basso al più alto in una composizione musicale.

Nella musica occidentale, un'ottava include 12 semitoni, dalla nota C alla B, e poi si torna a una C più alta.

Ad esempio, la frequenza del Do centrale (C4) è di circa 261,63 Hz. La frequenza di una nota può essere calcolata utilizzando la seguente formula:

.. image:: img/7_music_format.png

dove f_0 è la nota di riferimento (solitamente A4, con frequenza 440 Hz), e n è il numero di semitoni rispetto alla nota di riferimento. Numeri positivi indicano un aumento, numeri negativi una diminuzione. 
Utilizzando questa formula, possiamo calcolare la frequenza di qualsiasi nota.

Ecco una tabella di frequenze:

* C (C4): 262 Hz (actually close to 261.63 Hz, rounded to 262)
* D (D4): 294 Hz
* E (E4): 330 Hz
* F (F4): 349 Hz
* G (G4): 392 Hz
* A (A4): 440 Hz
* B (B4): 494 Hz

Ora esploreremo i segreti delle note musicali utilizzando Arduino e un buzzer. Facciamo suonare al buzzer passivo le prime due righe di "Twinkle, Twinkle, Little Star":

.. note::

  La melodia di "Twinkle, Twinkle, Little Star" si basa su combinazioni di note semplici, 
  e deriva dalla variazione di "Ah vous dirai-je, Maman" del compositore francese Wolfgang Amadeus Mozart, 
  rendendola molto adatta ai principianti.

  Ecco lo spartito di base per "Twinkle, Twinkle, Little Star", con ciascuna nota:

  .. code-block::

    C C G G A A G
    F F E E D D C
    G G F F E E D
    G G F F E E D
    C C G G A A G
    F F E E D D C

Costruzione del Circuito
----------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Breadboard
     - 1 * Buzzer Passivo
     - Fili Jumper
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_passive_buzzer| 
     - |list_wire| 
   * - 1 * Cavo USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 

**Istruzioni di Montaggio**

Questa lezione utilizza lo stesso circuito della Lezione 21.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Creazione del Codice - Array
--------------------------------
1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando “New Sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson22_Array`` usando ``Ctrl + S`` o cliccando su “Salva”.

3. Ora crea un array all'inizio del codice, memorizzando le note di "Twinkle Twinkle Little Star" nell'array.

.. code-block:: Arduino

  // Definisci le frequenze delle note della scala di Do maggiore (ottava a partire dal Do centrale)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Do alto

  // Definisci un array contenente la sequenza delle note della melodia
  int melodia[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

Un array è una struttura dati utilizzata per memorizzare più elementi dello stesso tipo nella programmazione Arduino.
È uno strumento molto basilare e potente, e se utilizzato correttamente può migliorare notevolmente l'efficienza e le prestazioni del programma.
Gli array possono memorizzare elementi come numeri interi, numeri a virgola mobile e caratteri.

Simile alla creazione di variabili e funzioni, anche la creazione di un array prevede la specifica del tipo e del nome dell'array - ``int melodia[]``.

Gli elementi all'interno di ``{}`` sono chiamati elementi dell'array, a partire dall'indice 0, quindi ``melodia[0]`` corrisponde al primo ``c(262)``, e ``melodia[13]`` è anch'esso ``c(262)``.

4. Ora stampa gli elementi all'indice 0 e 13 dall'array ``melodia[]`` nel monitor seriale.

.. code-block:: Arduino
  :emphasize-lines: 17,18

  // Definisci le frequenze delle note della scala di Do maggiore (ottava a partire dal Do centrale)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Do alto

  // Definisci un array contenente la sequenza delle note della melodia
  int melodia[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

  void setup() {
    // Inserisci qui il codice di configurazione da eseguire una sola volta:
    Serial.begin(9600);  // Inizializza la comunicazione seriale a 9600 baud
    Serial.println(melody[0]);
    Serial.println(melody[13]);
  }
  
  void loop() {
    // Inserisci qui il codice principale da eseguire ripetutamente:
  }

5. Dopo aver caricato il codice sull'Arduino Uno R3, apri il monitor seriale e vedrai due valori 262.

.. code-block::

  262
  262

6. Se vuoi stampare ogni elemento dell'array ``melodia[]`` uno per uno, prima dovrai conoscere la lunghezza dell'array. Puoi usare la funzione ``sizeof()`` per calcolare il numero di elementi nell'array.

.. code-block:: Arduino
  :emphasize-lines: 4

  void setup() {
    // Inserisci qui il codice di configurazione da eseguire una sola volta:
    Serial.begin(9600);  // Inizializza la comunicazione seriale a 9600 baud
    int note = sizeof(melodia) / sizeof(melodia[0]); // Calcola il numero di elementi
  }

  
* ``sizeof(melodia)`` restituisce il numero totale di byte utilizzati da tutti gli elementi dell'array.
* ``sizeof(melodia[0])`` restituisce il numero di byte utilizzati da un singolo elemento dell'array.
* Dividendo il totale dei byte per i byte per elemento ottieni il numero totale di elementi dell'array.

7. Usa poi un'istruzione ``for`` per iterare attraverso gli elementi dell'array ``melodia[]`` e stamparli usando la funzione ``Serial.println()``.

.. code-block:: Arduino

  // Definisci le frequenze delle note della scala di Do maggiore (ottava a partire dal Do centrale)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // High C

  // Definisci un array contenente la sequenza delle note della melodia
  int melodia[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };


  void setup() {
    // Inserisci qui il codice di configurazione da eseguire una sola volta:
    Serial.begin(9600);                              // Inizializza la comunicazione seriale a 9600 baud
    int notes = sizeof(melody) / sizeof(melody[0]); // Calcola il numero di elementi
    // Cicla attraverso ogni nota nell'array melodia
    for (int i = 0; i < notes; i = i + 1) {
      // Stampa la frequenza di ciascuna nota nel monitor seriale
      Serial.println(melody[i]);
    }
  }

  void loop() {
    // Inserisci qui il codice principale da eseguire ripetutamente:
  }

8. Dopo aver caricato il codice sull'Arduino Uno R3, apri il monitor seriale e vedrai gli elementi dell'array ``melodia[]`` stampati uno per uno.

.. code-block::

  262
  262
  392
  392
  440
  440
  392
  349
  349
  330
  ...

**Domande**

Puoi anche eseguire operazioni sugli elementi dell'array, come modificare ``Serial.println(melody[i] * 1.3);``. Quali dati otterrai e perché?


Creazione del Codice - Suona "Twinkle Twinkle Little Star"
-----------------------------------------------------------

Ora che abbiamo una solida comprensione della creazione di array, dell'accesso agli elementi dell'array e del calcolo delle loro lunghezze e operazioni, applichiamo queste conoscenze per programmare un buzzer passivo a suonare 'Twinkle, Twinkle, Little Star' utilizzando frequenze e intervalli memorizzati.

1. Apri lo sketch che hai salvato in precedenza, ``Lesson22_Array``.

2. Clicca su “Salva con nome...” dal menu “File” e rinominalo come ``Lesson22_Little_Star``. Clicca su "Salva".


3. Per prima cosa, definisci il pin del buzzer.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Assegna il pin 9 alla costante per il buzzer


4. Ora crea un altro array per memorizzare la durata delle note.

.. code-block:: Arduino
  :emphasize-lines: 3

  // Configura la sequenza delle note e le loro durate in millisecondi
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

5. Ora sposta parte del codice da ``void setup()`` a ``void loop()``.

.. code-block:: Arduino
  :emphasize-lines: 8-13

  void setup() {
    // inserisci qui il codice di configurazione da eseguire una volta:
    Serial.begin(9600);                              // Inizializza la comunicazione seriale a 9600 baud
  }

  void loop() {
    // inserisci qui il codice principale da eseguire ripetutamente:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calcola il numero di elementi
    // Cicla attraverso ogni nota nell'array melodia
    for (int i = 0; i < notes; i = i + 1) {
      // Stampa la frequenza di ogni nota sul monitor seriale
      Serial.println(melody[i]);
    }
  }

6. Nella dichiarazione ``for``, commenta il codice di stampa e usa la funzione ``tone()`` per suonare le note.

.. code-block:: Arduino
  :emphasize-lines: 9

  void loop() {
    // inserisci qui il codice principale da eseguire ripetutamente:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calcola il numero di elementi
    // Cicla attraverso ogni nota nell'array melodia
    for (int i = 0; i < notes; i = i + 1) {
      // Stampa la frequenza di ogni nota sul monitor seriale
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Suona la nota
    }
  }


7. Dopo aver suonato ogni nota, per rendere la melodia più naturale, aggiungi una breve pausa tra due note. Qui moltiplichiamo la durata delle note per 1,30 per calcolare l'intervallo, facendo sembrare la melodia meno frettolosa.

.. code-block:: Arduino
  :emphasize-lines: 10

  void loop() {
    // inserisci qui il codice principale da eseguire ripetutamente:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calcola il numero di elementi
    // Cicla attraverso ogni nota nell'array melodia
    for (int i = 0; i < notes; i = i + 1) {
      // Stampa la frequenza di ogni nota sul monitor seriale
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Suona la nota
      delay(noteDurations[i] * 1.30);                // Attendi prima di cambiare nota
    }
  }

8. Usa la funzione ``noTone()`` per interrompere l'uscita del tono dal pin corrente. Questo è un passaggio necessario per assicurarsi che ogni nota venga suonata chiaramente senza sovrapporsi alla successiva.

.. code-block:: Arduino
  :emphasize-lines: 11

  void loop() {
    // inserisci qui il codice principale da eseguire ripetutamente:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calcola il numero di elementi
    // Cicla attraverso ogni nota nell'array melodia
    for (int i = 0; i < notes; i = i + 1) {
      // Stampa la frequenza di ogni nota sul monitor seriale
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Suona la nota
      delay(noteDurations[i] * 1.30);                // Attendi prima di cambiare nota
      noTone(buzzerPin);                             // Interrompi la riproduzione della nota
    }
  }

9. Il tuo codice completo è riportato di seguito e, una volta caricato sull'Arduino Uno R3, sarai in grado di ascoltare il buzzer suonare "Twinkle Twinkle Little Star".

.. code-block:: Arduino

  int buzzerPin = 9;  // Assegna il pin 9 alla costante per il buzzer

  // Definisci le frequenze delle note della scala di Do maggiore (ottava a partire dal Do centrale)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Do alto

  // Configura la sequenza delle note e le loro durate in millisecondi
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

  void setup() {
    // inserisci qui il codice di configurazione da eseguire una volta:
    Serial.begin(9600);                              // Inizializza la comunicazione seriale a 9600 baud
  }

  void loop() {
    // inserisci qui il codice principale da eseguire ripetutamente:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calcola il numero di elementi
    // Cicla attraverso ogni nota nell'array melodia
    for (int i = 0; i < notes; i = i + 1) {
      // Stampa la frequenza di ogni nota sul monitor seriale
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Suona la nota
      delay(noteDurations[i] * 1.30);                // Attendi prima di cambiare nota
      noTone(buzzerPin);                             // Interrompi la riproduzione della nota
    }
  }
  
10. Infine, ricorda di salvare il codice e riordinare lo spazio di lavoro.

**Domanda**

Se sostituisci il buzzer passivo nel circuito con un buzzer attivo, riusciresti a suonare "Twinkle Twinkle Little Star"? Perché?

**Riepilogo**

Ora che la lezione è terminata, abbiamo imparato come utilizzare gli array per memorizzare i dati, calcolare la lunghezza degli array, indicizzare gli elementi all'interno di un array e eseguire operazioni su ciascun elemento. Memorizzando le frequenze delle note e gli intervalli di tempo in array e iterando attraverso di essi con un ciclo for, abbiamo programmato con successo un buzzer passivo per suonare "Twinkle, Twinkle, Little Star".

Inoltre, abbiamo imparato a interrompere la riproduzione di una nota utilizzando la funzione ``noTone()``.

Questa lezione non solo ha rafforzato la nostra comprensione delle operazioni sugli array e delle strutture di controllo nella programmazione, ma ha anche dimostrato come questi concetti possano essere applicati per creare musica con componenti elettronici, collegando conoscenze teoriche ad applicazioni pratiche in modo divertente e coinvolgente.


