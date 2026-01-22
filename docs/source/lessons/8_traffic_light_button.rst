.. note::

    Ciao, benvenuto nella Community SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts su Facebook! Approfondisci Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti a noi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotti e anteprime.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a omaggi e promozioni festive.

    👉 Sei pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi stesso!


8. Semaforo con Pulsante Pedonale
===============================================

Benvenuto nella prossima fase del nostro percorso con Arduino. Nella lezione precedente, abbiamo costruito un sistema semaforico di base, che regola il traffico con le luci rosse, gialle e verdi. Ora aggiungiamo un livello di interazione che riflette la complessità del mondo reale: un pulsante pedonale. Questa funzione introduce un elemento umano nel nostro incrocio elettronico, permettendo un'interazione dinamica tra i pedoni e le strade trafficate.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/8_traffic_light_button.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In questa lezione imparerai a:

* Capire come funzionano i pulsanti e il loro ruolo nei circuiti.
* Utilizzare ``digitalRead()`` per rilevare i livelli di ingresso del pin.
* Implementare ``if`` statements per creare comportamenti condizionali nei sistemi semaforici.

Mentre ci immergiamo in questo progetto, esploreremo non solo l'assemblaggio tecnico, ma anche la logica e la programmazione che rendono possibili e efficienti tali sistemi nella gestione del traffico pedonale e veicolare.

Costruzione del Circuito
-----------------------------

**Componenti necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rosso
     - 1 * LED giallo
     - 1 * LED verde
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_yellow_led| 
     - |list_green_led| 
   * - 1 * Pulsante
     - 1 * Breadboard
     - 3 * Resistenze da 220Ω
     - 1 * Resistenza da 10KΩ
   * - |list_button| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Cavo USB
     - Cavi Jumper
     - 1 * Multimetro
     - 
   * - |list_usb_cable| 
     - |list_wire| 
     - |list_meter| 
     - 


**Costruzione passo-passo**

Segui il diagramma di collegamento o i passaggi qui sotto per costruire il tuo circuito.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center  

1. Inizia con il circuito semaforico della lezione precedente.

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

2. Trova un pulsante. 

.. image:: img/8_traffic_button.png
    :width: 500
    :align: center

I pulsanti sono componenti onnipresenti nell'elettronica, funzionando come interruttori per aprire o chiudere i circuiti. Di seguito è mostrata la struttura interna di un pulsante, insieme al suo simbolo comune utilizzato nei diagrammi dei circuiti.

.. image:: img/8_traffic_button_symbol.png
    :width: 500
    :align: center

Anche se i pulsanti hanno quattro pin, i pin 1 e 2 sono collegati tra loro, così come i pin 3 e 4. Premendo il pulsante, tutti e quattro i pin si connettono, chiudendo il circuito.

3. Inserisci il pulsante nel breadboard, attraversando il gap centrale, con i pin nei fori 18e, 18f, 20e e 20f.

.. note::

    Se non sei sicuro di come inserire il pulsante, prova entrambe le direzioni. In un modo, lo spazio tra i pin sarà leggermente troppo stretto per adattarsi.

.. image:: img/8_traffic_light_button_button.png
    :width: 600
    :align: center

4. Collega il pin in alto a destra del pulsante al pin digitale 8 dell'Arduino Uno R3 con un lungo cavo jumper, inserendo un'estremità nel foro 18j e l'altra nel pin 8.

.. image:: img/8_traffic_light_button_pin8.png
    :width: 600
    :align: center

5. Posiziona una resistenza da 10KΩ tra il pin in alto a sinistra del pulsante e il ground, collegando un'estremità al foro 18a e l'altra alla barra negativa del breadboard. Questa resistenza porta il pin 8 a terra, stabilizzandolo su LOW quando il pulsante non viene premuto.

    .. image:: img/8_traffic_light_button_10k.png
        :width: 600
        :align: center

Il pin 8 serve come ingresso per leggere lo stato del pulsante. Le schede Arduino leggono tensioni comprese tra 0 e circa 5 volt sui pin di ingresso, interpretandole come LOW o HIGH in base a una soglia di tensione. Perché un pin legga come HIGH, deve avere più di 3 volt. Per leggere come LOW, deve avere meno di 1,5 volt.

Senza la resistenza da 10K, il pin 8 collegato solo al pulsante fluttuerebbe tra 0 e 5V, causando una variazione casuale del suo stato tra HIGH e LOW.

