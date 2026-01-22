.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 zusammen mit anderen Enthusiasten ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Einblicke hinter die Kulissen.
    - **Spezielle Rabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu erschaffen? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

17. Morse-Code
========================

Der Morse-Code ist wie eine Geheimsprache, die aus Punkten (.) und Strichen (-) besteht und in den 1840er Jahren von Samuel Morse erfunden wurde. Er wurde entwickelt, um Nachrichten über weite Entfernungen mit Hilfe von Telegrafen zu übermitteln. Jeder Buchstabe des Alphabets und jede Zahl wird durch eine einzigartige Kombination dieser Signale dargestellt. Zum Beispiel ist die bekannteste Morsecode-Nachricht "SOS" (··· ––– ···), ein internationaler Hilferuf. Der Morsecode war vor der Erfindung von Telefonen und dem Internet unverzichtbar für die Kommunikation, insbesondere bei Schiffs- und Flugzeugbetreibern. Heute macht es Spaß, Morsecode zu lernen, um geheime Nachrichten an Freunde zu senden!

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/17_morse_code.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion wirst du lernen:

* Die Funktionsweise eines aktiven Summers verstehen.
* Das SOS-Signal im Morsecode zu programmieren, sodass du Nachrichten mit einem Summer im Morsecode senden kannst.


Morse-Code-Magie!
---------------------

.. image:: img/7_morse.jpeg

Stell dir vor, eine Möglichkeit zu erfinden, geheime Nachrichten nur mit Punkten und Strichen zu übermitteln! Genau das hat Samuel Morse 1836 mit dem Morsecode gemacht. Ursprünglich Maler, wurde Morse auf einer Schiffsreise inspiriert und entwickelte später zusammen mit seinem Kollegen Alfred Vail den Telegrafen, um Nachrichten über Drähte zu senden.

Der Morsecode verwendet Punkte (kurze Signale) und Striche (lange Signale), um Buchstaben und Zahlen darzustellen. Die erste gesendete Morsecode-Nachricht lautete "What hath God wrought" und wurde 1844 von Washington D.C. nach Baltimore übermittelt, was den Beginn des Telegrafen-Zeitalters markierte.

Heute wird der Morsecode nicht mehr so häufig verwendet, ist aber in Bereichen wie der Luftfahrt und bei Amateurfunkern nach wie vor beliebt. Nun wollen wir erkunden, wie der Morsecode mit Arduino und einem Summer funktioniert, und dabei Spaß mit diesem Stück Kommunikationsgeschichte haben!


Den Schaltkreis aufbauen
----------------------------

**Benötigte Bauteile**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Aktiver Summer
     - 1 * Steckbrett
     - Verbindungskabel
   * - |list_uno_r3| 
     - |list_active_buzzer| 
     - |list_breadboard| 
     - |list_wire| 
   * - 1 * USB-Kabel
     -
     - 
     - 
   * - |list_usb_cable| 
     -
     - 
     - 


**Schritt-für-Schritt-Anleitung**

1. Finde einen aktiven Summer, der normalerweise einen weißen Aufkleber auf der Vorderseite und eine versiegelte schwarze Rückseite hat.

.. image:: img/7_beep_2.png

Summersignale, als elektronische Klangerzeuger, haben eine reiche Geschichte, die bis ins 19. Jahrhundert zurückreicht. Der Vorläufer moderner Summer basiert auf der Entdeckung der elektromagnetischen Induktion durch Michael Faraday im Jahr 1831, welche das grundlegende Prinzip für den Betrieb elektromagnetischer Summer bildete. Nach Faradays bahnbrechender Entdeckung erkundeten viele Wissenschaftler und Erfinder die Anwendung elektromagnetischer Theorien auf praktische Geräte. Heute werden Summer in aktive und passive Typen unterteilt:

**Aktiver Summer**

.. image:: img/7_beep_ac.png
    :width: 300
    :align: center

