.. note::

    Ciao, benvenuto nella community di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperti**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

6. Blink LED
======================
Benvenuto in questa lezione, imparerai a manipolare i pin digitali dell'Arduino Uno R3 per controllare un LED in modo programmabile—accendendolo e spegnendolo senza intervento manuale, una competenza fondamentale per applicazioni elettroniche sia domestiche che industriali.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/6_blink_led.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In questa lezione, imparerai a:

* Creare e salvare sketch utilizzando l'Arduino IDE.
* Utilizzare le funzioni ``pinMode()`` e ``digitalWrite()`` per controllare gli elementi del circuito.
* Caricare sketch su Arduino Uno R3 e comprendere i loro effetti in tempo reale.
* Implementare ``delay()`` negli sketch per gestire i comportamenti del circuito.

Al termine di questa lezione, sarai in grado di costruire un circuito che non solo illumina un LED, ma lo fa lampeggiare a intervalli da te impostati, fornendoti una comprensione di base di come il software interagisce con l'hardware.

Costruzione del Circuito
-------------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED Rosso
     - 1 * Resistenza 220Ω
     - Fili di Collegamento
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

**Passaggi di Costruzione**

Prendi il circuito costruito nella sezione :ref:`2_first_circuit` e sposta il filo dal pin 5V al pin 3, come mostrato nell'immagine qui sotto.

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center

Se hai smontato il circuito precedente, puoi ricostruirlo seguendo questi passaggi:

1. Collega la resistenza da 220 ohm alla breadboard. Un filo deve essere collegato al terminale negativo e l'altro al foro 1B.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Aggiungi un LED rosso alla breadboard. L'anodo del LED (la gamba più lunga) deve essere inserito nel foro 1F. Il catodo (la gamba più corta) deve essere nel foro 1E. A volte può essere difficile distinguere l'anodo dal catodo osservando solo la lunghezza delle gambe. Ricorda che il lato catodo del LED ha anche un bordo piatto sulla lente colorata, mentre l'anodo ha un bordo arrotondato.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Utilizza un filo di collegamento corto per connettere il LED e la sorgente di alimentazione. Un'estremità del filo deve essere nel foro 1J e l'altra nel terminale positivo.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Collega il terminale positivo della breadboard al pin 3 dell'Arduino Uno R3.

.. image:: img/6_led_circuit_3.png
    :width: 600
    :align: center

5. Collega il terminale negativo della breadboard a uno dei pin GND dell'Arduino Uno R3. I pin GND sono indicati come "GND".

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center

Dare vita al LED
-----------------------------

Perfetto, è ora di accendere il LED! Invece di utilizzare l'esempio Blink predefinito di Arduino come abbiamo fatto in precedenza, questa volta inizieremo da zero e creeremo uno sketch nuovo di zecca. Cominciamo subito!

**1. Creare e Salvare uno Sketch**

1. Avvia l'Arduino IDE. Vai al menu “File” e clicca su “Nuovo Sketch” per iniziare da capo. Puoi chiudere eventuali altre finestre di sketch aperte.

    .. image:: img/6_blink_ide_new.png
        :align: center

2. Organizza la finestra dell'Arduino IDE affiancandola a questo tutorial online, in modo da poter vedere entrambi contemporaneamente. Potrebbe sembrare tutto un po' piccolo, ma è meglio che passare da una finestra all'altra.

    .. image:: img/6_blink_ide_tutorials.png

3. È ora di salvare il tuo sketch. Clicca su “Salva” dal menu “File” oppure premi ``Ctrl + S``.

    .. image:: img/6_blink_ide_save.png

4. Puoi salvare lo sketch nella posizione predefinita o in un'altra. Dai un nome significativo al tuo sketch, come ``Lezione6_Accendere_LED``, e clicca su “Salva”.

    * Dai un nome al tuo sketch che rifletta la sua funzione per trovarlo facilmente in futuro.
    * I nomi degli sketch di Arduino non possono contenere spazi.
    * Quando apporti modifiche significative, considera di salvare una nuova versione (ad es., V1) per mantenere un backup.

    .. image:: img/6_blink_ide_name.png

5. Il tuo nuovo sketch è composto da due parti principali, ``void setup()`` e ``void loop()``, che sono funzioni utilizzate in tutti gli sketch di Arduino.

    * ``void setup()`` viene eseguito una volta quando il programma inizia, impostando le condizioni iniziali.
    * ``void loop()`` viene eseguito ripetutamente, eseguendo azioni continue.
    * Inserisci i comandi per ciascuna funzione all'interno delle parentesi graffe ``{}``.
    * Ogni riga che inizia con ``//`` è un commento. Questi sono per le tue note e non influenzeranno l'esecuzione del codice.

    .. code-block:: Arduino

        void setup() {
        // Codice di setup, eseguito una volta:

        }

        void loop() {
        // Inserisci qui il tuo codice principale, eseguito ripetutamente:

        }

