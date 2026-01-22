.. note::

    Ciao, benvenuto nella community di appassionati SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci l'uso di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto tecnico**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anticipo agli annunci di nuovi prodotti e anteprime speciali.
    - **Sconti esclusivi**: Approfitta di sconti esclusivi sui nostri nuovi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni festive.

    👉 Sei pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

20. Il Timer Pomodoro
===========================================

In questa lezione, esploreremo l'incontro tra la gestione del tempo e la tecnologia creando un Timer Pomodoro utilizzando un Arduino e un buzzer attivo. Imparerai a utilizzare le capacità di temporizzazione interne dell'Arduino per costruire un timer che suddivide il lavoro in intervalli di 25 minuti di concentrazione seguiti da pause di 5 minuti. Questo metodo, noto come la Tecnica del Pomodoro, migliora la produttività e la concentrazione. Durante il corso, acquisirai solide basi nella temporizzazione elettronica e esperienza pratica nella programmazione e assemblaggio dei circuiti, culminando nella creazione di un Timer Pomodoro funzionale. Unisciti a noi per padroneggiare il tuo tempo e aumentare l'efficienza nelle tue attività quotidiane!

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/20_beep_timer.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Al termine di questa lezione, sarai in grado di:

* Comprendere il significato storico del suono nella misurazione del tempo.
* Identificare i componenti necessari per costruire un circuito timer elettronico.
* Programmare un Arduino per controllare un buzzer per la gestione del tempo utilizzando sia la funzione ``delay()`` che ``millis()``.
* Applicare la Tecnica del Pomodoro in un contesto pratico creando un timer che alterna periodi di lavoro e pausa.

Orologi e Suono
--------------------

Nel mondo antico, grandi campane venivano utilizzate per segnare il passare del tempo e specifici eventi sociali.
Ad esempio, le città medievali europee utilizzavano i rintocchi delle campane delle chiese per segnare gli orari di preghiera e l'inizio e la fine delle giornate lavorative.
Questi rintocchi erano più che semplici segnali temporali; servivano come strumenti per mantenere l'ordine sociale, attorno ai quali ruotava la vita quotidiana della comunità.

**Orologi Meccanici e Suono**

.. image:: img/7_big_ben.png
  :width: 500
  :align: center

Con lo sviluppo degli orologi meccanici, in particolare con la progettazione del Big Ben, gli orologi iniziarono a essere dotati di campane più complesse e meccanismi di temporizzazione.
Il suono del Big Ben è prodotto dalle sue grandi campane di bronzo, migliorando sia la propagazione del suono che la precisione degli annunci temporali.
In molte città e paesi, il suono del Big Ben divenne un punto di riferimento per i residenti, permettendo loro di regolare le proprie attività quotidiane, svolgendo un ruolo cruciale nella pianificazione precisa del tempo per la navigazione,
gli orari ferroviari e molto altro.

**Temporizzazione Sonora nell'Era Elettronica**

.. image:: img/19_timer.jpg
  :width: 500
  :align: center

Con l'ingresso nell'era elettronica, i timer sonori si sono evoluti. L'introduzione dei buzzers elettronici, soprattutto con l'ausilio di microcontrollori come l'Arduino,
ha permesso alla misurazione del tempo di diventare indipendente dai grandi dispositivi meccanici. Questi piccoli dispositivi possono produrre suoni di diverse frequenze e toni,
che possono essere utilizzati per vari tipi di temporizzazione, dai semplici timer da cucina al controllo di processi industriali complessi.
Esempi includono i sistemi di chiamata per infermieri negli ospedali moderni, le campanelle scolastiche e i promemoria nei dispositivi elettronici personali, tutti utilizzano i buzzers elettronici per la gestione del tempo.

Assemblaggio del Circuito
--------------------------------

**Componenti Necessari**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Breadboard
     - 1 * Buzzer Attivo
     - Fili Jumper
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_active_buzzer| 
     - |list_wire| 
   * - 1 * Cavo USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 



**Fase di Assemblaggio**

Questa lezione utilizza lo stesso circuito della Lezione 17.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Creazione del Codice - Tick Tick
-------------------------------------

