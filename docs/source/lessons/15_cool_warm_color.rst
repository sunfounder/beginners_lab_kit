.. note::

    Ciao, benvenuto nella community di SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts su Facebook! Approfondisci Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato a nuove presentazioni di prodotti e anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Omaggi Festivi**: Partecipa a promozioni e omaggi durante le festività.

    👉 Sei pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

15. Colori Caldi o Freddi
============================

I colori non fanno solo parte della nostra esperienza visiva, influenzano anche le nostre emozioni e sensazioni. In questa lezione esploreremo gli impatti psicologici dei colori e impareremo a manipolare un LED RGB per passare tra colori caldi e freddi, imitando gli effetti delle variazioni di temperatura della luce.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/15_cool_warm_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

**Panoramica**

Il concetto di colori caldi e freddi si riferisce agli effetti psicologici che i colori hanno sulla nostra percezione. Rossi, arancioni, gialli e marroni evocano solitamente sensazioni di calore e vitalità, classificandoli come colori caldi. Al contrario, verdi, blu e viola spesso trasmettono sensazioni di calma e freschezza, rendendoli colori freddi. Arancione e blu si trovano agli estremi opposti di questo spettro caldo-freddo.

.. image:: img/15_mix_color_warm_cool.png
    :width: 400
    :align: center

A casa o in ambienti di svago, le persone preferiscono luci in tonalità di giallo chiaro o bianco caldo, creando un'atmosfera accogliente, simile a quella di un tramonto o della luce di una candela.

.. image:: img/15_mix_color_warm_room.png
    :width: 400
    :align: center

In biblioteche, aule, uffici e ospedali, sono invece preferite tonalità di luce più fredde, in quanto favoriscono la concentrazione e una sensazione di freschezza, condizioni ideali per lavorare e studiare.

.. image:: img/15_mix_color_cool_room.png
    :width: 400
    :align: center

La sensazione di calore o freschezza della luce è un'esperienza viscerale che influisce sulla nostra risposta psicologica e sul comfort visivo. I progettisti e gli ingegneri dell'illuminazione selezionano attentamente le temperature di colore adatte alla funzione di uno spazio e all'atmosfera desiderata, creando ambienti di illuminazione esteticamente gradevoli e funzionali. Applicando scientificamente questi principi, possiamo migliorare la qualità dei nostri ambienti abitativi e di lavoro, creando atmosfere più sane e confortevoli.

In questa lezione, assumeremo il ruolo di ingegneri dell'illuminazione per creare un sistema di illuminazione che possa passare tra diverse temperature di colore.

**Obiettivi di Apprendimento**

- Comprendere gli effetti psicologici dei colori caldi e freddi.
- Esplorare come le temperature della luce influenzano l'umore e l'ambiente.
- Imparare a regolare i colori di un LED RGB per simulare diverse temperature con Arduino.
- Sviluppare competenze pratiche nell'uso della funzione ``map()`` per passare tra le temperature di colore.


Costruzione del Circuito
------------------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Resistenze da 220Ω
     - 1 * Potenziometro
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Cavo USB
     - 1 * Breadboard
     - Fili di Collegamento
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - 
     
**Fasi di Costruzione**

Questo circuito si basa su quello della Lezione 12 con l'aggiunta di un potenziometro.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center

1. Rimuovi il filo jumper che collega il pin GND dell'Arduino Uno R3 al pin GND del LED RGB, quindi inseriscilo nel terminale negativo della breadboard. Poi, collega un filo jumper dal terminale negativo al pin GND del LED RGB.

.. image:: img/15_cool_warm_color_gnd.png
    :width: 500
    :align: center

2. Inserisci il potenziometro nei fori 25G, 26F e 27G.

.. image:: img/15_cool_warm_color_pot.png
    :width: 500
    :align: center

3. Collega il pin centrale del potenziometro al pin A0 dell'Arduino Uno R3.

.. image:: img/15_cool_warm_color_a0.png
    :width: 500
    :align: center

