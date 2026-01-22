.. note::

    Ciao, benvenuto nella community di SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts su Facebook! Approfondisci Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotti e anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Omaggi**: Partecipa a omaggi e promozioni festive.

    👉 Sei pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi stesso!

13. Lo Spettro della Vista
================================================================================
Benvenuto in questa lezione, dove sveleremo il mistero della percezione dei colori da parte dell'uomo e la riprodurremo utilizzando la tecnologia. In questa lezione, esploreremo come i nostri occhi distinguono milioni di colori e come questa incredibile capacità possa essere simulata digitalmente con i LED RGB. Attraverso l'interazione tra i fotorecettori nei nostri occhi e il modello di colore RGB, imparerai a ricreare la vividezza del mondo in forma digitale.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/13_human_perception_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>


**Panoramica**

Il sistema visivo umano può percepire circa dieci milioni di colori diversi, 
capacità ottenuta grazie alle cellule fotorecettrici nella retina: coni e 
bastoncelli. La percezione del colore non è lineare; il nostro sistema visivo 
è più sensibile ai cambiamenti in certi colori rispetto ad altri. I coni, 
sensibili al colore, sono principalmente di tre tipi, ciascuno maggiormente 
sensibile alla luce rossa, verde o blu.

.. image:: img/13_mix_eyeballjpg.jpg

Il modello di colore RGB è un modello di colore additivo in cui i colori 
vengono creati mescolando intensità variabili di luce rossa, verde e blu. 
In questo modello, il rosso, il verde e il blu sono considerati tipicamente 
i canali di colore primari. Regolando l'intensità di ciascun canale (da 0 a 
un valore massimo, tipicamente 255 corrispondenti a una profondità di colore 
di 8 bit), è possibile produrre uno spettro visibile di oltre 16 milioni di 
colori diversi. Ad esempio, l'arancione si ottiene mescolando più rosso e meno verde.

.. image:: img/13_mix_orange.jpg

In questa lezione interattiva, applicherai questi principi per controllare un LED RGB, permettendogli di mostrare i colori di tua scelta attraverso precisi comandi elettronici.

**Obiettivi di Apprendimento**

* Comprendere come questo modello imiti la percezione del colore umano e la sua applicazione nei display digitali.
* Imparare a usare la Modulazione di Larghezza di Impulso (PWM) per una miscelazione dei colori più dettagliata con i LED RGB.
* Migliorare l'efficienza e la chiarezza del codice creando funzioni che accettano parametri in Arduino.
* Sperimentare con diversi valori RGB per personalizzare i colori del tuo LED, rispecchiando la complessità della visione umana.


Costruzione del Circuito
------------------------------

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
     - 
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - 
     - 

Questa lezione utilizza lo stesso circuito della Lezione 12.

.. image:: img/12_mix_color_bb_4.png
    :width: 600
    :align: center


Creazione del Codice - Visualizzare i Colori
-------------------------------------------------

Nel nostro percorso per padroneggiare il controllo dei LED RGB, abbiamo visto come l'uso di ``digitalWrite()`` possa accendere il LED in colori di base. Per esplorare ulteriormente e sbloccare l'intero spettro di colori che un LED RGB può produrre, ora approfondiremo l'uso di ``analogWrite()`` per inviare segnali PWM (Pulse Width Modulation), permettendoci di ottenere una vasta gamma di sfumature.

Vediamo come implementare questo con il codice.

1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando "Nuovo Sketch" dal menu "File".
2. Salva il tuo sketch come ``Lesson13_PWM_Color_Mixing`` utilizzando ``Ctrl + S`` o facendo clic su "Salva".

3. Per prima cosa, imposta i tre pin del LED RGB come output:

.. code-block:: Arduino
    :emphasize-lines: 3-5

    void setup() {
        // Imposta il codice da eseguire una sola volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

4. Usa ``analogWrite()`` per inviare valori PWM al LED RGB. Dalla Lezione 9 sappiamo che i valori PWM possono modificare la luminosità di un LED, e il range PWM è 0-255. Per visualizzare il rosso, impostiamo il valore PWM del pin rosso del LED RGB a 255, e gli altri due pin a 0.

.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // Imposta il codice da eseguire una sola volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // Codice principale da eseguire ripetutamente:
        analogWrite(9, 0);    // Imposta il valore PWM del pin Blu a 0
        analogWrite(10, 0);   // Imposta il valore PWM del pin Verde a 0
        analogWrite(11, 255);  // Imposta il valore PWM del pin Rosso a 255
    }

5. Con questa configurazione, dopo aver caricato il codice sull'Arduino Uno R3, vedrai il LED RGB accendersi di rosso.

6. La funzione ``analogWrite()`` permette al LED RGB di visualizzare non solo i sette colori di base, ma anche molte altre sfumature diverse. Ora puoi regolare i valori dei pin 9, 10 e 11 separatamente e annotare i colori osservati nel tuo manuale.

.. list-table::
    :widths: 20 20 20 40
    :header-rows: 1

    *   - Pin Rosso    
        - Pin Verde  
        - Pin Blu
        - Colore
    *   - 0
        - 128
        - 128
        - 
    *   - 128
        - 0
        - 255
        - 
    *   - 128
        - 128
        - 255
        - 
    *   - 255
        - 128
        - 0
        - 

Creazione del Codice - Funzioni con Parametri
--------------------------------------------------

L'uso della funzione ``analogWrite()`` per visualizzare diversi colori può rendere il tuo codice lungo se vuoi mostrare molti colori contemporaneamente. Per questo motivo, è necessario creare delle funzioni.