In Arduino, ``delay()`` è la funzione di temporizzazione più semplice e comunemente utilizzata.
Spesso la usiamo per mettere in pausa il programma per un breve periodo, che, combinato con i cicli, può creare un effetto LED lampeggiante. Qui, usiamo la funzione ``delay()`` per far suonare il buzzer una volta al secondo.

1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando “New Sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson20_Timer_Tick_Tick`` utilizzando ``Ctrl + S`` o cliccando su “Save”.

3. Scrivi il codice come segue:

.. code-block:: Arduino

  const int buzzerPin = 9;   // Assegna il pin 9 alla costante per il buzzer
  
  void setup() {
    // inserisci qui il setup, per eseguirlo una volta:
    pinMode(buzzerPin, OUTPUT);  // Imposta il pin 9 come output
  } 

  void loop() {
    // inserisci qui il codice principale, da eseguire ripetutamente:
    digitalWrite(buzzerPin, HIGH);  // Accendi il buzzer
    delay(100);                     // Durata del beep: 100 millisecondi
    digitalWrite(buzzerPin, LOW);   // Spegni il buzzer
    delay(1000);                    // Intervallo tra i segnali: 1000 millisecondi
  }

In questa configurazione, la prima funzione ``delay()`` mette in pausa l'Arduino Uno R3 per 100 millisecondi, durante i quali il buzzer continua a suonare. La seconda funzione ``delay()`` mette in pausa l'Arduino per 1000 millisecondi (1 secondo), durante i quali il buzzer è silenzioso.

4. Dopo aver caricato il codice sull'Arduino Uno R3, sentirai il buzzer emettere un beep ogni secondo.

Creazione del Codice - ``millis()``
-------------------------------------

Utilizzare ``delay()`` mette in pausa il codice, il che può risultare scomodo.

Ad esempio, immagina di riscaldare una pizza nel microonde mentre aspetti email importanti.
Metti la pizza nel microonde e la imposti per 10 minuti. L'analogia con l'uso di ``delay()`` è sedersi di fronte al microonde e osservare il timer contare da 10 minuti a zero. Se durante questo periodo ricevi un'email importante, la perderai.

Quello che normalmente fai è mettere la pizza nel microonde, poi controllare le tue email, magari fare qualcos'altro e periodicamente controllare se il timer è arrivato a zero, indicando che la pizza è pronta.

Arduino ha anche uno strumento di temporizzazione che non mette in pausa il programma, ed è ``millis()``.

``millis()`` è una funzione molto importante nella programmazione di Arduino. Restituisce il numero di millisecondi trascorsi da quando la scheda Arduino è stata accesa o resettata per l'ultima volta.

  * ``time = millis()``: Restituisce il numero di millisecondi trascorsi da quando la scheda Arduino ha iniziato a eseguire il programma attuale. Questo numero si azzererà (tornerà a zero) dopo circa 50 giorni.

  **Parametri**
    Nessuno

**Restituisce**
    Numero di millisecondi trascorsi dall'avvio del programma. Tipo di dato: unsigned long.

Qui faremo in modo che il buzzer emetta un beep ogni secondo.

1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando “New Sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson20_Timer_Millis`` utilizzando ``Ctrl + S`` o cliccando “Save”.

3. Prima di tutto, crea una costante chiamata ``buzzerPin`` e assegnale il valore del pin 9.

.. code-block:: Arduino
  :emphasize-lines: 1

  const int buzzerPin = 9;   // Assegna il pin 9 alla costante per il buzzer

  void setup() {
    // inserisci qui il codice di configurazione, eseguito una volta sola:
  }

4. Crea due variabili di tipo long, ``previousMillis`` che memorizzerà l'ultimo timestamp in cui il buzzer ha emesso un beep, e ``interval`` che imposta ogni quanto tempo (in millisecondi) il buzzer emetterà un beep. In questo caso, è impostato per emettere un beep ogni 1000 millisecondi (ovvero ogni secondo).

.. code-block:: Arduino
  :emphasize-lines: 3,4

  const int buzzerPin = 9;  // Assegna il pin 9 alla costante per il buzzer

  unsigned long previousMillis = 0;  // Memorizza il timestamp dell'ultima volta in cui il buzzer ha emesso un beep
  long interval = 1000;              // Intervallo in cui il buzzer emetterà un beep (millisecondi)

