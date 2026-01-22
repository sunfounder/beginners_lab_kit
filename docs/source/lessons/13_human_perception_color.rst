.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Experten-Support**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Sonderrabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu erkunden und zu kreieren? Klicke [|link_sf_facebook|] und tritt noch heute bei!

13. Das Farbspektrum des Sehens
================================================================================
Willkommen zu dieser Lektion, in der wir das Geheimnis der menschlichen Farbwahrnehmung entschlüsseln und es mithilfe von Technologie nachbilden. In dieser Lektion erforschen wir, wie unsere Augen Millionen von Farben unterscheiden und wie diese erstaunliche Fähigkeit digital mit RGB-LEDs simuliert werden kann. Durch die Untersuchung des Zusammenspiels von Photorezeptoren in unseren Augen und dem RGB-Farbmodell lernst du, die Lebendigkeit der Welt in digitaler Form nachzubilden.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/13_human_perception_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>


**Überblick**

Das menschliche visuelle System kann etwa zehn Millionen verschiedene Farben wahrnehmen, eine Fähigkeit, die durch Photorezeptorzellen in der Netzhaut – Zapfen und Stäbchen – ermöglicht wird. Die Farbwahrnehmung ist nicht linear; unser visuelles System ist empfindlicher gegenüber Änderungen bestimmter Farben als anderer. Zapfen, die für die Farbwahrnehmung zuständig sind, kommen hauptsächlich in drei Typen vor, die jeweils am empfindlichsten auf rotes, grünes oder blaues Licht reagieren.

Das menschliche Auge nimmt etwa zehn Millionen verschiedene Farben wahr, dank spezialisierter Zellen in der Netzhaut, den sogenannten Zapfen und Stäbchen. Diese Wahrnehmung ist nicht gleichmäßig über das Spektrum verteilt; wir sind empfindlicher für Veränderungen bei einigen Farben als bei anderen. Zapfen, die Farben erkennen, reagieren vorwiegend auf rote, grüne oder blaue Wellenlängen.

.. image:: img/13_mix_eyeballjpg.jpg

Das RGB-Farbmodell ist ein additives Farbmodell, bei dem Farben durch Mischen unterschiedlicher Intensitäten von Rot, Grün und Blau erzeugt werden. In diesem Modell gelten Rot, Grün und Blau typischerweise als primäre Farbkanäle. Durch die Anpassung der Intensität jedes Kanals (von 0 bis zu einem Maximalwert, typischerweise 255, was einer 8-Bit-Farbtiefe entspricht) können über 16 Millionen verschiedene Farben erzeugt werden. Zum Beispiel kann Orange durch Mischen von mehr Rot mit weniger Grün erreicht werden.

Das RGB-Farbmodell verwendet einen additiven Ansatz, bei dem rotes, grünes und blaues Licht gemischt wird, um eine Vielzahl von Farben zu erzeugen. Dieses Modell spiegelt wider, wie unser visuelles System Licht aus verschiedenen Teilen des Spektrums kombiniert, um diverse Farbtöne zu formen. Durch die Manipulation der Intensität dieser drei Primärfarben können wir über 16 Millionen verschiedene Farben erzeugen. Zum Beispiel erreichen wir Orange, indem wir Rot erhöhen und Grün verringern.

.. image:: img/13_mix_orange.jpg

In dieser interaktiven Lektion wendest du diese Prinzipien an, um eine RGB-LED zu steuern, die mithilfe präziser elektronischer Befehle die Farben deiner Wahl anzeigen kann.

**Lernziele**

* Verstehen, wie dieses Modell die menschliche Farbwahrnehmung nachahmt und seine Anwendung in digitalen Displays.
* Erlernen der Verwendung von Pulsweitenmodulation (PWM) für feine Farbmischungen mit einer RGB-LED.
* Verbesserung der Effizienz und Klarheit deines Codes durch das Erstellen von Funktionen mit Parametern in Arduino.
* Experimentiere mit verschiedenen RGB-Werten, um die Farben deiner LED individuell anzupassen und die Komplexität des menschlichen Farbsehens nachzuahmen.


Den Schaltkreis aufbauen
----------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB LED
     - 3 * 220Ω Widerstand
     - Steckbrücken
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     -
     -
   * - |list_usb_cable| 
     - |list_breadboard| 
     -
     -

Diese Lektion verwendet denselben Schaltkreis wie Lektion 12.