La resistenza da 10K collegata dal pin 8 a terra abbassa la tensione del pin a livello di terra, assicurando che legga come LOW quando il pulsante non è premuto.

6. Infine, alimenta il pulsante collegando la barra positiva del breadboard al pin 5V dell'Arduino Uno R3 con un cavo di alimentazione rosso.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center


**Domanda:**

Il tuo semaforo è un mix di circuiti in serie e parallelo. Discuti quali parti del tuo circuito sono in serie e perché. Poi, spiega quali parti sono in parallelo e perché.


Creazione del Codice
----------------------------

**Inizializzazione dei Pin**

Finora hai programmato i semafori per far lampeggiare sequenzialmente i LED verde, giallo e rosso. In questa lezione, programmerai il pulsante pedonale in modo che, quando viene premuto, i LED rosso e giallo si spengano mentre il LED verde lampeggia, segnalando che è sicuro attraversare per i pedoni.

1. Apri lo sketch che hai salvato in precedenza, ``Lesson7_Traffic_Light``. Clicca su "Salva con nome..." dal menu "File", e rinominalo ``Lesson8_Traffic_Light_Button``. Clicca su "Salva".

2. Nella funzione ``void setup()``, aggiungi un altro comando ``pinMode()`` per dichiarare il pin 8 come input (``INPUT``). Poi, aggiungi un commento al codice per spiegare il nuovo comando.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Codice di configurazione, da eseguire una volta:
        pinMode(3, OUTPUT); // Imposta il pin 3 come output
        pinMode(4, OUTPUT); // Imposta il pin 4 come output
        pinMode(5, OUTPUT); // Imposta il pin 5 come output
        pinMode(8, INPUT);  // Dichiarare il pin 8 (pulsante) come input
    }
    
    void loop() {
        // Codice principale da eseguire ripetutamente:
        digitalWrite(3, HIGH);  // Accende il LED sul pin 3
        digitalWrite(4, LOW);   // Spegne il LED sul pin 4
        digitalWrite(5, LOW);   // Spegne il LED sul pin 5
        delay(10000);           // Attende 10 secondi
        digitalWrite(3, LOW);   // Spegne il LED sul pin 3
        digitalWrite(4, HIGH);  // Accende il LED sul pin 4
        digitalWrite(5, LOW);   // Spegne il LED sul pin 5
        delay(3000);            // Attende 3 secondi
        digitalWrite(3, LOW);   // Spegne il LED sul pin 3
        digitalWrite(4, LOW);   // Spegne il LED sul pin 4
        digitalWrite(5, HIGH);  // Accende il LED sul pin 5
        delay(10000);           // Attende 10 secondi
    }

3. Dopo aver scritto il codice, verifica il tuo sketch e carica il codice sull'Arduino Uno R3.

**Misurazione della Tensione sul Pin 8**

Sappiamo già come funziona la sezione dei LED nel nostro circuito dalla lezione precedente. Ogni LED, agendo come output, è controllato da diversi pin sull'Arduino Uno R3.

Tuttavia, il pulsante collegato al pin 8 è diverso. È un dispositivo di input. Il pin 8 leggerà la tensione in entrata anziché inviare tensione in uscita.

Usiamo un multimetro per testare la tensione sul pin 8 quando il pulsante è premuto e rilasciato. Potresti aver bisogno di un amico per premere il pulsante durante questa misurazione.

1. Imposta il multimetro sulla modalità DC a 20 volt.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Quando il pulsante non è premuto, misura la tensione sul pin 8. Tocca il puntale rosso del multimetro sul pin 8 e il puntale nero su GND.

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

3. Registra la tensione misurata nella tabella.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Stato del Pulsante
     - Tensione Pin 8
     - Stato
   * - Rilasciato
     - *0,00 volt*
     - 
   * - Premuto
     - 
     - 

4. Fatti aiutare da un amico a premere il pulsante, quindi continua a misurare la tensione sul pin 8.

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

5. Quando il pulsante è premuto, registra la tensione sul pin 8 nella tabella.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Stato del Pulsante
     - Tensione Pin 8
     - Stato
   * - Rilasciato
     - *0,00 volt*
     - 
   * - Premuto
     - *≈4,97 volt*
     - 