**2. Selezione della Scheda e della Porta**

1. Collega il tuo Arduino Uno R3 al computer con un cavo USB. Vedrai accendersi la spia di alimentazione sull'Arduino.

    .. image:: img/1_connect_uno_pc.jpg
        :width: 600
        :align: center

2. Fai sapere all'IDE che stiamo utilizzando un **Arduino Uno**. Vai su **Strumenti** -> **Scheda** -> **Arduino AVR Boards** -> **Arduino Uno**.

    .. image:: img/6_blink_ide_board.png
        :width: 600
        :align: center

3. Successivamente, nell'IDE di Arduino, seleziona la porta a cui è collegato il tuo Arduino.

    .. note::

        * Una volta selezionata una porta, l'IDE di Arduino dovrebbe ricordarla ogni volta che l'Arduino viene collegato tramite USB.
        * Se viene collegata una scheda Arduino diversa, potrebbe essere necessario scegliere una nuova porta.
        * Controlla sempre prima la porta se ci sono problemi di connessione.

    .. image:: img/6_blink_ide_port.png
        :width: 600
        :align: center

**3. Scrivere il Codice**

1. Nel nostro progetto, utilizziamo il pin digitale 3 della scheda per controllare un LED. Ogni pin può funzionare sia come uscita, inviando 5 volt, che come ingresso, leggendo la tensione in entrata. Per configurare il LED, impostiamo il pin come uscita utilizzando la funzione ``pinMode(pin, mode)``.

    Vediamo la sintassi di ``pinMode()``.

    * ``pinMode(pin, mode)``: Imposta un pin specifico su ``INPUT`` o ``OUTPUT``.

    **Parametri**
        - ``pin``: il numero del pin di cui vuoi impostare la modalità.
        - ``mode``: ``INPUT``, ``OUTPUT`` o ``INPUT_PULLUP``.

    **Restituisce**
        Nulla

2. Ora, è il momento di aggiungere la nostra prima riga di codice nella funzione ``void setup()``.

    .. note::

        - La programmazione in Arduino è case-sensitive. Assicurati di scrivere le funzioni esattamente come sono.
        - Nota che il comando termina con un punto e virgola. Nell'IDE di Arduino, ogni comando deve terminare con uno.
        - I commenti nel codice sono utili per ricordarti cosa fa una riga o una sezione di codice.

    .. code-block:: Arduino
        :emphasize-lines: 3

        void setup() {
            // Codice di setup, eseguito una volta:
            pinMode(3,OUTPUT); // imposta il pin 3 come uscita
        }

        void loop() {
        // Inserisci qui il tuo codice principale, eseguito ripetutamente:

        }

**4. Verifica del Codice**

Prima di attivare il nostro semaforo, verificheremo il codice. Questo processo controlla se l'IDE di Arduino può comprendere e compilare i tuoi comandi in linguaggio macchina.

1. Per verificare il tuo codice, clicca sul pulsante con il **segno di spunta** nell'angolo in alto a sinistra della finestra.

    .. image:: img/6_blink_ide_verify.png
        :width: 600
        :align: center

2. Se il codice è leggibile dalla macchina, un messaggio in basso indicherà che il codice è stato compilato correttamente. Questa sezione mostra anche quanto spazio di archiviazione utilizza il tuo programma.

    .. image:: img/6_blink_ide_verify_done.png
        :width: 600
        :align: center

3. Se c'è un errore nel codice, vedrai un messaggio di errore arancione. L'IDE solitamente evidenzia dove si trova l'errore, di solito vicino alla riga evidenziata. Ad esempio, un errore di punto e virgola mancante evidenzierà la riga successiva all'errore.

    .. image:: img/6_blink_ide_verify_error.png
        :width: 600
        :align: center

4. Quando incontri errori, è il momento di fare debug, ossia trovare e correggere gli errori nel codice. Controlla problemi comuni come:

    - Il ``M`` in ``pinMode`` è maiuscolo?
    - Hai scritto ``OUTPUT`` tutto in maiuscolo?
    - Hai usato sia parentesi aperte che chiuse nella funzione ``pinMode``?
    - Hai terminato la funzione ``pinMode`` con un punto e virgola?
    - Hai controllato l'ortografia? Se trovi errori, correggili e verifica di nuovo il codice. Continua a fare debug finché lo sketch non è privo di errori.

L'IDE di Arduino si ferma alla prima segnalazione di errore, quindi potresti dover verificare più volte per correggere più errori. Verificare il codice regolarmente è una buona pratica.