Aktive Summer sind an der Rückseite versiegelt und enthalten einen internen Oszillator, der bei Stromzufuhr einen Einzelton erzeugt.

**Passiver Summer**

.. image:: img/7_beep_pa.png
    :width: 300
    :align: center

Passive Summer haben eine offene Rückseite und benötigen ein externes Frequenzsignal von einem Mikrocontroller, um Töne zu erzeugen, was eine Vielzahl von Klängen ermöglicht.

1. Ein aktiver Summer ist auch ein polares Bauteil. Die Vorderseite hat ein "+"-Zeichen, das den positiven Anschluss (Anode) kennzeichnet, der auch der längere Pin ist. Stecke nun den Summer so in das Steckbrett, dass die Anode in Loch 15F und die Kathode in Loch 18F ist.

.. image:: img/16_morse_code_buzzer.png
    :width: 500
    :align: center

2. Verbinde die Kathode mit dem GND-Pin des Arduino Uno R3.

.. image:: img/16_morse_code_gnd.png
    :width: 500
    :align: center

3. Wenn du die Anode des Summers in den 5V-Pin des Arduino Uno R3 steckst, hörst du sofort ein Geräusch vom aktiven Summer. Natürlich kannst du diese Methode auch nutzen, um zu überprüfen, ob dein Summer korrekt ist. Ein passiver Summer gibt keinen Ton von sich, wenn er direkt mit einer Stromquelle verbunden wird.

.. image:: img/16_morse_code_5v.png
    :width: 500
    :align: center

4. Entferne nun das Kabel, das im 5V-Pin steckt, und stecke es in Pin 9 des Arduino Uno R3, damit der Summer über den Code gesteuert werden kann.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center



