.. note::

    Ciao, benvenuto nella Community SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts su Facebook! Immergiti nel mondo del Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti a noi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotti e anteprime.
    - **Sconti speciali**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

16. Allarme di temperatura
=================================

In questa lezione, esploreremo l'importanza cruciale della gestione della temperatura nella sicurezza alimentare. Non tutti gli alimenti necessitano di essere refrigerati o congelati; anche prodotti a lunga conservazione come patatine, pane e alcuni frutti richiedono una corretta conservazione a temperature adeguate per mantenere la qualità e la sicurezza. Costruendo un sistema di monitoraggio della temperatura, impareremo come mantenere gli alimenti entro range sicuri, attivando un allarme quando le temperature si discostano da tali limiti. Questo progetto pratico non solo aiuta a proteggere il cibo, ma rappresenta anche un'introduzione eccellente al monitoraggio ambientale con applicazioni reali.

.. .. image:: img/16_temperature.jpg
..     :width: 400
..     :align: center

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/16_temp_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Alla fine di questa lezione, sarai in grado di:

* Comprendere l'importanza del controllo della temperatura nella sicurezza alimentare.
* Costruire un circuito con un termistore per monitorare le variazioni di temperatura.
* Scrivere un programma Arduino per leggere i dati di temperatura da un termistore.
* Utilizzare la logica nella programmazione per attivare azioni (come accendere un LED o far suonare un allarme) in base ai dati di temperatura.
* Applicare concetti di resistenza elettrica e conversione della temperatura in scenari pratici.

Costruzione del circuito
------------------------------

**Componenti necessari**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Resistenza da 220Ω
     - 1 * Resistenza da 10KΩ
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Termistore
     - 1 * Breadboard
     - Cavi di collegamento
     - 1 * Cavo USB
   * - |list_thermistor| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
   * - 1 * Multimetro
     - 
     - 
     - 
   * - |list_meter| 
     - 
     - 
     - 

**Passi per la costruzione**

Questo circuito si basa su quello della lezione 12, aggiungendo un termistore.

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

1. Partendo dal circuito della lezione 12, rimuovi il cavo di collegamento che connette il pin GND dell'Arduino Uno R3 al pin GND del LED RGB e inseriscilo nel terminale negativo della breadboard. Quindi collega un cavo dal terminale negativo al pin GND del LED RGB.

.. image:: img/16_temperature_alarm_gnd.png
    :width: 500
    :align: center

2. Inserisci il termistore nei fori 6E e 8E. I pin non sono direzionali e possono essere inseriti liberamente.

.. image:: img/16_temperature_alarm_thermistor.png
    :width: 500
    :align: center

Un termistore è un tipo speciale di resistenza la cui resistenza varia con la temperatura. Questo dispositivo è molto utile poiché ci aiuta a rilevare e misurare la temperatura, controllandola in vari progetti e dispositivi elettronici.

Ecco il simbolo elettronico del termistore.

.. image:: img/16_thermistor_symbol.png
    :width: 300
    :align: center

Esistono due tipi fondamentali di termistori:

* **Termistori NTC**: La resistenza diminuisce con l'aumentare della temperatura. Sono comunemente utilizzati come sensori di temperatura o limitatori di corrente in circuiti.
* **Termistori PTC**: La resistenza aumenta con l'aumentare della temperatura. Spesso vengono utilizzati come fusibili ripristinabili per proteggere i circuiti da sovracorrenti.

Nel nostro kit utilizziamo un termistore di tipo **NTC**.

Ora utilizza un multimetro per misurare la resistenza di questo termistore per verificare se effettivamente diminuisce con l'aumento della temperatura.

3. Poiché la resistenza nominale del termistore è di 10K, imposta il multimetro per misurare la resistenza nel range di 20 kilo-ohm (20K).

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

4. Ora tocca i due pin del termistore con i puntali rosso e nero del multimetro.

.. image:: img/16_temperature_alarm_test.png
    :width: 500
    :align: center

5. Leggi il valore della resistenza alla temperatura corrente e registralo nella tabella qui sotto.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Ambiente
     - Resistenza (kilohm)
   * - Temperatura corrente
     - *9.37*
   * - Temperatura più alta
     - 
   * - Temperatura più bassa
     - 

6. Ora puoi chiedere a un amico di tenere il termistore o utilizzare qualcos'altro per aumentare la temperatura intorno al termistore (senza acqua, senza fuoco, la sicurezza prima di tutto). Registra il valore della resistenza del termistore in questo momento nella tabella.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Ambiente
     - Resistenza (kilohm)
   * - Temperatura corrente
     - *9.37*
   * - Temperatura più alta
     - *6.10*
   * - Temperatura più bassa
     - 

