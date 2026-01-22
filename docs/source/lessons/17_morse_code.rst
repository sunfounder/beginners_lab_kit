.. note::

    Ciao, benvenuto nella community di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto esperto**: Risolvi i problemi post-vendita e le sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima a nuovi annunci di prodotti e anticipazioni.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

17. Codice Morse
========================

Il codice Morse è come un linguaggio segreto fatto di punti (.) e linee (-), inventato da Samuel Morse negli anni '40 dell'Ottocento. Fu creato per inviare messaggi su lunghe distanze utilizzando i telegrafi. Ogni lettera dell'alfabeto e ogni numero è rappresentato da una combinazione unica di questi segnali. Ad esempio, il messaggio in codice Morse più famoso è "SOS" (··· ––– ···), un segnale internazionale di richiesta di aiuto. Prima dell'invenzione dei telefoni e di internet, il codice Morse era essenziale per le comunicazioni, ed era particolarmente popolare tra gli operatori di navi e aerei. Oggi è divertente impararlo per inviare messaggi segreti ai tuoi amici!

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/17_morse_code.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In questa lezione imparerai:

* Comprendere il funzionamento di un buzzer attivo.
* Imparare a programmare il segnale SOS in codice Morse, consentendoti di inviare messaggi utilizzando il codice Morse con un buzzer.


La magia del codice Morse!
------------------------------

.. image:: img/7_morse.jpeg

Immagina di inventare un modo per inviare messaggi segreti usando solo punti e linee! È quello che ha fatto Samuel Morse nel 1836 con il codice Morse. Inizialmente pittore, Morse fu ispirato durante un viaggio in barca e successivamente, con il suo amico Alfred Vail, creò il telegrafo per inviare messaggi attraverso i fili.

Il codice Morse utilizza punti (segnali brevi) e linee (segnali lunghi) per rappresentare lettere e numeri. Il primo messaggio in codice Morse? "What hath God wrought"—inviato nel 1844 da Washington D.C. a Baltimora, dando inizio all'era del telegrafo.

Oggi, il codice Morse non è più utilizzato così frequentemente, ma è ancora interessante in campi come l'aviazione e tra gli appassionati di radio amatoriale. Ora, esploriamo come funziona il codice Morse con Arduino e un buzzer, divertendoci con questo pezzo di storia della comunicazione!


Costruire il circuito
-------------------------

**Componenti necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Buzzer attivo
     - 1 * Breadboard
     - Fili jumper
   * - |list_uno_r3| 
     - |list_active_buzzer| 
     - |list_breadboard| 
     - |list_wire| 
   * - 1 * Cavo USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 


**Costruzione passo passo**

1. Trova un buzzer attivo, che solitamente ha un adesivo bianco sul davanti e un retro sigillato nero.

.. image:: img/7_beep_2.png

I buzzers, come dispositivi sonori elettronici, hanno una storia ricca che risale al XIX secolo. Il precursore dei buzzers moderni ha le sue radici nel 1831, quando Michael Faraday scoprì l'induzione elettromagnetica, che rappresenta il principio fondamentale dietro il funzionamento dei buzzers elettromagnetici. Oggi, i buzzers si dividono in due categorie principali: attivi e passivi:

**Buzzer attivo**

.. image:: img/7_beep_ac.png
    :width: 300
    :align: center

Sigillati sul retro, i buzzers attivi contengono un oscillatore interno che emette un suono continuo quando alimentati, tipicamente producendo un singolo tono.

**Buzzer passivo**

.. image:: img/7_beep_pa.png
    :width: 300
    :align: center

Aperto sul retro, un buzzer passivo richiede un segnale di frequenza esterno da un microcontrollore per generare suoni, permettendo di produrre una gamma di toni.

1. Il buzzer attivo è anche un dispositivo polarizzato. Il lato frontale ha un segno "+" che indica il terminale positivo (anodo), che corrisponde anche al pin più lungo. Inserisci ora il buzzer nella breadboard con l'anodo nel foro 15F e il catodo nel foro 18F.