6. Le schede Arduino leggono tensioni comprese tra 0 e circa 5 volt sui pin di ingresso, interpretandole come ``LOW`` o ``HIGH`` in base a una soglia di tensione. Perché un pin legga come ``HIGH``, deve avere più di 3 volt. Per leggere come ``LOW``, deve avere meno di 1,5 volt.

   In base alla tensione misurata, compila lo stato del pin 8.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Stato del Pulsante
     - Tensione Pin 8
     - Stato Pin 8
   * - Rilasciato
     - *0,00 volt*
     - *LOW*
   * - Premuto
     - *≈4,97 volt*
     - *HIGH*


**Istruzioni Condizionali**

Il semaforo dovrebbe mostrare due comportamenti diversi a seconda che il pulsante venga premuto:

* Quando il pulsante viene premuto, il codice per l'attraversamento pedonale deve essere eseguito, e il LED verde deve lampeggiare.
* Quando il pulsante non viene premuto, il semaforo deve funzionare normalmente come già programmato.

Per programmare questi comportamenti, userai una nuova funzione di codifica nota come istruzioni condizionali.

Le istruzioni condizionali sono talvolta chiamate istruzioni ``if-then``, o semplicemente un'istruzione ``if``.
Le istruzioni condizionali ti permettono di eseguire alcune righe di codice quando una specifica condizione o scenario è vero.


.. image:: img/if.png
    :width: 300
    :align: center


.. note::

    Usi spesso le istruzioni condizionali nella vita quotidiana per prendere decisioni, come ad esempio:

    .. code-block:: Arduino

        start;
        if cold;
        then wear a coat;
        end;
        
Nell'IDE di Arduino, un'istruzione condizionale appare così:

    .. code-block:: Arduino

        if (condition) {
            commands to run when the condition is true 
        }

La ``condizione`` si trova tra parentesi tonde, utilizzando operatori di confronto per confrontare due o più valori. Questi valori possono essere numeri, variabili o input che arrivano nell'Arduino Uno R3.

Ecco un elenco di operatori di confronto e come vengono utilizzati nella parte della condizione di un'istruzione if:

.. list-table::
    :widths: 20 20 60
    :header-rows: 1

    *   - Comparison Operator
        - Meaning
        - Example
    *   - ==
        - Equals
        - if (digitalRead(8) == HIGH) {do something}
    *   - !=
        - Not equal
        - if (digitalRead(5) != LOW) {do something}
    *   - <
        - Less than
        - if (distance < 100) {do something}
    *   - >
        - Greater than
        - if (count > 5) {do something}
    *   - <=
        - Less than or equal to
        - if (number <= minValue) {do something}
    *   - >=
        - Greater than or equal to
        - if (number >= maxValue) {do something}

.. note::

    Il confronto di uguaglianza utilizza due segni di uguale (``==``). Un singolo segno di uguale (``=``) viene utilizzato per assegnare un valore a una variabile (spiegato nelle sezioni successive), mentre il doppio uguale serve per confrontare due valori.

Quando si confrontano due valori in una condizione, il risultato può essere ``True`` o ``False``. Se la condizione è ``True``, allora i comandi all'interno delle parentesi graffe vengono eseguiti. Se la condizione è ``False``, i comandi all'interno delle parentesi graffe vengono ignorati.

Nella programmazione, le istruzioni condizionali possono essere semplici o coinvolgere argomentazioni logiche complesse con più condizioni e scenari. Userai la forma base delle istruzioni ``if`` nel prossimo passaggio.

**Pulsante non Premuto**

Sfruttando la nostra comprensione delle istruzioni condizionali, applichiamo questo concetto per migliorare il nostro sketch del semaforo. Poiché la pressione di un pulsante altera il flusso del traffico, incorporeremo una condizione per monitorare lo stato del pulsante.