7. Puoi posizionare il termistore all'aperto o ventilarlo per abbassare la temperatura circostante. Registra la resistenza misurata in questo momento nella tabella.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Ambiente
     - Resistenza (kilohm)
   * - Temperatura corrente
     - *9.37*
   * - Temperatura più alta
     - *6.10*
   * - Temperatura più bassa
     - *12.49*

Attraverso queste misurazioni, possiamo vedere che maggiore è la temperatura ambientale, minore è la resistenza.


8. Ora puoi continuare a costruire il circuito. Collega un'estremità del termistore a una resistenza da 10K, e l'altra estremità della resistenza da 10K al terminale negativo della breadboard.

.. image:: img/16_temperature_alarm_resistor.png
    :width: 500
    :align: center

9. Collega l'altra estremità della breadboard al pin 5V dell'Arduino Uno R3.

.. image:: img/16_temperature_alarm_5v.png
    :width: 500
    :align: center


10. Infine, collega il pin comune del fotoresistore e la resistenza da 10K al pin A0 dell'Arduino Uno R3.

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

Comprendere il calcolo della temperatura
-----------------------------------------
**A proposito della formula della temperatura**

La resistenza di un termistore NTC cambia con la temperatura. Questa relazione è solitamente descritta accuratamente dall'equazione di Steinhart-Hart, come segue:

.. image:: img/16_format_steinhart.png
    :width: 400
    :align: center

Qui, a, b e c sono chiamati parametri di Steinhart–Hart, che devono essere specificati per ogni dispositivo. T è la temperatura assoluta, e R è la resistenza.

Oltre all'equazione di Steinhart-Hart, molte applicazioni pratiche utilizzano anche una formula semplificata basata sul modello del parametro beta (parametro beta) per calcolare rapidamente la temperatura. Questo modello presume che la relazione tra resistenza e temperatura possa essere approssimata da una relazione esponenziale più semplice, semplificando così il processo di calcolo e rendendolo adatto al monitoraggio rapido della temperatura in applicazioni ingegneristiche.

.. image:: img/16_format_3.png
    :width: 400
    :align: center

* **T** è la temperatura del termistore in Kelvin.
* **T0** è una temperatura di riferimento, solitamente a 25°C (che corrisponde a 273,15 + 25 in Kelvin).
* **B** è il parametro beta del materiale; il coefficiente beta del termistore NTC usato in questo kit è 3950.
* **R** è la resistenza che misuriamo.
* **R0** è la resistenza alla temperatura di riferimento T0; la resistenza del termistore NTC in questo kit a 25°C è 10 kilohm.

Dopo aver convertito le formule sopra, la temperatura in Kelvin è calcolata come: ``T=1/(ln(R/R0)/B+1/T0)``, sottrai 273,15 per convertirla in gradi Celsius.

**Come misurare la resistenza?**

Nel nostro circuito, colleghiamo il termistore e una resistenza da 10K in serie.

.. image:: img/16_thermistor_sch.png
    :width: 200
    :align: center

La tensione al pin A0, che misuriamo, divisa per la resistenza in serie (la resistenza da 10K), ci indica la corrente che scorre attraverso il circuito. Questa corrente può anche essere ottenuta dividendo la tensione totale per la resistenza totale del circuito (resistenza in serie + termistore):

.. image:: img/16_format_1.png
    :width: 400
    :align: center

* **Vsupply**: La tensione fornita al circuito.
* **Rseries**: Il valore della resistenza in serie.
* **Vmeasured**: La tensione attraverso la resistenza da 10K, cioè la tensione al pin A0.

Da questi valori, possiamo riorganizzare la formula per trovare la resistenza del termistore:

.. image:: img/16_format_2.png
    :width: 400
    :align: center

Nel nostro codice, utilizziamo la funzione ``analogRead()`` per leggere la tensione al pin A0. La relazione tra la tensione **Vmeasured** e il valore analogico letto è:

.. code-block::

    (Analog value at A0) / 1023.0 = Vmeasured / Vsupply

Utilizzando la formula sopra, calcoliamo la resistenza del termistore:

.. code-block::

    R_thermistor =R_series x (1023.0 / (Analog value at A0) - 1)

.. note::

    Se le formule sembrano complicate, ricorda solo le seguenti e sei a posto!

    La resistenza del termistore può essere ottenuta tramite la seguente formula:

    .. code-block::

        R_thermistor =R_series x (1023.0 / (Analog value at A0) - 1)

    Poi calcola la temperatura in Kelvin usando la seguente formula:

    .. code-block::

        T=1/(ln(R/R0)/B+1/T0)

    * **T0**: 273,15 + 25.
    * **B**: 3950.
    * **R**: è la resistenza che misuriamo.
    * **R0**: 10 kilohm.

    Infine, converti in Celsius utilizzando la seguente formula:

    .. code-block::

        Tc = T - 273.15