5. Nella funzione ``void setup()``, imposta il pin del buzzer come modalità di uscita (output).

.. code-block:: Arduino
  :emphasize-lines: 8

  const int buzzerPin = 9;  // Assegna il pin 9 alla costante per il buzzer

  unsigned long previousMillis = 0;  // Memorizza il timestamp dell'ultima volta in cui il buzzer ha emesso un beep
  long interval = 1000;              // Intervallo in cui il buzzer emetterà un beep (millisecondi)

  void setup() {
    // inserisci qui il codice di configurazione, eseguito una volta sola:
    pinMode(buzzerPin, OUTPUT);  // Imposta il pin 9 come uscita
  }

6. Nella funzione ``void loop()``, crea una variabile di tipo ``unsigned long`` chiamata ``currentMillis`` per memorizzare l'ora corrente.

.. code-block:: Arduino
  :emphasize-lines: 3

  void loop() {
    // inserisci qui il codice principale, da eseguire ripetutamente:
    unsigned long currentMillis = millis();
  }

7. Quando il tempo corrente meno l'ultimo aggiornamento supera i 1000ms, attiva alcune funzioni. Inoltre, aggiorna ``previousMillis`` con il tempo corrente, in modo che il prossimo trigger avvenga dopo 1 secondo.

.. code-block:: Arduino
  :emphasize-lines: 5,6

  void loop() {
    // inserisci qui il codice principale, da eseguire ripetutamente:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Salva l'ultima volta in cui il buzzer ha emesso un beep
    }
  }

8. Aggiungi le funzioni principali che devono essere eseguite periodicamente. In questo caso, fai suonare il buzzer.

.. code-block:: Arduino
  :emphasize-lines: 7,8,9

  void loop() {
    // inserisci qui il codice principale, da eseguire ripetutamente:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Salva l'ultima volta in cui il buzzer ha emesso un beep
      digitalWrite(buzzerPin, HIGH);   // Attiva il buzzer
      delay(100);
      digitalWrite(buzzerPin, LOW);    // Silenzio
    }
  }

9. Il codice completo dovrebbe apparire così. Caricalo sull'Arduino Uno R3 e vedrai che il buzzer emetterà un beep ogni secondo.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Assegna il pin 9 alla costante per il buzzer

  unsigned long previousMillis = 0;  // Memorizza il timestamp dell'ultima volta in cui il buzzer ha emesso un beep
  long interval = 1000;              // Intervallo in cui il buzzer emetterà un beep (millisecondi)

  void setup() {
    // inserisci qui il codice di configurazione, eseguito una volta sola:
    pinMode(buzzerPin, OUTPUT);  // Imposta il pin 9 come uscita
  }

  void loop() {
    // inserisci qui il codice principale, da eseguire ripetutamente:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Salva l'ultima volta in cui il buzzer ha emesso un beep
      digitalWrite(buzzerPin, HIGH);   // Attiva il buzzer
      delay(100);
      digitalWrite(buzzerPin, LOW);    // Silenzio
    }
  }

**Domanda**

Cosa succederebbe al programma se il comando ``delay(100);`` fosse cambiato in ``delay(1000);``? Perché?

Creazione del Codice - Pomodoro Timer
------------------------------------------

La Tecnica del Pomodoro, conosciuta anche come la Tecnica del Pomodoro, è un metodo di gestione del tempo sviluppato da Francesco Cirillo alla fine degli anni '80.
Questo metodo utilizza un timer per suddividere il lavoro in intervalli di 25 minuti, seguiti da brevi pause.
Ogni intervallo di lavoro è chiamato "pomodoro", in onore del timer da cucina a forma di pomodoro che Cirillo utilizzava durante i suoi anni universitari.

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

I passaggi base della Tecnica del Pomodoro includono:

1. **Definire il Compito**: Decidere il compito che si vuole completare prima di iniziare.
2. **Impostare il Timer Pomodoro**: Impostare un timer per 25 minuti di tempo di lavoro.
3. **Lavorare Intensamente**: Concentrarsi completamente sul compito per questi 25 minuti, evitando qualsiasi forma di distrazione.
4. **Fare una Breve Pausa**: Una volta scaduto il tempo di lavoro, fare una pausa di 5 minuti. Durante questo tempo, si può camminare, fare stretching, bere acqua, ecc., ma evitando di fare attività correlate al lavoro.