4. Infine, collega il pin sinistro del potenziometro al pin 5V dell'Arduino Uno R3 e il pin destro al terminale negativo della breadboard.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center


Creazione del Codice
-------------------------

**Comprendere i Colori Caldi e Freddi**

Prima di regolare la temperatura del colore, dobbiamo comprendere le differenze tra i valori RGB per i colori freddi e caldi.

La percezione del calore nella luce è in parte soggettiva, ma i colori caldi devono tendere verso l'arancio-rosso, mentre i colori freddi devono tendere verso il blu.

1. Apri **Paint** o un qualsiasi strumento di selezione colori, trova quelli che consideri i colori più caldi e freddi, e registra i loro valori RGB nel tuo quaderno.


.. note::

    Nota che, prima di selezionare un colore, devi regolare i lumen nella posizione corretta.

.. list-table::
   :widths: 25 25 50 25
   :header-rows: 1

   * - Tipo di Colore
     - Rosso
     - Verde
     - Blu
   * - Colore Caldo
     - 
     - 
     - 
   * - Colore Freddo
     - 
     - 
     - 

2. Ecco alcuni esempi di tonalità calde e fredde con i relativi valori RGB:

* Rosso (Rosso: 246, Verde: 52, Blu: 8)

.. image:: img/15_mix_color_tone_warm.png

* Azzurro Chiaro (Rosso: 100, Verde: 150, Blu: 255)

.. image:: img/15_mix_color_tone_cool.png

La differenza principale tra i colori caldi e freddi è il rapporto tra le intensità dei tre colori primari. Successivamente, memorizzeremo questi valori RGB caldi e freddi nel nostro sketch.

3. Apri lo sketch che hai salvato in precedenza, ``Lesson13_PWM_Color_Mixing``.

4. Clicca su "Salva con nome..." dal menu "File" e rinominalo in ``Lesson15_Cool_Warm_Color``. Premi "Salva".

5. Prima del ``void setup()``, dichiara sei variabili per memorizzare i valori RGB di questi due colori. Usa i colori che hai selezionato.

.. code-block:: Arduino
    :emphasize-lines: 1-4,6-9

    // Valori RGB per un colore caldo
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // Valori RGB per un colore freddo
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Codice da eseguire una volta all'inizio:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

**Utilizzo della funzione map()**

Per passare dall'illuminazione calda a quella fredda, tutto ciò che devi fare è ridurre l'intensità della luce rossa, aumentare quella blu e regolare finemente l'intensità della luce verde.

Nei progetti precedenti, abbiamo imparato come variare la luminosità del LED in base alla rotazione di un potenziometro.

Tuttavia, in questo progetto, la rotazione del potenziometro causa il cambiamento delle intensità dei pin RGB all'interno di un intervallo specifico, rendendo inadeguata una semplice divisione. Per questo, utilizziamo la funzione ``map()``.

Nel linguaggio di programmazione Arduino, la funzione ``map()`` è estremamente utile perché ti permette di mappare (o convertire) un intervallo numerico in un altro.

Ecco come utilizzarla:

* ``map(value, fromLow, fromHigh, toLow, toHigh)``: Mappa un numero da un intervallo a un altro. Un valore di ``fromLow`` verrà mappato su ``toLow``, un valore di ``fromHigh`` su ``toHigh`` e così via per i valori intermedi.

    **Parametri**
        * ``value``: il numero da mappare.
        * ``fromLow``: il limite inferiore dell'intervallo di partenza.
        * ``fromHigh``: il limite superiore dell'intervallo di partenza.
        * ``toLow``: il limite inferiore dell'intervallo di destinazione.
        * ``toHigh``: il limite superiore dell'intervallo di destinazione.

    **Restituisce**
        Il valore mappato. Tipo di dato: long.

La funzione ``map()`` scala un valore dal suo intervallo originale (fromLow a fromHigh) a un nuovo intervallo (toLow a toHigh). Prima, calcola la posizione del ``value`` all'interno dell'intervallo originale, quindi applica la stessa proporzione per scalare questa posizione nel nuovo intervallo.