Il debugging è una parte importante della programmazione. I programmatori professionisti spesso trascorrono più tempo a correggere errori che a scrivere nuovo codice. Gli errori sono normali, quindi non scoraggiarti. Diventare un buon risolutore di problemi è la chiave per diventare un ottimo programmatore.

**5. Continuare a Scrivere lo Sketch**

1. Ora sei pronto per iniziare la funzione ``void loop()``. Questo è il punto in cui avviene l'azione principale del tuo sketch o programma. Per accendere il LED collegato all'Arduino Uno R3, dovremo fornire tensione al circuito utilizzando ``digitalWrite()``.

    * ``digitalWrite(pin, value)``: Invia un segnale ``HIGH`` (5V) o ``LOW`` (0V) a un pin digitale, cambiando lo stato operativo del componente.

    **Parametri**
        - ``pin``: il numero del pin dell'Arduino.
        - ``value``: ``HIGH`` o ``LOW``.

    **Restituisce**
        Nulla

5. Sotto il commento nella funzione ``void loop()``, scrivi un comando per accendere il LED collegato al pin 3. Non dimenticare di terminare il comando con un punto e virgola. Verifica e correggi il codice se necessario.

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Codice di setup, eseguito una volta:
            pinMode(3, OUTPUT);  // imposta il pin 3 come uscita
        }

        void loop() {
            // Inserisci qui il tuo codice principale, eseguito ripetutamente:
            digitalWrite(3, HIGH);
        }

6. Dopo il comando ``digitalWrite()``, aggiungi un commento nel codice che spieghi cosa fa questa riga. Ad esempio:

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Codice di setup, eseguito una volta: 
            pinMode(3, OUTPUT);  // imposta il pin 3 come uscita
        }

        void loop() {
            // Inserisci qui il tuo codice principale, eseguito ripetutamente:
            digitalWrite(3, HIGH);  // Accende il LED sul pin 3
        }


**6. Caricare il Codice**

Con il codice privo di errori e verificato, è ora di caricarlo sull'Arduino Uno R3 e vedere il tuo semaforo prendere vita.

1. Nell'IDE, clicca sul pulsante “Upload”. Il computer compilerà il codice e poi lo trasferirà sull'Arduino Uno R3. Durante il trasferimento, dovresti vedere alcune luci lampeggiare sulla scheda, indicando la comunicazione con il computer.

.. image:: img/6_blink_ide_upload.png
    :width: 600
    :align: center

2. Un messaggio di “Done Uploading” significa che il codice non ha problemi e che hai selezionato la scheda e la porta corrette.

.. image:: img/6_blink_ide_upload_done.png
    :width: 600
    :align: center


3. Una volta completato il trasferimento, il codice verrà eseguito e dovresti vedere il LED sulla breadboard accendersi.

**7. Misurare la Tensione sull'LED**

Utilizziamo un multimetro per misurare la tensione al pin 3 e comprendere cosa significa effettivamente lo stato ``HIGH`` nel codice.

1. Imposta il multimetro sulla modalità 20 volt DC.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Inizia misurando la tensione al Pin 3. Tocca il puntale rosso del multimetro al Pin 3 e il puntale nero al GND.

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

3. Registra la tensione misurata nella tabella per il Pin 3 sotto la riga etichettata "HIGH".

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - Stato
     - Tensione Pin 3
   * - HIGH
     - *≈4.95 volt*
   * - LOW
     -


4. Dopo aver effettuato la misurazione, ricorda di spegnere il multimetro impostandolo su "OFF".

Le nostre misurazioni rivelano che la tensione su tutti e tre i pin è vicina a 5V. Questo indica che impostare un pin su ``HIGH`` nel codice significa che la tensione di uscita su quel pin è vicina a 5V.

La tensione dei pin dell'R3 è di 5V, quindi impostandola su ``HIGH`` si raggiunge quasi 5V. Tuttavia, alcune schede funzionano a 3.3V, il che significa che il loro stato ``HIGH`` sarebbe vicino a 3.3V.

Far Lampeggiare il LED
------------------------------
Ora che il tuo LED è acceso, è il momento di farlo lampeggiare.

1. Apri lo sketch che hai salvato in precedenza, ``Lesson6_Light_up_LED``. Clicca su “Salva con nome...” dal menu “File” e rinominalo in ``Lesson6_Blink_LED``. Clicca su "Salva".