I benefici della Tecnica del Pomodoro includono un focus migliorato, riduzione della fatica, una chiara distinzione tra tempi di lavoro e di pausa, aiutando a gestire le distrazioni e aumentando la motivazione e la soddisfazione nel completare i compiti. Inoltre, la Tecnica del Pomodoro non richiede strumenti o tecnologie complesse: un semplice timer è sufficiente.

Adesso, programmeremo un timer che emetterà un segnale acustico ogni 25 minuti per segnalare la fine di un periodo di lavoro seguito da un promemoria per una pausa di 5 minuti:

1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando “New Sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson20_Timer_Millis_Pomodoro`` utilizzando ``Ctrl + S`` o cliccando “Save”.

3. Definisci alcune costanti e variabili prima di ``void setup()``.

* ``buzzerPin`` identifica a quale pin è collegato il buzzer.
* ``startMillis`` tiene traccia del momento in cui il timer è stato avviato.
* ``workPeriod`` e ``breakPeriod`` definiscono la durata di ciascun periodo.
* ``isWorkPeriod`` è una variabile booleana utilizzata per tenere traccia se è il momento di lavorare o di fare una pausa.

.. code-block:: Arduino

  const int buzzerPin = 9;          // Assegna il pin 9 alla costante per il buzzer
  unsigned long startMillis;        // Memorizza il momento in cui il timer inizia
  const long workPeriod = 1500000;  // Periodo di lavoro di 25 minuti
  const long breakPeriod = 300000;  // Periodo di pausa di 5 minuti
  static bool isWorkPeriod = true;  // Tiene traccia se è un periodo di lavoro o di pausa

4. Inizializza il pin del buzzer come output e avvia il timer registrando l'ora di inizio con ``millis()``.

.. code-block:: Arduino
  :emphasize-lines: 2,3
  
  void setup() {
    pinMode(buzzerPin, OUTPUT); // Inizializza il pin del buzzer come output
    startMillis = millis(); // Registra l'ora di inizio
  }

5. Nella funzione ``void loop()`` crea una variabile ``unsigned long`` chiamata ``currentMillis`` per memorizzare l'ora corrente.

.. code-block:: Arduino
  :emphasize-lines: 2

  void loop() {
    unsigned long currentMillis = millis(); // Aggiorna l'ora corrente
  }

6. Usa dichiarazioni condizionali ``if else if`` per determinare se è un periodo di lavoro.

.. code-block:: Arduino
  :emphasize-lines: 4-6

  void loop() {
    unsigned long currentMillis = millis(); // Aggiorna l'ora corrente

    if (isWorkPeriod){ 
    } else if (!isWorkPeriod){
    }
  }

7. Se lo è, verifica se il tempo attuale ha superato il ``workPeriod``. In tal caso, reimposta il timer, passa al periodo di pausa e attiva il buzzer per suonare due volte con una lunga durata.

.. code-block:: Arduino
  :emphasize-lines: 5-16

  void loop() {
    unsigned long currentMillis = millis();  // Aggiorna l'ora corrente

    if (isWorkPeriod) {
      if (currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis;  // Reimposta il timer
        isWorkPeriod = false;         // Passa al periodo di pausa
        digitalWrite(buzzerPin, HIGH);  // Accendi il buzzer
        delay(500);                     // Il buzzer suona per 500 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il buzzer
        delay(200);                     // Buzzer spento per 200 millisecondi
        digitalWrite(buzzerPin, HIGH);  // Accendi il buzzer
        delay(500);                     // Il buzzer suona per 500 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il buzzer
        delay(200);                     // Buzzer spento per 200 millisecondi
      }
    } else if (!isWorkPeriod) {
    }
  }

8. Usa dichiarazioni condizionali ``else if`` per determinare se è un periodo di pausa, e similmente verifica se il tempo attuale ha superato il ``breakPeriod``. In tal caso, reimposta il timer, passa nuovamente al periodo di lavoro e attiva il buzzer per suonare brevemente due volte.

