.. note::

    Ciao, benvenuto nella comunità di appassionati di Raspberry Pi & Arduino & ESP32 di SunFounder su Facebook! Approfondisci Raspberry Pi, Arduino ed ESP32 con altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni l'accesso anticipato a nuovi annunci di prodotti e anteprime.
    - **Sconti speciali**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a omaggi e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi stesso!

24. Luce Scorrevole con 74HC595
=======================================

In questa lezione, esploreremo il mondo del chip 74HC595, un componente potente che ci permette di controllare numerosi LED con pochi pin, rendendolo perfetto per creare effetti di luce scorrevole. Alla fine di questa lezione, avrai una solida comprensione di come funziona il 74HC595, come usarlo per spostare i dati binari e come applicarlo in un esperimento pratico di controllo LED.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/24_flowing_light.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In questa lezione imparerai:

* Comprendere i principi di funzionamento del chip 74HC595 e le sue funzioni pin.
* Imparare a utilizzare la funzione ``shiftOut()`` per spostare i dati.
* Costruire un circuito di luce scorrevole usando il chip 74HC595 e Arduino.
* Controllare 8 LED utilizzando dati binari e il chip 74HC595 per creare un effetto di luce scorrevole.

Imparare il Chip 74HC595
----------------------------

Il chip 74HC595 consiste in un registro a scorrimento a 8 bit e un registro di memoria con uscite parallele a tre stati. Converte l'input seriale in output parallelo, permettendoti di risparmiare porte IO di un microcontrollore.

.. image:: img/24_74hc595.png
    :width: 300
    :align: center

**Funzioni dei Pin**

.. image:: img/24_74hc595_pin.png
    :width: 500
    :align: center

* **Q0-Q7**: Uscite dati parallele a 8 bit, capaci di controllare direttamente 8 LED o 8 pin di un display a 7 segmenti.
* **Q7'**: Pin di uscita seriale, collegato al DS di un altro 74HC595 per connettere più 74HC595 in serie.
* **MR**: Pin di reset, attivo a livello basso.
* **SHcp**: Ingresso della sequenza temporale del registro a scorrimento. Al fronte di salita, i dati nel registro a scorrimento si spostano successivamente di un bit, ovvero i dati in Q1 si spostano su Q2, e così via. Al fronte di discesa, i dati nel registro rimangono invariati.
* **STcp**: Ingresso della sequenza temporale del registro di memoria. Al fronte di salita, i dati nel registro a scorrimento si trasferiscono nel registro di memoria.
* **CE**: Pin di abilitazione dell'uscita, attivo a livello basso.
* **DS**: Pin di ingresso dati seriali.
* **VCC**: Alimentazione positiva.
* **GND**: Terra.

**Principio di Funzionamento**

Quando MR (pin 10) è a livello alto e OE (pin 13) è a livello basso, 
i dati vengono inseriti al fronte di salita di SHcp e passano al registro di memoria al fronte di salita di STcp.

* Registro a Scorrimento

    * Supponiamo di voler inserire i dati binari 1110 1110 nel registro a scorrimento del 74HC595.
    * I dati vengono inseriti a partire dal bit 0 del registro a scorrimento.
    * Ogni volta che il clock del registro a scorrimento ha un fronte di salita, i bit nel registro vengono spostati di un passo. Ad esempio, il bit 7 accetta il valore precedente del bit 6, il bit 6 prende il valore del bit 5, e così via.

.. image:: img/24_74hc595_shift.png
    :width: 600
    :align: center

* Registro di Memoria

    * Quando il registro di memoria si trova nello stato di fronte di salita, i dati del registro a scorrimento vengono trasferiti nel registro di memoria.
    * Il registro di memoria è direttamente collegato agli 8 pin di uscita; Q0 ~ Q7 saranno in grado di ricevere un byte di dati. 
    * Il cosiddetto registro di memoria significa che i dati possono rimanere in questo registro e non scompariranno con un'uscita. 
    * I dati rimarranno validi e invariati finché il 74HC595 rimane alimentato. 
    * Quando arrivano nuovi dati, quelli presenti nel registro di memoria verranno sovrascritti e aggiornati.

.. image:: img/24_74hc595_storage.png
    :width: 600
    :align: center