.. image:: img/16_morse_code_buzzer.png
    :width: 500
    :align: center

2. Collega il catodo al pin GND dell'Arduino Uno R3.

.. image:: img/16_morse_code_gnd.png
    :width: 500
    :align: center

3. Se inserisci l'anodo del buzzer nel pin 5V dell'Arduino Uno R3, sentirai il buzzer attivo emettere un suono direttamente. Ovviamente, puoi usare questo metodo per verificare se il buzzer che hai è corretto. Un buzzer passivo non emetterà suoni se collegato direttamente a una fonte di alimentazione.

.. image:: img/16_morse_code_5v.png
    :width: 500
    :align: center

4. Ora, rimuovi il filo inserito nel pin 5V e inseriscilo nel pin 9 dell'Arduino Uno R3, così il buzzer potrà essere controllato tramite il codice.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Creazione del codice
-------------------------

1. Apri l'IDE di Arduino e avvia un nuovo progetto selezionando “Nuovo sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson17_Morse_Code`` usando ``Ctrl + S`` o cliccando su "Salva".

3. Per prima cosa, crea una costante chiamata ``buzzerPin`` e assegnale il valore del pin 9.

.. code-block:: Arduino
    :emphasize-lines: 1

    const int buzzerPin = 9;   // Assegna il pin 9 alla costante per il buzzer

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una sola volta:
    }

4. Inizializza il pin: Nella funzione ``void setup()``, imposta il pin del buzzer in modalità output.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;   // Assegna il pin 9 alla costante per il buzzer

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una sola volta:
        pinMode(buzzerPin, OUTPUT);  // Imposta il pin 9 come output
    }

5. Far suonare un buzzer attivo è semplice come accendere un LED; devi solo usare ``digitalWrite()`` per impostare il pin 9 alto o basso e ``delay()`` per controllare il tempo.

.. code-block:: Arduino
    :emphasize-lines: 10-13

    const int buzzerPin = 9;   // Assegna il pin 9 alla costante per il buzzer

    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una sola volta:
        pinMode(buzzerPin, OUTPUT);  // Imposta il pin 9 come output
    }

    void loop() {
        // inserisci qui il codice principale, da eseguire ripetutamente:
        digitalWrite(buzzerPin, HIGH);  // Accendi il buzzer
        delay(250);                     // Durata del beep: 250 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il buzzer
        delay(250);                     // Intervallo tra i segnali: 250 millisecondi
    }

6. Puoi caricare il codice sull'Arduino Uno R3 e sentire il suono "beep beep".

7. Per far emettere al buzzer il codice Morse, devi creare due funzioni dopo ``void loop()``, per emettere i punti (segnali brevi) e le linee (segnali lunghi).

.. note::

    Nel codice Morse, ci sono regole tradizionali sui tempi dei punti (segnali brevi), delle linee (segnali lunghi) e degli intervalli tra i segnali per garantire che il messaggio venga ricevuto e compreso correttamente. Ecco alcune regole di base:

    * Durata di un punto: l'unità di tempo base.
    * Durata di una linea: uguale a tre punti.
    * Intervallo tra i punti: la lunghezza di un punto.
    * Intervallo all'interno di un carattere (tra punti e linee di una lettera o numero): la lunghezza di un punto.
    * Intervallo tra i caratteri (ad es. tra due lettere): tre punti.
    * Intervallo tra le parole (ad es. tra due parole): sette punti.

    Pertanto, impostiamo la lunghezza di un punto a 250ms, una linea a 750ms, e l'intervallo tra gli elementi a 250ms.

.. code-block:: Arduino
    :emphasize-lines: 9-14,16-21

    void loop() {
        // inserisci qui il codice principale, da eseguire ripetutamente:
        digitalWrite(buzzerPin, HIGH);  // Accendi il buzzer
        delay(250);                     // Durata del beep: 250 millisecondi
        digitalWrite(buzzerPin, LOW);   // Spegni il buzzer
        delay(250);                     // Intervallo tra i segnali: 250 millisecondi
    }

    void punto() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Durata breve per un punto
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervallo tra i segnali
    }

    void linea() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Durata più lunga per una linea
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervallo tra i segnali
    }