1. Dai nostri precedenti rilevamenti della tensione sul pin 8, sappiamo che quando il pulsante non è premuto, il pin 8 è su ``LOW``. Quindi, se lo stato letto dal pin 8 è ``LOW``, significa che non è premuto. Ora, all'inizio della funzione ``void loop()`` nel tuo codice precedente, inserisci la seguente istruzione:

    .. code-block:: Arduino
        :emphasize-lines: 11,13

        void setup() {
            // Codice di configurazione, da eseguire una volta:
            pinMode(3, OUTPUT); // Imposta il pin 3 come output
            pinMode(4, OUTPUT); // Imposta il pin 4 come output
            pinMode(5, OUTPUT); // Imposta il pin 5 come output
            pinMode(8, INPUT);  // Dichiarare il pin 8 (pulsante) come input
        }

        void loop() {
            // Codice principale da eseguire ripetutamente:
            if (digitalRead(8) == LOW) {
                
            }

            digitalWrite(3, HIGH);  // Accendi il LED sul pin 3
            digitalWrite(4, LOW);   // Spegni il LED sul pin 4
            digitalWrite(5, LOW);   // Spegni il LED sul pin 5

            ...

Proprio come il comando ``digitalWrite()`` viene usato per i pin di output, il comando ``digitalRead()`` viene usato per i pin di input. ``digitalRead(pin)`` è il comando per leggere se un pin digitale è su ``HIGH`` o ``LOW``.

Ecco la sua sintassi:

    * ``digitalRead(pin)``: Legge il valore da un pin digitale specificato, che può essere ``HIGH`` o ``LOW``.

        **Parametri**
            - ``pin``: il numero del pin dell'Arduino che vuoi leggere
        
        **Restituisce**
            ``HIGH`` o ``LOW``

**Inizializzazione dei Pin**

Finora, hai programmato il semaforo affinché lampeggi sequenzialmente con i LED verde, giallo e rosso. In questa lezione, programmerai il pulsante pedonale in modo che, quando viene premuto, i LED rosso e giallo si spengano mentre il LED verde lampeggia, indicando che è sicuro attraversare.

1. Apri lo sketch salvato in precedenza, ``Lesson7_Traffic_Light``. Clicca su "Salva con nome..." dal menu "File" e rinominalo ``Lesson8_Traffic_Light_Button``. Clicca su "Salva".

2. Nella funzione ``void setup()``, aggiungi un altro comando ``pinMode()`` per dichiarare il pin 8 come input (``INPUT``). Poi, aggiungi un commento per spiegare il nuovo comando.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Codice di configurazione da eseguire una volta:
        pinMode(3, OUTPUT); // Imposta il pin 3 come output
        pinMode(4, OUTPUT); // Imposta il pin 4 come output
        pinMode(5, OUTPUT); // Imposta il pin 5 come output
        pinMode(8, INPUT);  // Dichiarare il pin 8 (pulsante) come input
    }
    
    void loop() {
        // Codice principale da eseguire ripetutamente:
        digitalWrite(3, HIGH);  // Accendi il LED sul pin 3
        digitalWrite(4, LOW);   // Spegni il LED sul pin 4
        digitalWrite(5, LOW);   // Spegni il LED sul pin 5
        delay(10000);           // Attendi 10 secondi
        digitalWrite(3, LOW);   // Spegni il LED sul pin 3
        digitalWrite(4, HIGH);  // Accendi il LED sul pin 4
        digitalWrite(5, LOW);   // Spegni il LED sul pin 5
        delay(3000);            // Attendi 3 secondi
        digitalWrite(3, LOW);   // Spegni il LED sul pin 3
        digitalWrite(4, LOW);   // Spegni il LED sul pin 4
        digitalWrite(5, HIGH);  // Accendi il LED sul pin 5
        delay(10000);           // Attendi 10 secondi
    }

Nota come i comandi all'interno dell'istruzione ``if`` siano rientrati. L'uso dell'indentazione aiuta a mantenere il codice ordinato e chiarisce i comandi che vengono eseguiti all'interno di una funzione. Anche se può richiedere qualche secondo in più, utilizzare l'indentazione, i salti di riga e i commenti al codice può migliorare l'estetica del tuo codice, il che sarà vantaggioso a lungo termine.

Un errore di sintassi comune è dimenticare il numero corretto di parentesi graffe. A volte, la parentesi destra manca in una funzione, oppure vengono aggiunte troppe parentesi destra. Nel tuo sketch, ogni parentesi sinistra deve avere una parentesi destra corrispondente. Una corretta indentazione aiuta anche a risolvere eventuali problemi di parentesi non corrispondenti.


**Quando il pulsante è premuto**

Ora è il momento di scrivere il codice che consente ai pedoni di attraversare la strada quando il pulsante viene premuto.

Questo richiederà una seconda istruzione condizionale. Tuttavia, questa volta dovrai confrontare il valore di ``digitalRead()`` del pin 8 con ``HIGH`` invece di ``LOW``.