Costruzione del Circuito
--------------------------------

**Componenti Necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 8 * LED
     - 8 * Resistenza da 220Ω
     - 1 * 74HC595
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_74hc595|  
   * - 1 * Breadboard
     - Fili di collegamento
     - 1 * Cavo USB
     - 
   * - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
     - 

**Costruzione Passo per Passo**

Segui il diagramma di cablaggio o i passaggi seguenti per costruire il tuo circuito.

.. image:: img/24_flow_light.png
    :width: 600
    :align: center

1. Inserisci 8 LED nella breadboard, in qualsiasi configurazione di colore desideri. Assicurati che tutti i catodi (gambe corte) degli LED siano collegati alla barra di terra sulla breadboard, mentre gli anodi siano collegati a file separate.

.. image:: img/24_flow_light_led.png
    :width: 500
    :align: center

2. Collega una resistenza da 220Ω a ciascun anodo degli LED.

.. image:: img/24_flow_light_resistor.png
    :width: 500
    :align: center

3. Trova il chip 74HC595 e inseriscilo nella breadboard. Assicurati che il chip attraversi il divario centrale.

.. note::

    Fai molta attenzione all'orientamento del 74HC595 per evitare danni. Puoi identificare l'orientamento corretto usando i seguenti indizi:

    * L'etichetta sul chip è in posizione verticale.
    * La tacca sul chip è rivolta verso sinistra.

.. image:: img/24_flow_light_74hc595.png
    :width: 500
    :align: center

4. Collega i pin VCC e MR del 74HC595 alla barra positiva della breadboard.

.. image:: img/24_flow_light_vcc.png
    :width: 500
    :align: center

5. Collega i pin CE e GND del 74HC595 alla barra negativa della breadboard.

.. image:: img/24_flow_light_gnd.png
    :width: 500
    :align: center

6. Collega i pin Q0-Q7 del 74HC595 alle file della breadboard che contengono le resistenze da 220Ω.

.. image:: img/24_flow_light_q0_q7.png
    :width: 500
    :align: center

7. Collega il pin DS del 74HC595 al pin 11 dell'Arduino Uno R3.

.. image:: img/24_flow_light_pin11.png
    :width: 600
    :align: center

8. Collega il pin ST_CP del 74HC595 al pin 12 dell'Arduino Uno R3.

.. image:: img/24_flow_light_pin12.png
    :width: 600
    :align: center

9. Collega il pin Sh_CP del 74HC595 al pin 8 dell'Arduino Uno R3.

.. image:: img/24_flow_light_pin8.png
    :width: 600
    :align: center

10. Infine, collega i pin GND e 5V dell'Arduino Uno R3 rispettivamente alle barre negative e positive sulla breadboard.

.. image:: img/24_flow_light.png
    :width: 600
    :align: center

11. La seguente tabella mostra le connessioni tra il 74HC595 e l'Arduino Uno R3.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - Arduino UNO R3
    *   - VCC
        - 5V
    *   - Q0~Q7
        - LED
    *   - DS
        - 11
    *   - CE
        - GND
    *   - ST_CP
        - 12
    *   - SH_CP
        - 8
    *   - MR
        - 5V
    *   - GND
        - GND

Creazione del Codice - Accendere i LED
--------------------------------------------

L'Arduino Uno R3 invia gruppi di dati binari al chip 74HC595.
I dati binari formano il nucleo dei computer e di molti dispositivi elettronici, utilizzando semplici 0 e 1 per elaborare dati e istruzioni complessi. 
Nella scienza informatica e nell'elettronica digitale, i dati binari sono essenziali poiché costituiscono la base per l'elaborazione e l'archiviazione delle informazioni nei computer elettronici.
Qui, 0 e 1 possono essere visti come stati di un interruttore, dove 0 rappresenta spento (chiuso) e 1 rappresenta acceso (aperto).

Per i numeri binari, è necessario comprendere due concetti base:

* Bit: Un bit è l'unità di base nel sistema binario, e ogni bit può essere 0 o 1.
* Byte: Un byte è composto da 8 bit. È un'unità comune di elaborazione dati nei computer. (E guarda, il chip 74HC595 accetta esattamente 1 byte di dati alla volta!)