8. Ora puoi trasmettere il codice Morse. Ad esempio, per inviare "SOS" (... --- ...), il codice Morse per 'S' consiste in tre punti, mentre 'O' è composto da tre linee, quindi chiami semplicemente le funzioni punto e linea tre volte ciascuna.

.. code-block:: Arduino
    :emphasize-lines: 2-11

    void loop() {
        dot();
        dot();
        dot();  // S: ...
        dash();
        dash();
        dash();  // O: ---
        dot();
        dot();
        dot();       // S: ...
        delay(750);  // Repeat after a period
    }

9. Ecco il codice completo. Ora puoi cliccare su "Carica" per caricare il codice sull'Arduino Uno R3, dopodiché sentirai il codice Morse per "SOS" (... --- ...).

.. code-block:: Arduino

    const int buzzerPin = 9;   // Assegna il pin 9 alla costante per il buzzer
    
    void setup() {
        // inserisci qui il codice di configurazione, da eseguire una sola volta:
        pinMode(buzzerPin, OUTPUT);  // Imposta il pin 9 come output
    }

    void loop() {
        dot();
        dot();
        dot();  // S: ...
        dash();
        dash();
        dash();  // O: ---
        dot();
        dot();
        dot();       // S: ...
        delay(750);  // Repeat after a period
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Durata breve per un punto
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervallo tra i segnali
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Durata più lunga per una linea
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervallo tra i segnali
    }

10. Infine, ricordati di salvare il codice e di sistemare l'area di lavoro.


**Riassunto**

In questa lezione, hai esplorato i fondamenti del codice Morse, una forma unica di comunicazione sviluppata negli anni 1840 da Samuel Morse. Hai imparato a utilizzare un buzzer attivo per inviare il codice Morse per SOS, un segnale di soccorso riconosciuto universalmente. Questa lezione ti ha insegnato non solo come configurare e programmare un buzzer attivo, ma ti ha anche dato un assaggio dell'importanza storica del codice Morse nelle telecomunicazioni. Con queste competenze, ora puoi inviare messaggi in codice Morse segreti ai tuoi amici o esplorare ulteriormente le sue applicazioni nei dispositivi moderni.

In questa lezione, abbiamo utilizzato solo i codici Morse per le lettere "S" e "O". Di seguito trovi la tabella con i codici Morse per le 26 lettere dell'alfabeto e i 10 numeri.


.. list-table::
    :widths: 8 8 8 8 8 8 8 8
    :header-rows: 1

    * - Letter
      - Code
      - Letter
      - Code
      - Letter
      - Code
      - Letter
      - Code
    * - A
      - \.- 
      - B
      - \-...
      - C
      - \-.\-.
      - D
      - \-..
    * - E
      - \.
      - F
      - \..-.
      - G
      - \-\-.
      - H
      - \....
    * - I
      - \..
      - J
      - \.\-\-\-
      - K
      - \-.-
      - L
      - \.-..
    * - M
      - \--
      - N
      - \-.
      - O
      - \-\-\-
      - P
      - \.-\-.
    * - Q
      - \-\-.-
      - R
      - \.-.
      - S
      - \...
      - T
      - \-
    * - U
      - \..-
      - V
      - \...-
      - W
      - \.-\-
      - X
      - \-..-
    * - Y
      - \-.-\-
      - Z
      - \-\-..
      - 1
      - \.\-\-\-\-
      - 2
      - \..\-\-\-
    * - 3
      - \...-\-
      - 4
      - \....-
      - 5
      - \.....
      - 6
      - \-....
    * - 7
      - \-\-...
      - 8
      - \-\-\-..
      - 9
      - \-\-\-\-.
      - 
      - 
    


**Domanda**

Utilizzando la tabella del codice Morse fornita, scrivi un codice per inviare il messaggio "Hello".

