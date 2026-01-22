.. note::

    Ciao, benvenuto nella community di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti a noi?**

    - **Supporto esperto**: Risolvi i problemi post-vendita e le sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a concorsi e promozioni durante le festività.

    👉 Sei pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!


FAQ
====================

Cosa è incluso nel kit?
-------------------------------

Il kit include una scheda Arduino Uno R3 e una varietà di sensori, moduli, componenti e accessori per costruire esperimenti e progetti.

Vedi: :ref:`include_in_kit`


Qual è la differenza tra “Tutorial Video” e “Lezioni Pratiche”?
--------------------------------------------------------------------------------

* **Tutorial Video** ti aiutano a comprendere i concetti e a vedere le dimostrazioni.
* **Lezioni Pratiche** ti guidano nella costruzione dei circuiti e nella scrittura del codice utilizzando i componenti del kit.

Suggerimento:

* Guarda prima il video, poi completa la lezione pratica per una migliore memorizzazione.


Perché l’ Arduino UNO R3 non può essere utilizzato
-------------------------------------------------------------------

Anche utilizzando un Arduino UNO R3 ufficiale, la scheda potrebbe non funzionare correttamente a causa di fattori ambientali o operativi.  
Di seguito sono riportate le cause e le spiegazioni più comuni.

#. **Problemi con il driver USB o il sistema operativo**

   L’ Arduino UNO R3 utilizza un chip di interfaccia USB **ATmega16U2**, che normalmente viene riconosciuto automaticamente su Windows 10 / 11 e macOS.
   
   Tuttavia, sui sistemi più vecchi (come Windows 7 o installazioni Windows leggere), il driver USB CDC richiesto potrebbe mancare.  
   In questo caso, il computer potrebbe non riconoscere il dispositivo seriale Arduino.
   
   **Soluzione:**
   
   * Aggiorna o installa manualmente il driver USB di Arduino tramite **Gestione dispositivi**.
   * Si consiglia di includere le istruzioni per l’ aggiornamento del driver USB nelle FAQ come riferimento.


#. **Scheda o porta selezionata in modo errato nell’ Arduino IDE**

   Se la **Scheda** o la **Porta** corrette non sono selezionate nell’ Arduino IDE, il caricamento degli sketch fallirà.
   
   Un messaggio di errore comune è::
   
       stk500_recv(): programmer not responding
   
   Questo è un problema di configurazione e **non indica un danno hardware**.
   
   **Soluzione:**
   
   * Seleziona **Arduino UNO** in *Strumenti → Scheda*
   * Seleziona la porta seriale corretta in *Strumenti → Porta*


#. **Utilizzo di un hub USB o di una porta USB instabile**

   Se Arduino è collegato tramite:
   
   * Hub USB
   * Porte USB sui monitor
   * Porte USB integrate nelle tastiere
   
   L’ alimentazione e il segnale possono essere instabili, causando il fallimento della enumerazione USB di Arduino.
   
   **Raccomandazione:**
   
   * Collega Arduino **direttamente alla porta USB del computer**.


#. Problemi con la porta USB del computer

   Alcune porte USB possono presentare problemi come:
   
   * Alimentazione insufficiente (comune sulle porte USB frontali)
   * Scarso contatto fisico
   * Porte USB danneggiate
   
   **Raccomandazione:**
   
   * Prova una porta USB diversa
   * Preferibilmente utilizza le **porte USB posteriori sulla scheda madre**


#. Utilizzo simultaneo dell’ alimentazione USB e dell’ alimentazione esterna

   Se Arduino è alimentato tramite USB mentre viene fornita anche un’ alimentazione esterna tramite **5V** o **Vin**, ciò può causare:
   
   * Blocco del regolatore di tensione
   * Surriscaldamento del circuito di alimentazione
   * Comunicazione USB instabile
   
   Questo può far apparire Arduino disconnesso o instabile.
   
   **Raccomandazione:**
   
   * Evita di fornire alimentazione USB e alimentazione esterna contemporaneamente, a meno che non sia necessario e progettato correttamente.


#. **Errori di cablaggio che causano danni al chip USB**

   Durante il collegamento di moduli esterni, un cablaggio errato può causare danni al chip USB **ATmega16U2**, inclusi:
   
   * Inversione di **5V** e **GND**
   * Applicazione di alta tensione (come 12V) ai pin di Arduino
   * Conflitti di alimentazione tra USB e alimentatori esterni
   
   In questo caso, Arduino può ancora accendersi, ma il computer non riconoscerà la porta seriale.
   
   **Nota:**
   
   Questo tipo di guasto è causato da un uso scorretto e **non è un problema di qualità** della scheda Arduino stessa.


Perché il multimetro non può essere utilizzato
---------------------------------------------------------

Anche se il multimetro stesso funziona normalmente, un uso scorretto può farlo sembrare *non acceso* o *incapace di misurare*.  
Di seguito sono riportate le cause e le soluzioni più comuni.

#. **Batteria non installata**

   Sebbene nel kit sia inclusa una batteria da 9V, deve essere installata dall’ utente. Se la batteria non è installata, lo schermo del multimetro non si accenderà.
   
   Un video tutorial per l’ installazione della batteria è disponibile in :ref:`use_multimeter`.

#. Puntali di test collegati ai jack sbagliati

   Se il puntale rosso è inserito nel jack **10A** o **mA**, il multimetro non mostrerà letture quando si misurano tensione o resistenza.
   
   * Per le misurazioni di tensione o resistenza:
   
     * Puntale rosso → **VΩ**
     * Puntale nero → **COM**

#. **Intervallo di misura selezionato in modo errato**

   Se la modalità selezionata non corrisponde all’ obiettivo della misurazione, ad esempio:
   
   * Misurare la tensione DC usando l’ intervallo AC
   * Misurare la tensione usando la modalità resistenza
   
   Il multimetro non mostrerà letture corrette.
   
   **Soluzione:**
   
   * Seleziona l’ intervallo appropriato:
     * **DCV** per la tensione DC
     * **Ω** per la resistenza

#. Il multimetro si accende ma non può misurare

   Se il multimetro visualizza valori ma non può misurare con precisione, i puntali di test potrebbero essere danneggiati.
   
   La trazione o la torsione ripetuta dei puntali può causare la rottura interna dei fili e un contatto instabile.
   
   **Soluzione:**
   
   * Sostituisci i puntali di test se si verificano letture instabili o intermittenti


Come eseguire il mio primo programma Arduino?
------------------------------------------------

1. Collega la scheda Arduino al computer tramite un cavo USB.
2. Apri l’ Arduino IDE e seleziona la **Scheda** e la **Porta** corrette.
3. Apri uno sketch di esempio (come Blink) e fai clic su **Carica**.
4. Conferma il comportamento del LED integrato per verificare che funzioni.

Vedi: :ref:`first_sketch`


Il mio circuito non funziona come previsto. Cosa dovrei fare per prima cosa?
---------------------------------------------------------------------------------------

* Ricontrolla il cablaggio confrontandolo con il diagramma del tutorial (la maggior parte dei problemi sono errori di cablaggio).
* Verifica la polarità dei componenti (direzione del LED, polarità dei condensatori elettrolitici, ecc.).
* Conferma che l’ alimentazione e la massa siano collegate correttamente.
* Usa un multimetro per verificare la tensione nei punti chiave, se disponibile.