I numeri binari sono ordinati dal bit meno significativo al più significativo, con il bit più a destra che è il meno significativo e il bit più a sinistra che è il più significativo.

.. image:: img/24_binary_bit.png
    :width: 500
    :align: center

Vediamo ora come il 74HC595 riceve i dati binari e li trasmette ai LED!

1. Apri l'Arduino IDE e avvia un nuovo progetto selezionando "New Sketch" dal menu "File".
2. Salva il tuo sketch come ``Lesson24_Lighting_up_LEDs`` utilizzando ``Ctrl + S`` o cliccando "Save".

3. Il controllo del 74HC595 richiede solo tre pin per fornire segnali di impulso, quindi imposta questi pin come OUTPUT.

.. code-block:: Arduino

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595

    void setup() {
        // Imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

4. Il tuo computer invia dati binari al pin ``DS`` (Data Input) del 74HC595, quindi utilizza il segnale di clock dal pin ``SH_CP`` (Shift Register Clock Input) per spostare ogni bit di dati in avanti. Questo processo di trasmissione dati può essere implementato utilizzando la funzione ``shiftOut()``.

    * ``shiftOut(dataPin, clockPin, bitOrder, value)``: Sposta un byte di dati un bit alla volta. Inizia dal bit più significativo (MSB) o meno significativo (LSB). Ogni bit viene scritto sul pin dei dati, dopodiché un pin di clock viene pulsato (prima alto, poi basso) per indicare che il bit è pronto.

    **Parametri**

        * ``dataPin``: il pin su cui inviare ogni bit. Tipi di dati ammessi: int.
        * ``clockPin``: il pin da alternare una volta che il dataPin è stato impostato sul valore corretto. Tipi di dati ammessi: int.
        * ``bitOrder``: l'ordine con cui inviare i bit; può essere ``MSBFIRST`` o ``LSBFIRST`` (Most Significant Bit First o Least Significant Bit First).
        * ``value``: il dato da spostare. Tipi di dati ammessi: byte.

    **Restituisce**
        Nessun valore.

5. Qui, proviamo a inviare un byte (8 bit) di dati al registro a scorrimento del 74HC595 usando la funzione ``shiftOut()``.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop()
    {
        shiftOut(DS, SHcp, MSBFIRST, B11101110);  // Sposta i dati, MSB first
    }

* Questo invia i dati ``B11101110`` (binario, B indica binario) al registro a scorrimento del 74HC595, con i dati inviati a partire dal bit più significativo.
* Ogni volta che il pin ``SH_CP`` riceve un segnale di fronte di salita (il momento in cui la tensione passa da bassa ad alta), i bit nel registro a scorrimento vengono spostati di un passo.
* Ad esempio, il bit 7 accetta il valore precedente del bit 6, il bit 6 prende il valore del bit 5, e così via.

.. image:: img/24_74hc595_shift.png
    :width: 500
    :align: center

6. Dopo che tutti i bit di dati sono stati immessi attraverso il pin DS e spostati nelle posizioni corrette utilizzando segnali di clock multipli, il passaggio successivo è copiare questi dati dal registro a scorrimento a un registro di memoria.

.. code-block:: Arduino
    :emphasize-lines: 2,7

    void loop() {
        digitalWrite(STcp, LOW);  // Imposta ST_CP (Pin Latch) a livello basso e mantienilo basso durante la trasmissione dei dati
        
        // Invia i dati al registro a scorrimento utilizzando MSBFIRST (Most Significant Bit First)
        shiftOut(DS, SHcp, MSBFIRST, B11101110);
        
        digitalWrite(STcp, HIGH);  // Porta ST_CP a livello alto per salvare i dati nei pin di uscita
        
        delay(1000);  // Attendi un secondo prima di ripetere
    }

* Quando il pin ``ST_CP`` riceve un segnale di fronte di salita, i dati nel registro a scorrimento vengono copiati nel registro di memoria.
* Una volta copiati i dati nel registro di memoria, i LED collegati ai pin di uscita corrispondenti (Q0 ~ Q7) si accenderanno o rimarranno spenti a seconda che il dato sia 1 o 0.

.. image:: img/24_74hc595_storage_1data.png
    :width: 300
    :align: center

7. Ecco il tuo codice completo. Ora puoi caricare questo codice sull'Arduino Uno R3. Dopodiché vedrai i LED collegati a Q0 e Q4 spenti mentre gli altri LED saranno accesi.

.. code-block:: Arduino

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595

    void setup() {
        // Imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        digitalWrite(STcp, LOW);  // Porta ST_CP a livello basso e mantienilo basso durante la trasmissione
        shiftOut(DS, SHcp, MSBFIRST, B11101110);  // Invia i dati, MSB first
        digitalWrite(STcp, HIGH);  // Porta ST_CP a livello alto per salvare i dati
        delay(1000);  // Attendi un secondo
    }

**Domanda**

Cosa succede se cambiamo ``MSBFIRST`` con ``LSBFIRST`` in ``shiftOut(DS, SHcp, MSBFIRST, B11101110);``? Perché?



Creazione del Codice - Luce Scorrevole
---------------------------------------------

Come possiamo implementare un effetto di luce scorrevole, dove i LED si accendono uno alla volta?

1. Apri lo sketch che hai salvato in precedenza, ``Lesson24_Lighting_up_LEDs``. 

2. Fai clic su “Salva con nome...” dal menu “File” e rinominalo in ``Lesson24_Flowing_Light``. Clicca su "Salva".

3. Qui, vogliamo configurare una luce scorrevole, dove i LED si accendono uno alla volta. Scriveremo gli stati di accensione/spegnimento di questa sequenza di luci scorrevoli come un array.

.. code-block:: Arduino
    :emphasize-lines: 4

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595
    int datArray[] = {B00000000, B00000001, B00000011, B00000111, B00001111, B00011111, B00111111, B01111111, B11111111};

4. Poi, utilizza un ciclo ``for`` per chiamare sequenzialmente questo array.

.. code-block:: Arduino
    :emphasize-lines: 3,5

    void loop()
    {
        for (int num = 0; num <= 8; num++) {
            digitalWrite(STcp, LOW);                      // Imposta ST_CP a livello basso e mantienilo basso durante la trasmissione
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Invia i dati, MSB first
            digitalWrite(STcp, HIGH);                     // Porta ST_CP a livello alto per salvare i dati
            delay(1000);                                  // Attendi un secondo
        }
    }

5. Ecco il tuo codice completo. Ora puoi caricare questo codice sull'Arduino Uno R3, e vedrai i LED accendersi uno alla volta, come una luce scorrevole.

.. code-block:: Arduino

    const int STcp = 12;  // Pin collegato a ST_CP del 74HC595
    const int SHcp = 8;   // Pin collegato a SH_CP del 74HC595
    const int DS = 11;    // Pin collegato a DS del 74HC595
    int datArray[] = {B00000000, B00000001, B00000011, B00000111, B00001111, B00011111, B00111111, B01111111, B11111111};

    void setup ()
    {
        // Imposta i pin come output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop()
    {
        for (int num = 0; num <= 8; num++) {
            digitalWrite(STcp, LOW);                      // Imposta ST_CP a livello basso e mantienilo basso durante la trasmissione
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Invia i dati, MSB first
            digitalWrite(STcp, HIGH);                     // Porta ST_CP a livello alto per salvare i dati
            delay(1000);                                  // Attendi un secondo
        }
    }

6. Infine, ricorda di salvare il codice e sistemare la tua postazione di lavoro.

**Domanda**

Se vogliamo avere tre LED accesi alla volta e farli sembrare "scorrere", come dovrebbero essere modificati gli elementi dell'array ``datArray[]``?

**Riepilogo**

In questa lezione, abbiamo esplorato la struttura e il funzionamento del chip 74HC595, imparando come trasferire i dati binari attraverso il suo registro a scorrimento e costruire un esperimento di luce scorrevole. Utilizzando la funzione ``shiftOut()`` per controllare la trasmissione dei dati binari, siamo riusciti a gestire l'accensione sequenziale di 8 LED per ottenere un effetto di luce scorrevole. Con queste nuove conoscenze, ora dovresti essere in grado di utilizzare efficacemente il chip 74HC595 per aggiungere effetti di illuminazione brillanti ai tuoi progetti.