Creazione del Codice
-----------------------

**Ottenere la Temperatura**

1. Apri l'Arduino IDE e inizia un nuovo progetto selezionando “Nuovo Sketch” dal menu “File”.
2. Salva il tuo sketch come ``Lesson16_Temperature_Alarm`` usando ``Ctrl + S`` o cliccando su “Salva”.

3. Nelle lezioni precedenti, abbiamo fatto riferimento direttamente ai pin dell'RGB LED nel nostro codice; qui, li definiamo come costanti.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // Configurazioni dei pin
    const int tempSensorPin = A0;  // Ingresso analogico del termistore NTC
    const int redPin = 11;         // Pin digitale LED rosso
    const int greenPin = 10;       // Pin digitale LED verde
    const int bluePin = 9;         // Pin digitale LED blu

    void setup() {
        // Inserisci qui il tuo codice di setup, da eseguire una sola volta:
    }

Utilizzare costanti anziché variabili, che rimangono invariate durante il programma, fornisce chiarezza e semplifica la manutenzione. Permette di usare nomi significativi al posto di numeri e le modifiche devono essere fatte solo nella dichiarazione, non ovunque nel codice. Le costanti seguono le stesse regole di denominazione delle variabili, evitando qualsiasi parola riservata o comando dell'IDE Arduino.

4. Prima di utilizzare il termistore, dobbiamo anche definire alcune altre costanti per memorizzare i parametri relativi al circuito.

.. note::

    Vedrai che ci sono costanti di tipo ``int`` e costanti di tipo ``float``. Quindi, qual è la differenza tra questi due tipi di costanti?

  * ``const int``: Una costante ``int`` (abbreviazione di integer) contiene numeri interi. Questo tipo non supporta frazioni o punti decimali. Occupa solitamente 16 o 32 bit di memoria, a seconda del sistema.
  * ``const float``: Una costante ``float`` (abbreviazione di floating-point) contiene numeri che possono avere parti frazionarie. È usata quando è necessaria maggiore precisione, ad esempio nelle misurazioni o nei calcoli che richiedono valori decimali. Un ``float`` occupa tipicamente 32 bit di memoria e può rappresentare una gamma più ampia di numeri rispetto a un ``int``.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // Configurazioni dei pin
    const int tempSensorPin = A0;  // Ingresso analogico del termistore NTC
    const int redPin = 10;         // Pin digitale LED rosso
    const int greenPin = 11;       // Pin digitale LED verde
    const int bluePin = 12;        // Pin digitale LED blu

    // Costanti per il calcolo della temperatura
    const float beta = 3950.0;               // Valore Beta del termistore NTC
    const float seriesResistor = 10000;      // Valore della resistenza in serie (ohm)
    const float roomTempResistance = 10000;  // Resistenza del NTC a 25°C
    const float roomTemp = 25 + 273.15;      // Temperatura ambiente in Kelvin

5. Nel ``void setup()``, imposta i pin dell'RGB LED come output e configura la velocità di comunicazione seriale a 9600 baud.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    void setup() {
        // Inizializza i pin LED come output
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);
        
        // Avvia la comunicazione seriale a 9600 baud
        Serial.begin(9600);
    }

6. Per prima cosa, devi leggere il valore analogico del pin A0 in ``void loop()``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leggi il valore del termistore
    }

7. Successivamente, calcola la resistenza del termistore usando la formula derivata precedentemente per convertire i valori analogici in tensione.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leggi il valore del termistore
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcola la resistenza del termistore
    }

8. Poi, calcola la temperatura in Kelvin utilizzando la formula mostrata qui sotto:

.. code-block:: Arduino
    :emphasize-lines: 6

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leggi il valore del termistore
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcola la resistenza del termistore

        // Calcola la temperatura in Kelvin usando l'equazione del parametro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    }

9. Sottrai 273.15 dalla temperatura in Kelvin per convertirla in Celsius, e poi stampa il risultato sul monitor seriale usando la funzione ``Serial.printlnln()``.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leggi il valore del termistore
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcola la resistenza del termistore

        // Calcola la temperatura in Kelvin usando l'equazione del parametro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // Converti in Celsius
        Serial.println(tempC);           // Visualizza la temperatura in Celsius sul monitor seriale
    }

10. A questo punto, puoi caricare il codice sul tuo Arduino Uno R3 e ottenere i valori di temperatura attuali in Celsius.