Code-Erstellung
--------------------
1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „Datei“ die Option „Neue Skizze“ auswählst.
2. Speichere deine Skizze als ``Lesson17_Morse_Code`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Erstelle zunächst eine Konstante namens ``buzzerPin`` und weise ihr den Wert für Pin 9 zu.

.. code-block:: Arduino
    :emphasize-lines: 1

    const int buzzerPin = 9;   // Weist Pin 9 der Konstanten für den Summer zu

    void setup() {
        // Hier kommt der Setup-Code, der einmal ausgeführt wird:
    }

4. Initialisiere den Pin: In der Funktion ``void setup()`` setze den Summer-Pin auf den Ausgangsmodus.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;   // Weist Pin 9 der Konstanten für den Summer zu

    void setup() {
        // Hier kommt der Setup-Code, der einmal ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 auf Ausgang
    }

5. Einen aktiven Summer einen Ton ausgeben zu lassen, ist genauso einfach wie eine LED zu steuern; du musst nur ``digitalWrite()`` verwenden, um Pin 9 auf HIGH oder LOW zu setzen, und mit ``delay()`` die Zeitsteuerung kontrollieren.

.. code-block:: Arduino
    :emphasize-lines: 10-13

    const int buzzerPin = 9;   // Weist Pin 9 der Konstanten für den Summer zu

    void setup() {
        // Hier kommt der Setup-Code, der einmal ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 auf Ausgang
    }

    void loop() {
        // Hier kommt der Hauptcode, der wiederholt ausgeführt wird:
        digitalWrite(buzzerPin, HIGH);  // Schaltet den Summer ein
        delay(250);                     // Tonlänge: 250 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schaltet den Summer aus
        delay(250);                     // Abstand zwischen Signalen: 250 Millisekunden
    }

6. Du kannst deinen Code auf das Arduino Uno R3 hochladen, dann wirst du den „Beep-Beep“-Ton hören.

7. Um den Summer Morsecode ausgeben zu lassen, musst du zwei Funktionen nach ``void loop()`` erstellen, eine für Punkte (kurze Signale) und eine für Striche (lange Signale).

.. note::

    Im Morsecode gibt es traditionelle Zeitregeln für Punkte (kurze Signale), Striche (lange Signale) und die Abstände zwischen den Signalen, um sicherzustellen, dass die Nachricht korrekt empfangen und verstanden wird. Hier sind einige Grundregeln:

    * Länge eines Punktes: die Basiseinheit der Zeit.
    * Länge eines Strichs: entspricht drei Punkten.
    * Abstand zwischen Punkten: die Länge eines Punktes.
    * Abstand innerhalb eines Zeichens (zwischen Punkten und Strichen eines Buchstabens oder einer Zahl): die Länge eines Punktes.
    * Abstand zwischen Zeichen (z. B. zwischen zwei Buchstaben): drei Punkte.
    * Abstand zwischen Wörtern (z. B. zwischen zwei Wörtern): sieben Punkte.

    Daher setzen wir die Länge eines Punktes auf 250 ms, eines Strichs auf 750 ms und den Abstand zwischen den Elementen auf 250 ms.

.. code-block:: Arduino
    :emphasize-lines: 9-14,16-21

    void loop() {
        // Hier kommt der Hauptcode, der wiederholt ausgeführt wird:
        digitalWrite(buzzerPin, HIGH);  // Schaltet den Summer ein
        delay(250);                     // Tonlänge: 250 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schaltet den Summer aus
        delay(250);                     // Abstand zwischen Signalen: 250 Millisekunden
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Kurze Dauer für einen Punkt
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Abstand zwischen Signalen
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Längere Dauer für einen Strich
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Abstand zwischen Signalen
    }

8. Jetzt kannst du Morsecode senden. Um zum Beispiel "SOS" (... --- ...) zu senden, besteht der Morsecode für 'S' aus drei Punkten, und 'O' aus drei Strichen. Du rufst also einfach die Funktionen dot und dash jeweils dreimal auf.

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
        delay(750);  // Wiederholen nach einer kurzen Pause
    }

9. Hier ist dein vollständiger Code. Du kannst nun auf "Hochladen" klicken, um den Code auf das Arduino Uno R3 hochzuladen, danach wirst du den Morsecode für "SOS" (... --- ...) hören.

.. code-block:: Arduino

    const int buzzerPin = 9;   // Weist Pin 9 der Konstanten für den Summer zu
    
    void setup() {
        // Hier kommt der Setup-Code, der einmal ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 auf Ausgang
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
        delay(750);  // Wiederholen nach einer kurzen Pause
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Kurze Dauer für einen Punkt
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Abstand zwischen Signalen
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Längere Dauer für einen Strich
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Abstand zwischen Signalen
    }

10. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.


**Zusammenfassung**

In dieser Lektion hast du die Grundlagen des Morsecodes erkundet, einer einzigartigen Kommunikationsform, die in den 1840er Jahren von Samuel Morse entwickelt wurde. Du hast gelernt, wie man einen aktiven Summer verwendet, um den Morsecode für SOS, ein weltweit anerkanntes Notsignal, zu senden. Diese Lektion hat dir nicht nur gezeigt, wie man einen aktiven Summer einrichtet und programmiert, sondern dir auch einen Einblick in die historische Bedeutung des Morsecodes in der Telekommunikation gegeben. Mit diesen Fähigkeiten kannst du nun geheime Morsecode-Nachrichten an Freunde senden oder die Anwendungen des Morsecodes in modernen Geräten weiter erkunden.

In dieser Lektion haben wir nur die Morsecodes für die Buchstaben "S" und "O" verwendet. Hier ist die Tabelle mit den Morsecodes für die 26 Buchstaben und 10 Ziffern.

.. list-table::
    :widths: 8 8 8 8 8 8 8 8
    :header-rows: 1

    * - Buchstabe
      - Code
      - Buchstabe
      - Code
      - Buchstabe
      - Code
      - Buchstabe
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

**Frage**

Verwende die bereitgestellte Morsecode-Tabelle und schreibe einen Code, um die Nachricht "Hello" zu senden.