Quando il pulsante è premuto, il semaforo deve fermare tutti i veicoli e segnalare che è sicuro per i pedoni attraversare. Per farlo, spegnerai i LED rosso e giallo e farai lampeggiare il LED verde. All'interno delle parentesi graffe della tua seconda istruzione condizionale, aggiungi tre comandi ``digitalWrite()``:

* Accendi il LED verde collegato al pin 3.
* Spegni il LED giallo collegato al pin 4.
* Spegni il LED rosso collegato al pin 5.

Poi, fai lampeggiare il LED verde. Ricorda, la frequenza del lampeggio è determinata dalle tue istruzioni ``delay()``.

Il tuo sketch dovrebbe apparire così:


.. code-block:: Arduino
    :emphasize-lines: 24-31

    void setup() {
        pinMode(3, OUTPUT);  // dichiara il pin 3 (LED verde) come output
        pinMode(4, OUTPUT);  // dichiara il pin 4 (LED giallo) come output
        pinMode(5, OUTPUT);  // dichiara il pin 5 (LED rosso) come output
        pinMode(8, INPUT);   // dichiara il pin 8 (pulsante) come input
    }

    void loop() {
        // Codice principale da eseguire ripetutamente:
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // Accendi il LED sul pin 3
            digitalWrite(4, LOW);   // Spegni il LED sul pin 4
            digitalWrite(5, LOW);   // Spegni il LED sul pin 5
            delay(10000);           // Attendi 10 secondi
            digitalWrite(3, LOW);   // Spegni il LED sul pin 3
            digitalWrite(4, HIGH);  // Accendi il LED sul pin 4
            digitalWrite(5, LOW);   // Spegni il LED sul pin 5
            delay(3000);            // Attendi 3 secondi
            digitalWrite(3, LOW);   // Spegni il LED sul pin 3
            digitalWrite(4, LOW);   // Spegni il LED sul pin 4
            digitalWrite(5, HIGH);  // Accendi il LED sul pin 5
            delay(10000);           // Attendi 10 secondi
        }
        if (digitalRead(8) == HIGH) {  //se il pulsante è premuto:
            digitalWrite(3, HIGH);       // Accendi il LED sul pin 3
            digitalWrite(4, LOW);        // Spegni il LED sul pin 4
            digitalWrite(5, LOW);        // Spegni il LED sul pin 5
            delay(500);                  // Attendi mezzo secondo
            digitalWrite(3, LOW);        // Spegni il LED sul pin 3
            delay(500);                  // Attendi mezzo secondo
        }
    }

Carica il tuo codice sull'Arduino Uno R3. Una volta che lo sketch è stato completamente trasferito, il codice verrà eseguito.

Osserva il comportamento del tuo semaforo. Premi il pulsante e aspetta che il semaforo completi il suo ciclo. Il LED verde lampeggia? Quando il pulsante viene rilasciato, il semaforo torna alla sua normale modalità operativa? In caso contrario, apporta le modifiche necessarie al tuo sketch e ricaricalo sull'R3.

Una volta completato, salva il tuo sketch.

**Domanda**

Durante i test, potresti notare che il LED verde lampeggia solo mentre il pulsante pedonale viene mantenuto premuto, ma i pedoni non possono attraversare la strada continuando a premere il pulsante. Come puoi modificare il codice per garantire che, una volta premuto il pulsante pedonale, il LED verde rimanga acceso abbastanza a lungo per permettere un attraversamento sicuro senza dover tenere premuto continuamente il pulsante? Scrivi la soluzione in pseudo-codice nel tuo quaderno.

**Riepilogo**

In questa lezione, abbiamo integrato un pulsante pedonale nel sistema del semaforo, simulando uno scenario reale che bilancia il flusso di traffico pedonale e veicolare. Abbiamo esplorato il funzionamento di un pulsante in un circuito elettronico e utilizzato la funzione ``digitalRead()`` per monitorare l'input dal pulsante. Implementando istruzioni condizionali con strutture ``if``, abbiamo programmato i semafori per rispondere dinamicamente agli input pedonali, migliorando la nostra comprensione dei sistemi interattivi. Questa lezione ha rafforzato le nostre competenze nella programmazione con Arduino e ha evidenziato l'applicazione pratica di queste tecnologie nella gestione efficiente delle situazioni quotidiane.
