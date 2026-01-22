.. note::

    Ciao, benvenuto nella community di SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato alle nuove presentazioni di prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e omaggi festivi**: Partecipa a omaggi e promozioni festive.

    👉 Sei pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

14. Colori Casuali
======================

A volte, la vita ha bisogno di un tocco di sorpresa. Quando sei indeciso, lascia che la casualità prenda il controllo. Questa lezione ti guiderà su come far illuminare un LED RGB con colori casuali, perfetto per aggiungere una scintilla imprevedibile ai tuoi progetti.

Costruzione del Circuito
-----------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Resistenze da 220Ω
     - Fili di collegamento
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

Creazione del Codice
----------------------------

Nelle lezioni precedenti, hai controllato il LED RGB per visualizzare i colori desiderati. Ma a volte potresti voler visualizzare un colore casuale, simile alle luci di scena. Come si può fare?

**Conoscere le funzioni random()**

Nel mondo fisico, la casualità abbonda, ma nella programmazione, i numeri "casuali" sono solitamente calcolati attraverso un algoritmo deterministico. Questo algoritmo richiede in genere un punto di partenza noto come "seme", rendendo questi numeri prevedibili, e quindi definiti "pseudo-casuali". Il prefisso "pseudo" indica che questi numeri sembrano casuali, ma in realtà seguono uno schema.

Interessante è che su un Arduino Uno R3 possiamo utilizzare misurazioni fisiche dal mondo reale come semi. Durante le tue misurazioni con un multimetro, potresti notare piccole fluttuazioni nei valori di tensione e corrente del circuito. Queste fluttuazioni possono fornire imprevedibilità ai nostri numeri casuali.

L'approccio di Arduino alla casualità prevede diverse funzioni:

* ``randomSeed();``: Inizializza il valore del seme del generatore di numeri casuali. Questa funzione garantisce che il punto di partenza della sequenza di numeri casuali vari ad ogni esecuzione del programma, generando così sequenze diverse.

    **Parametri**
        * ``seed``: Un valore usato per inizializzare il generatore di numeri casuali. Questo valore di tipo unsigned long imposta il punto di partenza della sequenza casuale.
    **Restituisce**
        Nessuno.

* ``long random(long max);``: Genera un numero casuale entro un intervallo specificato.

    **Parametri**
        ``max``: Il limite superiore del numero casuale (``max`` escluso), il che significa che il numero casuale sarà compreso tra 0 (incluso) e ``max-1`` (incluso).
    
    **Restituisce**
        Un numero di tipo long compreso tra 0 e max-1.

* ``long random(long min, long max);``: Genera un numero casuale entro un intervallo specificato.

    **Parametri**
        ``min``: Il limite inferiore del numero casuale (incluso).
        ``max``: Il limite superiore del numero casuale (``max`` escluso), il che significa che il numero casuale sarà compreso tra min (incluso) e max-1 (incluso).
    
    **Restituisce**
        Un numero di tipo long compreso tra min e max-1.

**Scrivere il Codice**

1. Apri lo sketch che hai salvato in precedenza, ``Lesson13_PWM_Color_Mixing``.

2. Clicca su “Salva con nome...” dal menu “File” e rinominalo in ``Lesson14_Random_Colors``. Clicca "Salva".

3. Chiama ``randomSeed()`` una sola volta in ``void setup()`` per inizializzare il seme. Evita di utilizzare un valore fisso per il seme, poiché questo causerebbe la generazione della stessa sequenza di numeri casuali ad ogni esecuzione del programma.

    Usiamo ``analogRead(A0)`` per leggere il valore da un pin analogico non connesso. Poiché questo pin non è collegato, rileva rumore che varia ad ogni lettura, fornendo un buon seme per ``randomSeed()``.

.. code-block:: Arduino
    :emphasize-lines: 9

    void setup() {
        // Codice di configurazione da eseguire una sola volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
            
        // Inizializza il seme casuale basato su un pin analogico non collegato
        // Questo assicura una sequenza diversa di numeri casuali ad ogni reset
        randomSeed(analogRead(A0));
    }

4. Ora in ``void loop()``, rimuovi il codice originale. Usa la funzione ``random()`` per generare valori casuali memorizzati nelle variabili ``redValue``, ``greenValue`` e ``blueValue``.

.. code-block:: Arduino
    :emphasize-lines: 3-5

    void loop(){
        // Genera valori casuali per ciascun componente del colore
        int redValue = random(0, 256);   // Valore casuale tra 0 e 255
        int greenValue = random(0, 256); // Valore casuale tra 0 e 255
        int blueValue = random(0, 256);  // Valore casuale tra 0 e 255
    }

5. Inserisci i valori RGB generati nella funzione ``setColor()``, permettendo al LED RGB di emettere il colore. Usa anche la funzione ``delay()`` per determinare quanto a lungo visualizzare il colore.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        // Genera valori casuali per ciascun componente del colore tra 0 e 255
        int redValue = random(0, 256);    // Genera un valore casuale per il rosso
        int greenValue = random(0, 256);  // Genera un valore casuale per il verde
        int blueValue = random(0, 256);   // Genera un valore casuale per il blu

        // Applica i valori casuali al LED RGB
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // Attendi 1 secondo
    }

6. Il tuo codice completo è pronto. Puoi caricarlo su Arduino Uno R3, e vedrai che il LED RGB mostrerà un colore casuale ogni secondo.

.. code-block:: Arduino
    :emphasize-lines: 19,20

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una volta:
        pinMode(9, OUTPUT);   // Imposta il pin Blu del LED RGB come output
        pinMode(10, OUTPUT);  // Imposta il pin Verde del LED RGB come output
        pinMode(11, OUTPUT);  // Imposta il pin Rosso del LED RGB come output
        
        // Inizializza il seme casuale basato su un pin analogico non collegato
        // Questo assicura una sequenza diversa di numeri casuali ad ogni reset
        randomSeed(analogRead(A0));
    }

    void loop() {
        // Genera valori casuali per ciascun componente del colore tra 0 e 255
        int redValue = random(0, 256);    // Genera un valore casuale per il rosso
        int greenValue = random(0, 256);  // Genera un valore casuale per il verde
        int blueValue = random(0, 256);   // Genera un valore casuale per il blu

        // Applica i valori casuali al LED RGB
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // Attendi 1 secondo
    }

    // Funzione per impostare il colore del LED RGB
    void setColor(int red, int green, int blue) {
        // Scrivi il valore PWM per rosso, verde e blu nel LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

7. Infine, ricorda di salvare il codice e sistemare il tuo spazio di lavoro.

**Domande**

1. Se cambi il codice da ``randomSeed(analogRead(A0))`` a ``randomSeed(0)``, come cambieranno i colori del LED RGB e perché?

2. Quali sono alcune situazioni in cui la casualità viene utilizzata per risolvere problemi nella vita quotidiana, oltre a scegliere colori casuali per la decorazione e numeri per la lotteria?

**Riepilogo**

Al termine di questa lezione, non solo avrai imparato la casualità nella programmazione e come manipolarla per creare vivaci display visivi inattesi, ma apprezzerai anche la bellezza semplice della casualità nella vita quotidiana. La programmazione può essere imprevedibile quanto la vita stessa, e con gli strumenti giusti, puoi sfruttare quell'imprevedibilità in modi creativi e funzionali.