2. Nella funzione ``void loop()`` del tuo sketch, copia i comandi ``digitalWrite()`` e incollali dopo gli originali. Per far lampeggiare il LED, dopo averlo acceso, imposta il suo stato su ``LOW`` per spegnerlo.

    .. note::
       * Copiare e incollare può essere il miglior alleato di un programmatore. Replica una sezione di codice pulita in una nuova posizione e modifica i suoi parametri per un'esecuzione rapida e pulita.
       * Ricorda di aggiornare i commenti per adattarli meglio all'azione eseguita.
       * Usa ``Ctrl+T`` per formattare il tuo codice ordinatamente con un clic, rendendolo più leggibile e organizzato.

    .. code-block:: Arduino
       :emphasize-lines: 8,9

       void setup() {
            // Codice di setup, eseguito una volta:
            pinMode(3, OUTPUT);  // imposta il pin 3 come uscita
       }

       void loop() {
            // Codice principale, eseguito ripetutamente:
            digitalWrite(3, HIGH);  // Accendi il LED sul pin 3   
            digitalWrite(3, LOW);  // Spegni il LED sul pin 3
       }

3. Premi il pulsante “Carica” per trasferire lo sketch sull'Arduino Uno R3. Dopo il trasferimento, potresti notare che il LED non lampeggia, o che lampeggia così velocemente che è impercettibile.

4. Per osservare visivamente il lampeggio, puoi utilizzare il comando ``delay()`` per far attendere l'Arduino Uno R3 per una durata specificata, espressa in millisecondi.

    * ``delay(ms)``: Ferma l'esecuzione del programma per il tempo specificato (in millisecondi). (Ci sono 1000 millisecondi in un secondo.)

    **Parametri**
        - ``ms``: il numero di millisecondi di attesa. Tipi di dati accettati: unsigned long.

    **Restituisce**
        Nulla

5. Ora, inserisci il comando ``delay(time)`` dopo ogni serie di comandi di accensione e spegnimento, impostando il tempo di attesa a 3000 millisecondi (3 secondi). Puoi modificare questa durata per far lampeggiare il LED più velocemente o più lentamente.

    .. note::

        Durante questa pausa, l'Arduino Uno R3 non può eseguire altre operazioni fino al termine del delay.
        
    .. code-block:: Arduino
       :emphasize-lines: 10,11

       void setup() {
            // Codice di setup, eseguito una volta:
            pinMode(3, OUTPUT);  // imposta il pin 3 come uscita
       }

       void loop() {
            // Codice principale, eseguito ripetutamente:
            digitalWrite(3, HIGH);  // Accendi il LED sul pin 3
            delay(3000); // Attendi 3 secondi   
            digitalWrite(3, LOW);  // Spegni il LED sul pin 3
            delay(3000); // Attendi 3 secondi
       }

6. Carica il tuo sketch sull'Arduino Uno R3. Dopo il caricamento, il tuo LED dovrebbe lampeggiare con un intervallo di 3 secondi.

7. Verifica che tutto funzioni correttamente, quindi salva lo sketch.

8. Utilizziamo un multimetro per misurare la tensione su tre pin e capire cosa significa effettivamente lo stato ``LOW`` nel codice. Imposta il multimetro su 20 volt in modalità DC.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

9. Inizia misurando la tensione al Pin 3. Tocca il puntale rosso del multimetro al Pin 3 e il puntale nero al GND.

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

10. Con tutti i LED spenti, registra la tensione misurata per il Pin 3 nella riga "LOW" della tua tabella.

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - Stato
     - Tensione Pin 3 
   * - HIGH
     - *≈4.95 volt*
   * - LOW
     - *0.00 volt*

Le nostre misurazioni mostrano che, quando i LED sono spenti, la tensione al Pin 3 scende a 0V. Questo dimostra che nel nostro codice, impostare un pin su "LOW" riduce efficacemente la tensione di uscita su quel pin a 0V, spegnendo il LED collegato. Questo principio ci permette di controllare gli stati di accensione e spegnimento dei LED con un timing preciso, simulando il funzionamento di un semaforo.

**Domanda**

Carica il codice sopra, e noterai che il LED lampeggia ripetutamente con un intervallo di 3 secondi. Se volessi che si accendesse e spegnesse una sola volta, cosa dovresti fare?

**Riepilogo**

Congratulazioni per aver completato questa lezione, in cui hai programmato con successo un LED per farlo lampeggiare utilizzando l'Arduino Uno R3. Questa lezione è stata un'introduzione alla scrittura e al caricamento di sketch per Arduino, all'impostazione delle modalità dei pin e alla manipolazione delle uscite per ottenere risposte elettriche desiderate. Costruendo il circuito e programmando l'Arduino Uno R3, hai acquisito preziose conoscenze sull'interazione tra comandi software e comportamenti dell'hardware fisico.

La tua capacità di controllare un LED è solo l'inizio: immagina cosa potrai fare ampliando queste basi! 