.. image:: img/15_map_pic.png
    :width: 400
    :align: center

Pertanto, può essere scritta come la formula mostrata di seguito:

.. code-block::

    (value-fromLow)/(fromHigh-fromLow) = (y-toLow)/(toHigh-toLow)

Utilizzando l'algebra, puoi riordinare questa equazione per risolvere ``y``:

.. code-block::

    y = (value-fromLow) * (toHigh-toLow) / (fromHigh-fromLow) + toLow

.. image:: img/15_map_format.png

Ad esempio, utilizzando ``y = map(value, 0, 1023, 246, 100);``, se ``value`` è uguale a 434, allora ``y = (434-0) * (100 - 246) / (1023-0) + 246``, che è approssimativamente uguale a 152.

6. Rimuovi il codice originale nel ``void loop()``, quindi scrivi del codice per leggere il valore del potenziometro, memorizzandolo nella variabile ``potValue``.

.. code-block:: Arduino

    void loop() {
        // Codice da eseguire ripetutamente:
        int potValue = analogRead(A0);                         // Legge il valore dal potenziometro
    }

7. Usa poi la funzione ``map()`` per mappare il valore del potenziometro dall'intervallo 0~1023 all'intervallo 255 (``warm_r``) ~ 100 (``cool_r``).

.. code-block:: Arduino

    void loop() {
        // Codice da eseguire ripetutamente:
        int potValue = analogRead(A0);                         // Legge il valore dal potenziometro
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappa il valore del potenziometro sull'intensità del rosso
    }

8. Puoi usare il monitor seriale per visualizzare il ``potValue`` e il valore mappato ``value_r`` per approfondire la tua comprensione della funzione ``map()``. Ora, avvia il monitor seriale nel ``void setup()``.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Codice da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
        Serial.begin(9600);        // Configurazione della comunicazione seriale a 9600 baud
    }

9. Stampa le variabili ``potValue`` e ``value_r`` sulla stessa linea, separate da "|".

.. code-block:: Arduino
    :emphasize-lines: 23-26

    // Valori RGB per un colore caldo
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // Valori RGB per un colore freddo
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Codice da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
        Serial.begin(9600);        // Configurazione della comunicazione seriale a 9600 baud
    }

    void loop() {
        // Codice da eseguire ripetutamente:
        int potValue = analogRead(A0);                         // Legge il valore dal potenziometro
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappa il valore del potenziometro sull'intensità del rosso
        Serial.print(potValue);
        Serial.print(" | ");
        Serial.println(value_r);
        delay(500);  // Attende 500ms
    }

    // Funzione per impostare il colore del LED RGB
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // Scrive il valore PWM sul pin rosso
        analogWrite(10, green);  // Scrive il valore PWM sul pin verde
        analogWrite(9, blue);    // Scrive il valore PWM sul pin blu
    }

10. Ora puoi verificare e caricare il tuo codice, aprire il monitor seriale e vedrai due colonne di dati stampati.

.. code-block::

    434 | 152
    435 | 152
    434 | 152
    434 | 152
    434 | 152
    434 | 152

Dai dati è evidente che il valore 434, all'interno dell'intervallo 0~1023, corrisponde al valore 152 all'interno dell'intervallo 246~100.

**Regolazione della temperatura colore**

Qui utilizziamo la funzione ``map()`` per far variare l'intensità dei tre pin del LED RGB in base alla rotazione del potenziometro, passando dalle tonalità più calde a quelle più fredde.
Più specificamente, prendendo come riferimento i valori forniti, mentre si ruota il potenziometro, il valore R del LED RGB passerà gradualmente da 246 a 100, il valore G da 8 a 150 (anche se la variazione del valore G potrebbe non essere molto evidente), e il valore B da 8 a 255.