.. code-block:: Arduino

  } else if (!isWorkPeriod) {
    if (currentMillis - startMillis >= breakPeriod) {
      startMillis = currentMillis;  // Reimposta il timer
      isWorkPeriod = true;          // Passa al periodo di lavoro
      digitalWrite(buzzerPin, HIGH);  // Accendi il buzzer
      delay(200);                     // Il buzzer suona per 200 millisecondi
      digitalWrite(buzzerPin, LOW);   // Spegni il buzzer
      delay(200);                     // Buzzer spento per 200 millisecondi
      digitalWrite(buzzerPin, HIGH);  // Accendi il buzzer
      delay(200);                     // Il buzzer suona per 200 millisecondi
      digitalWrite(buzzerPin, LOW);   // Spegni il buzzer
      delay(200);                     // Buzzer spento per 200 millisecondi
    }
  }


9. Il tuo codice completo dovrebbe apparire così, e puoi caricarlo su Arduino Uno R3 per vedere gli effetti.

.. note::

  Se durante il debug trovi che attendere 25 minuti per un periodo di lavoro e 5 minuti per una pausa sia troppo lungo, 
  puoi ridurre ``workPeriod`` a 15000 millisecondi e ``breakPeriod`` a 3000 millisecondi. In questo modo sentirai il cicalino emettere due suoni lunghi ogni 15 secondi, seguiti da due suoni brevi dopo 3 secondi.

.. code-block:: Arduino

  const int buzzerPin = 9;          // Assegna il pin 9 alla costante per il cicalino
  unsigned long startMillis;        // Memorizza il momento in cui inizia il timer
  const long workPeriod = 1500000;  // Periodo di lavoro di 25 minuti
  const long breakPeriod = 300000;  // Periodo di pausa di 5 minuti
  static bool isWorkPeriod = true;  // Tiene traccia se è un periodo di lavoro o di pausa

  void setup() {
    pinMode(buzzerPin, OUTPUT); // Inizializza il pin del cicalino come uscita
    startMillis = millis(); // Registra l'orario di inizio
  }

  void loop() {
    unsigned long currentMillis = millis(); // Aggiorna l'orario corrente

    if (isWorkPeriod){ 
      if(currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis; // Reimposta il timer
        isWorkPeriod = false; // Passa al periodo di pausa
        digitalWrite(buzzerPin, HIGH);  // Accendi il cicalino
        delay(500);                     // Il cicalino suona per 500 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il cicalino
        delay(200);                     // Cicalino spento per 200 millisecondi
        digitalWrite(buzzerPin, HIGH);  // Accendi il cicalino
        delay(500);                     // Il cicalino suona per 500 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il cicalino
        delay(200);                     // Cicalino spento per 200 millisecondi
      }
    } else if (!isWorkPeriod) 
      if(currentMillis - startMillis >= breakPeriod) {
        startMillis = currentMillis; // Reimposta il timer
        isWorkPeriod = true; // Passa al periodo di lavoro
        digitalWrite(buzzerPin, HIGH);  // Accendi il cicalino
        delay(200);                     // Il cicalino suona per 200 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il cicalino
        delay(200);                     // Cicalino spento per 200 millisecondi
        digitalWrite(buzzerPin, HIGH);  // Accendi il cicalino
        delay(200);                     // Il cicalino suona per 200 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il cicalino
        delay(200);                     // Cicalino spento per 200 millisecondi
      }
    }
  }

10. Infine, ricorda di salvare il tuo codice e mettere in ordine la tua postazione di lavoro.

**Domanda**

Pensa ad altri contesti della tua vita quotidiana in cui puoi "sentire" il passare del tempo. Elenca qualche esempio e scrivili nel tuo quaderno!

**Sommario**

Nella lezione di oggi, abbiamo costruito con successo una versione elettronica del Pomodoro Timer, uno strumento prezioso per migliorare la produttività attraverso periodi strutturati di lavoro e pausa. Attraverso questo progetto, gli studenti hanno appreso l'utilità dei cicalini nella gestione del tempo e l'applicazione pratica della funzione ``millis()`` per creare codice di timer non bloccante in Arduino. Questo approccio consente di eseguire più compiti contemporaneamente in applicazioni con microcontrollori, rispecchiando sistemi più complessi nella tecnologia e nell'industria.