.. image:: img/12_mix_color_bb_4.png
    :width: 600
    :align: center


Codeerstellung - Farben anzeigen
------------------------------------

Auf unserer Reise zur Beherrschung der Steuerung von RGB-LEDs haben wir gesehen, wie mit ``digitalWrite()`` die LED in Grundfarben leuchtet. Um das gesamte Farbspektrum, das eine RGB-LED erzeugen kann, weiter zu erkunden, tauchen wir nun in die Verwendung von ``analogWrite()`` ein, um PWM-Signale (Pulsweitenmodulation) zu senden, die es uns ermöglichen, eine breite Palette von Farbtönen zu erreichen.

Sehen wir uns an, wie wir dies mit Code umsetzen können.

1. Öffne die Arduino-IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem „File“-Menü wählst.
2. Speichere deinen Sketch als ``Lesson13_PWM_Color_Mixing`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Zuerst stellst du die drei Pins der RGB-LED als Ausgänge ein:

.. code-block:: Arduino
    :emphasize-lines: 3-5

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Setze den blauen Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setze den grünen Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setze den roten Pin der RGB-LED als Ausgang
    }

4. Verwende ``analogWrite()``, um PWM-Werte an die RGB-LED zu senden. Aus Lektion 9 wissen wir, dass PWM-Werte die Helligkeit einer LED ändern können, und der PWM-Bereich liegt zwischen 0 und 255. Um Rot anzuzeigen, setzen wir den PWM-Wert des roten Pins der RGB-LED auf 255 und die anderen beiden Pins auf 0.

.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Setze den blauen Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setze den grünen Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setze den roten Pin der RGB-LED als Ausgang
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        analogWrite(9, 0);    // Setze den PWM-Wert des blauen Pins auf 0
        analogWrite(10, 0);   // Setze den PWM-Wert des grünen Pins auf 0
        analogWrite(11, 255);  // Setze den PWM-Wert des roten Pins auf 255
    }

5. Mit diesem Setup wird die RGB-LED nach dem Hochladen des Codes auf das Arduino Uno R3 Rot anzeigen.

6. Die Funktion ``analogWrite()`` ermöglicht es der RGB-LED, nicht nur die sieben Grundfarben, sondern viele andere Farbtöne anzuzeigen. Jetzt kannst du die Werte der Pins 9, 10 und 11 separat anpassen und die beobachteten Farben in deinem Notizbuch festhalten.

.. list-table::
    :widths: 20 20 20 40
    :header-rows: 1

    *   - Roter Pin    
        - Grüner Pin  
        - Blauer Pin
        - Farbe
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

Code-Erstellung - Parametrisierte Funktionen
------------------------------------------------

Die Verwendung der Funktion ``analogWrite()`` zum Anzeigen verschiedener Farben kann deinen Code umfangreich machen, wenn du viele Farben gleichzeitig anzeigen möchtest. Deshalb müssen wir Funktionen erstellen.

Im Gegensatz zur vorherigen Lektion bereiten wir uns darauf vor, eine Funktion mit Parametern zu erstellen.

Eine parametrisierte Funktion ermöglicht es, spezifische Werte an die Funktion zu übergeben, die diese dann zur Ausführung ihrer Aufgaben verwendet. Dies ist äußerst nützlich, um Eigenschaften wie die Farbintensität dynamisch anzupassen. Dadurch wird dein Code flexibler und leichter lesbar.

Beim Definieren einer parametrisierten Funktion gibst du an, welche Werte sie durch Parameter in Klammern nach dem Funktionsnamen benötigt, um zu funktionieren. Diese Parameter dienen als Platzhalter, die durch tatsächliche Werte ersetzt werden, wenn die Funktion aufgerufen wird.

So definierst du eine parametrisierte Funktion zur Einstellung der Farbe einer RGB-LED:

1. Öffne den Sketch, den du zuvor gespeichert hast, ``Lesson13_PWM_Color_Mixing``.

2. Wähle „Speichern unter...“ im Menü „Datei“ und benenne ihn um in ``Lesson13_PWM_Color_Mixing_Function``. Klicke auf "Speichern".

3. Beginne mit der Deklaration der Funktion nach ``void loop()`` mit dem Schlüsselwort ``void``, gefolgt vom Funktionsnamen und den Parametern in Klammern. Für unsere Funktion ``setColor`` verwenden wir drei Parameter—``red``, ``green`` und ``blue``—die jeweils die Intensität der entsprechenden Farbkomponente der RGB-LED darstellen.

.. code-block:: Arduino
    :emphasize-lines: 5,6

    void loop() {
        // Hier kommt dein Hauptcode, der wiederholt ausgeführt wird:
    }

    void setColor(int red, int green, int blue) {
    }


4. Innerhalb des Funktionskörpers verwendest du den Befehl ``analogWrite()``, um PWM-Signale an die RGB-LED-Pins zu senden. Die an ``setColor`` übergebenen Werte bestimmen die Helligkeit jeder Farbe. Die Parameter ``red``, ``green`` und ``blue`` werden hier verwendet, um die Intensität jedes LED-Pins direkt zu steuern.

.. code-block:: Arduino

    // Funktion zur Einstellung der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        // Schreibe den PWM-Wert für Rot, Grün und Blau auf die RGB-LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

5. Jetzt kannst du deine neu erstellte Funktion ``setColor()`` in der Funktion ``void loop()`` aufrufen. Da du eine Funktion mit Parametern erstellt hast, musst du die Argumente in die Klammern schreiben, wie z.B. ``(255, 0, 0)``. Denke daran, Kommentare zu schreiben.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        // Hier kommt dein Hauptcode, der wiederholt ausgeführt wird:
        setColor(255, 0, 0); // Zeige rote Farbe an
    }

    // Funktion zur Einstellung der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        // Schreibe den PWM-Wert für Rot, Grün und Blau auf die RGB-LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

6. Wir wissen bereits, dass durch das Anlegen verschiedener Werte an die drei Pins der RGB-LED unterschiedliche Farben erzeugt werden können. Wie lassen wir die RGB-LED also genau die Farbe leuchten, die wir wollen? Dazu brauchen wir eine Farbpalette. Öffne **Paint** (dieses Programm ist in Windows enthalten) oder eine beliebige Zeichensoftware auf deinem Computer.

.. image:: img/13_mix_color_paint.png

7. Wähle eine Farbe, die dir gefällt, und notiere ihre RGB-Werte.

.. note::

    Beachte, dass du vor der Farbauswahl die Helligkeit auf die richtige Position einstellen solltest.

.. image:: img/13_mix_color_paint_2.png

8. Trage die ausgewählte Farbe in die Funktion ``setColor()`` in der ``void loop()`` ein und verwende die Funktion ``delay()``, um die Anzeigedauer jeder Farbe festzulegen.

.. code-block:: Arduino

    void loop() {
        // Hier kommt dein Hauptcode, der wiederholt ausgeführt wird:
        setColor(255, 0, 0);      // Zeige rote Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(0, 128, 128);    // Zeige türkise Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 0, 255);    // Zeige lila Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 128, 255);  // Zeige hellblaue Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(255, 128, 0);    // Zeige orange Farbe an
        delay(1000);              // Warte 1 Sekunde
    }

9. Unten findest du den vollständigen Code; du kannst auf "Upload" klicken, um den Code auf das Arduino Uno R3 hochzuladen und die Effekte zu sehen.

.. code-block:: Arduino

    void setup() {
        // Hier kommt dein Setup-Code, der einmalig ausgeführt wird:
        pinMode(9, OUTPUT);   // Setze den blauen Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setze den grünen Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setze den roten Pin der RGB-LED als Ausgang
    }

    void loop() {
        // Hier kommt dein Hauptcode, der wiederholt ausgeführt wird:
        setColor(255, 0, 0);      // Zeige rote Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(0, 128, 128);    // Zeige türkise Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 0, 255);    // Zeige lila Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 128, 255);  // Zeige hellblaue Farbe an
        delay(1000);              // Warte 1 Sekunde
        setColor(255, 128, 0);    // Zeige orange Farbe an
        delay(1000);              // Warte 1 Sekunde
    }

    // Funktion zur Einstellung der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        // Schreibe den PWM-Wert für Rot, Grün und Blau auf die RGB-LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

10. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Zusammenfassung**

Die heutige Erforschung der Farbwahrnehmung schlägt eine Brücke zwischen der Biologie des Menschen und der elektronischen Anwendung und zeigt die Macht des Programmierens, abstrakte Konzepte zum Leben zu erwecken. Durch die Anpassung von RGB-Werten an einer LED hast du die Methode des Auges zur Farbwahrnehmung nachgeahmt und dabei sowohl ein tieferes Verständnis für die menschliche Biologie als auch fortgeschrittene Fähigkeiten in der elektronischen Steuerung erworben.