11. Successivamente, non avremo bisogno della stampa seriale temporaneamente, e la stampa seriale potrebbe influire sull'intero processo del codice, quindi usa ``Ctrl + /`` per commentare il codice relativo.

    .. note::

        Il motivo per cui non eliminiamo direttamente è che, se in futuro sarà necessario stampare, non sarà necessario riscrivere il codice; basterà selezionare queste righe e premere ``Ctrl + /`` per decommentarle.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        int potValue = analogRead(A0);                         // Leggi il valore dal potenziometro
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappa il valore del potenziometro sull'intensità del rosso
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Attendi per 500ms
    }

12. Continua a chiamare la funzione ``map()`` per ottenere i valori mappati ``value_g`` e ``value_b`` in base al valore del potenziometro.

.. code-block:: Arduino
    :emphasize-lines: 9,10

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        int potValue = analogRead(A0);                         // Leggi il valore dal potenziometro
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappa il valore del potenziometro sull'intensità del rosso
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Attendi per 500ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Mappa il valore del potenziometro sull'intensità del verde
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Mappa il valore del potenziometro sull'intensità del blu
    }

13. Infine, chiama la funzione ``setColor()`` per visualizzare i valori RGB mappati sul LED RGB.

.. code-block:: Arduino
    :emphasize-lines: 11,12

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        int potValue = analogRead(A0);                         // Leggi il valore dal potenziometro
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappa il valore del potenziometro sull'intensità del rosso
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Attendi per 500ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Mappa il valore del potenziometro sull'intensità del verde
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Mappa il valore del potenziometro sull'intensità del blu
        setColor(value_r, value_g, value_b);                   // Imposta il colore del LED
        delay(500);
    }

14. Il tuo codice completo è il seguente; puoi cliccare sul pulsante Upload per caricare il codice sull'Arduino Uno R3. Quindi puoi ruotare il potenziometro e noterai che il LED RGB passa lentamente da una tonalità fredda a una calda, o viceversa.

.. code-block:: Arduino

    // Valori RGB per un colore caldo
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // Valori RGB per un colore freddo
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // inserisci qui il codice di configurazione da eseguire una sola volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        int potValue = analogRead(A0);                         // Leggi il valore dal potenziometro
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappa il valore del potenziometro sull'intensità del rosso
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Attendi per 500ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Mappa il valore del potenziometro sull'intensità del verde
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Mappa il valore del potenziometro sull'intensità del blu
        setColor(value_r, value_g, value_b);                   // Imposta il colore del LED
        delay(500);                                            // Attendi 500ms
    }

    // Funzione per impostare il colore del LED RGB
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // Scrivi PWM sul pin rosso
        analogWrite(10, green);  // Scrivi PWM sul pin verde
        analogWrite(9, blue);    // Scrivi PWM sul pin blu
    }

15. Infine, ricorda di salvare il tuo codice e sistemare la tua area di lavoro.

**Consigli**

Durante l'esperimento, potresti notare che il passaggio tra tonalità calde e fredde non è così evidente come visto sullo schermo; ad esempio, una luce calda attesa potrebbe apparire bianca. Questo è normale, poiché la miscelazione dei colori in un LED RGB non è raffinata come su uno schermo.

In questi casi, puoi ridurre l'intensità dei valori G e B nel colore caldo per far visualizzare al LED RGB un colore più appropriato.

**Domanda**

Nota che i "limiti inferiori" di un intervallo possono essere maggiori o minori dei "limiti superiori", quindi la funzione ``map(value, fromLow, fromHigh, toLow, toHigh)`` può essere utilizzata per invertire un intervallo di numeri, ad esempio:

.. code-block::

    y = map(x, 1, 50, 50, 1);

La funzione gestisce bene anche i numeri negativi, quindi questo esempio è valido e funziona correttamente.

.. code-block::

    y = map(x, 1, 50, 50, -100);

Per ``y = map(x, 1, 50, 50, -100);``, se ``x`` è uguale a 20, quale dovrebbe essere ``y``? Fai riferimento alla seguente formula per calcolarlo.

.. image:: img/15_map_format.png