A differenza della lezione precedente, ci stiamo preparando a creare una funzione con parametri.

Una funzione parametrizzata ti consente di passare valori specifici alla funzione, che poi utilizzerà questi valori per svolgere i suoi compiti. Questo è estremamente utile per regolare proprietà come l'intensità del colore in modo dinamico. Rende il tuo codice più flessibile e facile da leggere.

Quando definisci una funzione con parametri, specifichi quali valori sono necessari per il suo funzionamento attraverso parametri elencati tra parentesi subito dopo il nome della funzione. Questi parametri agiscono come segnaposto che vengono sostituiti da valori reali quando la funzione viene chiamata.

Ecco come definire una funzione parametrizzata per impostare il colore di un LED RGB:

1. Apri lo sketch che hai salvato in precedenza, ``Lesson13_PWM_Color_Mixing``.

2. Clicca su “Salva con nome...” dal menu “File” e rinominalo in ``Lesson13_PWM_Color_Mixing_Function``. Clicca "Salva".

3. Inizia dichiarando la funzione dopo il ``void loop()`` con la parola chiave ``void``, seguita dal nome della funzione e dai parametri tra parentesi. Per la nostra funzione ``setColor``, utilizzeremo tre parametri— ``red``, ``green`` e ``blue``—ciascuno rappresentante l'intensità del corrispondente componente di colore del LED RGB.

.. code-block:: Arduino
    :emphasize-lines: 5,6

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
    }

    void setColor(int red, int green, int blue) {
    }

   
4. All'interno del corpo della funzione, usa il comando ``analogWrite()`` per inviare segnali PWM ai pin del LED RGB. I valori passati a ``setColor`` determineranno la luminosità di ciascun colore. I parametri ``red``, ``green`` e ``blue`` vengono utilizzati qui per controllare direttamente l'intensità di ciascun pin LED.

.. code-block:: Arduino

    // Funzione per impostare il colore del LED RGB
    void setColor(int red, int green, int blue) {
        // Scrivi il valore PWM per rosso, verde e blu nel LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }


5. Ora puoi chiamare la tua funzione appena creata ``setColor()`` nel ``void loop()``. Dal momento che hai creato una funzione con parametri, devi riempire gli argomenti tra le ``()`` come ``(255, 0, 0)``. Ricorda di aggiungere commenti.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        setColor(255, 0, 0); // Mostra il colore rosso
    }

    // Funzione per impostare il colore del LED RGB
    void setColor(int red, int green, int blue) {
        // Scrivi il valore PWM per rosso, verde e blu nel LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

6. Sappiamo già che fornendo valori diversi ai tre pin del LED RGB, possiamo accendere diverse tonalità di luce. Quindi, come facciamo a far illuminare il LED RGB esattamente del colore che desideriamo? Ciò richiede l'uso di una palette di colori. Apri **Paint** (software incluso in Windows) o qualsiasi programma di disegno sul tuo computer.

.. image:: img/13_mix_color_paint.png

7. Scegli un colore che ti piace e annota i suoi valori RGB.

.. note::

    Nota che prima di selezionare un colore, regola la luminosità alla posizione corretta.

.. image:: img/13_mix_color_paint_2.png

8. Inserisci il colore che hai selezionato nella funzione ``setColor()`` nel ``void loop()``, utilizzando la funzione ``delay()`` per specificare il tempo di visualizzazione di ciascun colore.

.. code-block:: Arduino

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        setColor(255, 0, 0);      // Mostra il colore rosso
        delay(1000);              // Attendi 1 secondo
        setColor(0, 128, 128);    // Mostra il colore turchese
        delay(1000);              // Attendi 1 secondo
        setColor(128, 0, 255);    // Mostra il colore viola
        delay(1000);              // Attendi 1 secondo
        setColor(128, 128, 255);  // Mostra il colore blu chiaro
        delay(1000);              // Attendi 1 secondo
        setColor(255, 128, 0);    // Mostra il colore arancione
        delay(1000);              // Attendi 1 secondo
    }

9. Di seguito è riportato il codice completo; puoi fare clic su "Carica" per caricare il codice sull'Arduino Uno R3 e vedere gli effetti.

.. code-block:: Arduino

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
    }

    void loop() {
        // inserisci qui il codice principale da eseguire ripetutamente:
        setColor(255, 0, 0);      // Mostra il colore rosso
        delay(1000);              // Attendi 1 secondo
        setColor(0, 128, 128);    // Mostra il colore turchese
        delay(1000);              // Attendi 1 secondo
        setColor(128, 0, 255);    // Mostra il colore viola
        delay(1000);              // Attendi 1 secondo
        setColor(128, 128, 255);  // Mostra il colore blu chiaro
        delay(1000);              // Attendi 1 secondo
        setColor(255, 128, 0);    // Mostra il colore arancione
        delay(1000);              // Attendi 1 secondo
    }

    // Funzione per impostare il colore del LED RGB
    void setColor(int red, int green, int blue) {
        // Scrivi il valore PWM per rosso, verde e blu nel LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

10. Infine, ricorda di salvare il codice e sistemare il tuo spazio di lavoro.


**Riepilogo**

L'esplorazione odierna della percezione del colore colma il divario tra la scienza biologica e l'applicazione elettronica, evidenziando il potere della programmazione nel portare concetti astratti alla realtà. Regolando i valori RGB su un LED, hai imitato il metodo dell'occhio umano di percepire i colori, ottenendo una maggiore comprensione della biologia umana e competenze avanzate nel controllo elettronico.