.. code-block::

    26.28
    26.19
    26.19
    26.28
    26.28
    
**Modifica del Colore dell'RGB LED**

Ora, cambiamo il colore dell'RGB LED in base alla temperatura misurata dal termistore.

Ad esempio, impostiamo tre intervalli di temperatura:

* Sotto i 10 gradi, l'RGB LED si illumina di verde, indicando che la temperatura è confortevole.
* Tra 10 e 20 gradi, l'RGB LED si illumina di giallo, segnalando cautela per la temperatura attuale.
* Sopra i 21 gradi, l'RGB LED si illumina di rosso, indicando che la temperatura è troppo alta e sono necessarie misure.

11. Per controllare l'RGB LED, utilizzeremo la funzione ``setColor()`` creata nelle lezioni precedenti.

.. code-block:: Arduino

    // Funzione per impostare il colore dell'RGB LED
    void setColor(int red, int green, int blue) {
        // Scrivi i valori PWM per rosso, verde e blu sull'RGB LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

12. Ora, utilizziamo una dichiarazione ``if else if`` per controllare il colore dell'RGB LED in base alle diverse temperature.

.. code-block:: Arduino
    :emphasize-lines: 12-18

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leggi il valore del termistore
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcola la resistenza del termistore

        // Calcola la temperatura in Kelvin usando l'equazione del parametro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // Converti in Celsius
        Serial.println(tempC);           // Visualizza la temperatura in Celsius sul Monitor Seriale

        // Regola il colore dell'LED in base alla temperatura
        if (tempC < 10) {
            setColor(0, 0, 255);  // Freddo: blu
        } else if (tempC >= 10 && tempC <= 21) {
            setColor(0, 255, 0);  // Confortevole: verde
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // Caldo: rosso
        }
        delay(1000);  // Ritarda di 1 secondo prima della prossima lettura
    }

13. Il tuo codice completo è ora pronto. Puoi caricare il codice sull'Arduino Uno R3 per vedere gli effetti.

.. code-block:: Arduino

    // Configurazione dei pin
    const int tempSensorPin = A0;  // Ingresso analogico del termistore NTC
    const int redPin = 10;         // Pin digitale LED rosso
    const int greenPin = 11;       // Pin digitale LED verde
    const int bluePin = 12;        // Pin digitale LED blu

    // Costanti per il calcolo della temperatura
    const float beta = 3950.0;               // Valore Beta del termistore NTC
    const float seriesResistor = 10000;      // Valore della resistenza in serie (ohm)
    const float roomTempResistance = 10000;  // Resistenza del NTC a 25°C
    const float roomTemp = 25 + 273.15;      // Temperatura ambiente in Kelvin

    void setup() {
        // Inizializza i pin LED come output
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);

        // Avvia la comunicazione seriale a 9600 baud
        Serial.begin(9600);
    }

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leggi il valore del termistore
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcola la resistenza del termistore

        // Calcola la temperatura in Kelvin usando l'equazione del parametro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);

        float tempC = tempK - 273.15;  // Converti in Celsius
        Serial.println(tempC);           //Visualizza la temperatura in Celsius sul Monitor Seriale

        // Regola il colore dell'LED in base alla temperatura
        if (tempC < 10) {
            setColor(0, 0, 255);  // Freddo: blu
        } else if (tempC >= 10 && tempC <= 21) {
            setColor(0, 255, 0);  // Confortevole: verde
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // Caldo: rosso
        }
        delay(1000);  // Ritarda di 1 secondo prima della prossima lettura
    }

    // Funzione per impostare il colore dell'RGB LED
    void setColor(int red, int green, int blue) {
        // Scrivi i valori PWM per rosso, verde e blu sull'RGB LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

14. Infine, ricorda di salvare il codice e di ordinare il tuo spazio di lavoro.

**Domande**

1. Nel codice, vengono calcolate le temperature in Kelvin e in Celsius. Se vuoi sapere anche la temperatura in Fahrenheit, cosa dovresti fare?

2. Riesci a pensare ad altre situazioni o luoghi in cui un sistema di monitoraggio della temperatura come quello che abbiamo costruito oggi potrebbe essere utile?

**Riepilogo**

Nella lezione di oggi, abbiamo costruito un sistema di allarme di temperatura che utilizza un termistore per monitorare la temperatura di un'area di stoccaggio per alimenti a lunga conservazione. Abbiamo imparato come leggere e convertire i valori di resistenza del termistore in letture di temperatura in gradi Celsius. Attraverso la nostra programmazione, abbiamo anche impostato condizioni per cambiare il colore di un RGB LED in base alla temperatura, fornendo un avviso visivo per temperature troppo basse, ideali o troppo alte.

