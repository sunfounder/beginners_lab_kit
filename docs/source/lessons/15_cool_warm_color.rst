.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in Raspberry Pi, Arduino und ESP32 ein, gemeinsam mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte frühzeitig Informationen über neue Produkte und Vorschauen.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Gewinnspielen und Sonderaktionen zu Feiertagen teil.

    👉 Bereit, mit uns zu experimentieren und zu gestalten? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

15. Warme oder kühle Farben
====================================

Farben sind nicht nur Teil unserer visuellen Erfahrung – sie beeinflussen auch unsere Emotionen und Gefühle. In dieser Lektion befassen wir uns mit den psychologischen Auswirkungen von Farben und lernen, wie man eine RGB-LED zwischen warmen und kühlen Farben wechseln lässt, um die Effekte wechselnder Lichttemperaturen nachzuahmen.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/15_cool_warm_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

**Überblick**

Das Konzept von warmen und kühlen Farben bezieht sich auf die psychologischen Wirkungen, die Farben auf unsere Wahrnehmung haben. Rottöne, Orangetöne, Gelb- und Brauntöne rufen in der Regel Gefühle von Wärme und Aufregung hervor und werden als warme Farben eingestuft. Im Gegensatz dazu vermitteln Grün-, Blau- und Violetttöne oft beruhigende, erfrischende und weite Gefühle, was sie zu kühlen Farben macht. Orange und Blau stehen dabei an den entgegengesetzten Enden dieses Wärme-Kälte-Spektrums.

.. image:: img/15_mix_color_warm_cool.png
    :width: 400
    :align: center

Zuhause oder in Freizeitumgebungen bevorzugen Menschen oft Licht in hellen Gelb- oder Weißtönen, die eine gemütliche Atmosphäre schaffen, ähnlich dem Licht bei Sonnenuntergang oder Kerzenschein.

.. image:: img/15_mix_color_warm_room.png
    :width: 400
    :align: center

In Bibliotheken, Klassenzimmern, Büros und Krankenhäusern werden kühlere Lichttöne bevorzugt, da sie die Konzentration fördern und Frische ausstrahlen – ideal für Lern- und Arbeitsumgebungen.

.. image:: img/15_mix_color_cool_room.png
    :width: 400
    :align: center

Die Wärme oder Kühle des Lichts ist eine spürbare Erfahrung, die unsere psychologische Reaktion und unseren visuellen Komfort beeinflusst. Designer und Lichtingenieure wählen sorgfältig Farbtemperaturen aus, die der Funktion eines Raums und der gewünschten Atmosphäre entsprechen, um sowohl ästhetisch ansprechende als auch funktionale Beleuchtungsumgebungen zu schaffen. Durch die wissenschaftliche Anwendung dieser Prinzipien können wir die Qualität unserer Lebens- und Arbeitsumgebungen verbessern und eine gesündere und angenehmere Atmosphäre schaffen.

In dieser Lektion übernehmen wir die Rolle von Lichttechnikern und entwickeln ein Beleuchtungssystem, das zwischen verschiedenen Farbtemperaturen wechseln kann.

**Lernziele**

- Verstehen der psychologischen Wirkungen von kühlen und warmen Farben.
- Erforschen, wie Lichttemperaturen die Stimmung und Umgebung beeinflussen.
- Lernen, wie RGB-LED-Farben mit Arduino angepasst werden, um verschiedene Lichttemperaturen zu simulieren.
- Praktische Fertigkeiten im Umgang mit der ``map()``-Funktion zur Übergangsgestaltung zwischen Farbtemperaturen entwickeln.


Aufbau der Schaltung
------------------------------------

**Benötigte Komponenten**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB-LED
     - 3 * 220Ω Widerstand
     - 1 * Potentiometer
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Jumper-Kabel
     -
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     -
     
**Aufbauschritte**

Diese Schaltung baut auf der aus Lektion 12 auf und fügt ein Potentiometer hinzu.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center

1. Entferne das Jumper-Kabel, das den GND-Pin des Arduino Uno R3 mit dem GND-Pin der RGB-LED verbindet, und stecke es in den negativen Anschluss des Steckbretts. Verbinde dann ein Jumper-Kabel vom negativen Anschluss zum GND-Pin der RGB-LED.

.. image:: img/15_cool_warm_color_gnd.png
    :width: 500
    :align: center

2. Stecke das Potentiometer in die Löcher 25G, 26F und 27G.

.. image:: img/15_cool_warm_color_pot.png
    :width: 500
    :align: center

3. Verbinde den mittleren Pin des Potentiometers mit dem A0-Pin des Arduino Uno R3.

.. image:: img/15_cool_warm_color_a0.png
    :width: 500
    :align: center

4. Verbinde schließlich den linken Pin des Potentiometers mit dem 5V-Pin des Arduino Uno R3 und den rechten Pin mit dem negativen Anschluss des Steckbretts.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center



Erstellung des Codes
-------------------------

**Warme und kühle Farben verstehen**

Bevor wir die Farbtemperatur anpassen, müssen wir die Unterschiede zwischen den RGB-Werten für kühle und warme Farben verstehen.

Die Wahrnehmung von Wärme in der Beleuchtung ist zwar subjektiv, doch eindeutig sollten warme Farben in Richtung Orange-Rot tendieren, während kühle Farben eher in Richtung Blau gehen.

1. Öffne **Paint** oder ein beliebiges Farbwahlwerkzeug, finde die wärmsten und kühlsten Farben, die du dir vorstellen kannst, und notiere ihre RGB-Werte in deinem Notizbuch.
.. note::

    Beachten Sie, dass Sie vor der Auswahl einer Farbe die Lumen auf die richtige Position einstellen sollten.

.. list-table::
   :widths: 25 25 50 25
   :header-rows: 1

   * - Farbtyp
     - Rot
     - Grün
     - Blau
   * - Warme Farbe
     -
     -
     -
   * - Kühle Farbe
     -
     -
     -

2. Hier sind Beispiele für warme und kühle Farbtöne zusammen mit ihren RGB-Werten:

* Rot (Rot: 246, Grün: 52, Blau: 8)

.. image:: img/15_mix_color_tone_warm.png

* Hellblau (Rot: 100, Grün: 150, Blau: 255)

.. image:: img/15_mix_color_tone_cool.png

Der Hauptunterschied zwischen warmen und kühlen Farben ist das Verhältnis der Intensitäten der drei Primärfarben. Als Nächstes speichern wir diese warmen und kühlen RGB-Werte in unserem Sketch.

3. Öffnen Sie den Sketch, den Sie zuvor gespeichert haben, ``Lesson13_PWM_Color_Mixing``.

4. Wählen Sie „Speichern unter...“ im „Datei“-Menü und benennen Sie ihn in ``Lesson15_Cool_Warm_Color`` um. Klicken Sie auf „Speichern“.

5. Deklarieren Sie vor dem ``void setup()`` sechs Variablen, um die RGB-Werte für diese beiden Farben zu speichern. Verwenden Sie die von Ihnen ausgewählten Farben.

.. code-block:: Arduino
    :emphasize-lines: 1-4,6-9

    // RGB-Werte für eine warme Farbe
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // RGB-Werte für eine kühle Farbe
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Blauen Pin der RGB-LED als Ausgang festlegen
        pinMode(10, OUTPUT);  // Grünen Pin der RGB-LED als Ausgang festlegen
        pinMode(11, OUTPUT);  // Roten Pin der RGB-LED als Ausgang festlegen
    }

**Die map() Funktion verwenden**

Um von warmer zu kühler Beleuchtung zu wechseln, müssen Sie lediglich die Intensität des roten Lichts reduzieren, das blaue Licht verstärken und die Intensität des grünen Lichts feinjustieren.

In früheren Projekten haben wir gelernt, wie man die Helligkeit der LED abhängig von der Drehung eines Potentiometers verändert.

In diesem Projekt führt jedoch die Drehung des Potentiometers dazu, dass sich die Intensitäten der RGB-Pins innerhalb eines bestimmten Bereichs ändern, was einfache Division unzureichend macht. Daher benötigen wir eine neue Funktion, ``map()``.

In der Arduino-Programmierung ist die ``map()``-Funktion äußerst nützlich, da sie es Ihnen ermöglicht, einen Zahlenbereich auf einen anderen Bereich zu übertragen (oder zu "mappen").

So wird sie verwendet:

* ``map(value, fromLow, fromHigh, toLow, toHigh)``: Ordnet eine Zahl von einem Bereich einem anderen zu. Ein Wert von ``fromLow`` wird auf ``toLow`` abgebildet, ein Wert von ``fromHigh`` auf ``toHigh``, und Werte dazwischen entsprechend.

    **Parameter**
        * ``value``: die Zahl, die abgebildet werden soll.
        * ``fromLow``: die untere Grenze des aktuellen Bereichs des Wertes.
        * ``fromHigh``: die obere Grenze des aktuellen Bereichs des Wertes.
        * ``toLow``: die untere Grenze des Zielbereichs.
        * ``toHigh``: die obere Grenze des Zielbereichs.

    **Rückgabewert**
        Der abgebildete Wert. Datentyp: long.

Die ``map()``-Funktion skaliert einen Wert von seinem ursprünglichen Bereich (fromLow bis fromHigh) auf einen neuen Bereich (toLow bis toHigh). Zuerst wird die Position des ``value`` innerhalb seines ursprünglichen Bereichs berechnet, dann wird diese Position proportional auf den neuen Bereich übertragen.

.. image:: img/15_map_pic.png
    :width: 400
    :align: center

So kann sie mit der unten gezeigten Formel geschrieben werden:

.. code-block::

    (value-fromLow)/(fromHigh-fromLow) = (y-toLow)/(toHigh-toLow)

Mit Algebra können Sie diese Gleichung umstellen, um ``y`` zu berechnen:

.. code-block::

    y = (value-fromLow) * (toHigh-toLow) / (fromHigh-fromLow) + toLow

.. image:: img/15_map_format.png

Beispielsweise ergibt ``y = map(value, 0, 1023, 246, 100);``, wenn ``value`` 434 beträgt, ``y = (434-0) * (100 - 246) / (1023-0) + 246``, was ungefähr 152 ergibt.


6. Entfernen Sie den ursprünglichen Code in ``void loop()``, und schreiben Sie dann den Code, um den Potentiometerwert auszulesen und ihn in der Variablen ``potValue`` zu speichern.

.. code-block:: Arduino

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Wert des Potentiometers auslesen
    }

7. Verwenden Sie dann die ``map()``-Funktion, um den Potentiometerwert von 0~1023 auf den Bereich 255 (``warm_r``) ~ 100 (``cool_r``) zu mappen.

.. code-block:: Arduino

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Wert des Potentiometers auslesen
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Potentiometerwert auf Rot-Intensität mappen
    }

8. Sie können den seriellen Monitor verwenden, um den ``potValue`` und den gemappten Wert ``value_r`` anzuzeigen, um Ihr Verständnis der ``map()``-Funktion zu vertiefen. Starten Sie nun den seriellen Monitor in ``void setup()``.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Blauen Pin der RGB-LED als Ausgang festlegen
        pinMode(10, OUTPUT);  // Grünen Pin der RGB-LED als Ausgang festlegen
        pinMode(11, OUTPUT);  // Roten Pin der RGB-LED als Ausgang festlegen
        Serial.begin(9600);        // Serielle Kommunikation mit 9600 Baudrate starten
    }

9. Gib die Variablen ``potValue`` und ``value_r`` in derselben Zeile aus, getrennt durch ein "|".

.. code-block:: Arduino
    :emphasize-lines: 23-26

    // RGB-Werte für eine warme Farbe
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // RGB-Werte für eine kühle Farbe
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Einmalige Initialisierung des Systems:
        pinMode(9, OUTPUT);   // Setzt den blauen Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setzt den grünen Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setzt den roten Pin der RGB-LED als Ausgang
        Serial.begin(9600);        // Seriellen Kommunikationskanal mit 9600 Baudrate einrichten
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Wert des Potentiometers lesen
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Potentiometerwert auf Rot-Intensität abbilden
        Serial.print(potValue);
        Serial.print(" | ");
        Serial.println(value_r);
        delay(500);  // 500 ms warten
    }

    // Funktion, um die Farbe der RGB-LED festzulegen
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // PWM-Wert auf den roten Pin schreiben
        analogWrite(10, green);  // PWM-Wert auf den grünen Pin schreiben
        analogWrite(9, blue);    // PWM-Wert auf den blauen Pin schreiben
    }

10. Nun können Sie den Code verifizieren und hochladen, den seriellen Monitor öffnen, und Sie werden zwei Spalten mit gedruckten Daten sehen.

.. code-block::

    434 | 152
    435 | 152
    434 | 152
    434 | 152
    434 | 152
    434 | 152

An den Daten ist erkennbar, dass die Position des Wertes 434 im Bereich von 0 bis 1023 der Position des Wertes 152 im Bereich von 246 bis 100 entspricht.


**Anpassung der Farbtemperatur**

Hier verwenden wir die Funktion ``map()``, um die Intensität der drei Pins der RGB-LED durch Drehen des Potentiometers zu verändern, sodass die Farben von den wärmsten zu den kältesten Tönen übergehen.
Konkret wird im Beispiel mit den von mir angegebenen Referenzwerten beim Drehen des Potentiometers der R-Wert der RGB-LED allmählich von 246 auf 100 geändert, der G-Wert von 8 auf 150 (obwohl die Veränderung des G-Werts kaum sichtbar ist) und der B-Wert allmählich von 8 auf 255.


11. Als nächstes benötigen wir die serielle Ausgabe vorübergehend nicht, da diese den gesamten Codeprozess beeinflussen kann. Verwenden Sie daher ``Ctrl +/``, um den entsprechenden Code auszukommentieren.

    .. note::

        Der Grund, warum wir den Code nicht direkt löschen, ist, dass Sie bei Bedarf die Ausgabe einfach wieder aktivieren können, indem Sie die Zeilen markieren und mit ``Ctrl+/`` auskommentieren.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Wert des Potentiometers lesen
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Potentiometerwert auf Rot-Intensität abbilden
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // 500 ms warten
    }

12. Fahren Sie fort, die Funktion ``map()`` aufzurufen, um basierend auf dem Potentiometerwert die zugeordneten ``value_g`` und ``value_b`` zu erhalten.

.. code-block:: Arduino
    :emphasize-lines: 9,10

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Wert des Potentiometers lesen
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Potentiometerwert auf Rot-Intensität abbilden
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // 500 ms warten
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Potentiometerwert auf Grün-Intensität abbilden
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Potentiometerwert auf Blau-Intensität abbilden
    }

13. Rufe abschließend die Funktion ``setColor()`` auf, um die abgebildeten RGB-Werte auf der RGB-LED anzuzeigen.

.. code-block:: Arduino
    :emphasize-lines: 11,12

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Wert des Potentiometers lesen
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Potentiometerwert auf Rot-Intensität abbilden
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // 500 ms warten
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Potentiometerwert auf Grün-Intensität abbilden
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Potentiometerwert auf Blau-Intensität abbilden
        setColor(value_r, value_g, value_b);                   // Farbe der LED einstellen
        delay(500);
    }

14. Der vollständige Code ist wie folgt. Sie können nun auf den "Upload"-Button klicken, um den Code auf den Arduino Uno R3 hochzuladen. Anschließend können Sie das Potentiometer drehen und sehen, wie die RGB-LED allmählich von einem kühlen zu einem warmen Farbton übergeht oder umgekehrt.

.. code-block:: Arduino

    // RGB-Werte für eine warme Farbe
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // RGB-Werte für eine kühle Farbe
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Einmalige Initialisierung des Systems:
        pinMode(9, OUTPUT);   // Setzt den blauen Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setzt den grünen Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setzt den roten Pin der RGB-LED als Ausgang
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Wert des Potentiometers lesen
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Potentiometerwert auf Rot-Intensität abbilden
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // 500 ms warten
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Potentiometerwert auf Grün-Intensität abbilden
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Potentiometerwert auf Blau-Intensität abbilden
        setColor(value_r, value_g, value_b);                   // Farbe der LED einstellen
        delay(500);                                            // 500 ms warten
    }

    // Funktion, um die Farbe der RGB-LED einzustellen
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // PWM-Wert auf den roten Pin schreiben
        analogWrite(10, green);  // PWM-Wert auf den grünen Pin schreiben
        analogWrite(9, blue);    // PWM-Wert auf den blauen Pin schreiben
    }

15. Speichern Sie abschließend Ihren Code und räumen Sie Ihren Arbeitsbereich auf.

**Tipps**

Während des Experiments stellen Sie möglicherweise fest, dass der Übergang zwischen warmen und kühlen Farbtönen nicht so deutlich sichtbar ist wie auf dem Bildschirm. Zum Beispiel kann ein erwartetes warmes Licht weiß erscheinen. Dies ist normal, da das Farbmischen in einer RGB-LED nicht so fein ist wie auf einem Display.

In solchen Fällen können Sie die Intensität der G- und B-Werte bei der warmen Farbe verringern, um eine passendere Farbgebung auf der RGB-LED zu erzielen.

**Frage**

Beachten Sie, dass die "unteren Grenzen" eines Bereichs größer oder kleiner als die "oberen Grenzen" sein können, sodass die Funktion ``map(value, fromLow, fromHigh, toLow, toHigh)`` auch verwendet werden kann, um einen Zahlenbereich umzukehren, zum Beispiel:

.. code-block::

    y = map(x, 1, 50, 50, 1);

Die Funktion funktioniert auch gut mit negativen Zahlen, sodass dieses Beispiel ebenfalls gültig ist:

.. code-block::

    y = map(x, 1, 50, 50, -100);

Für ``y = map(x, 1, 50, 50, -100);``, wenn ``x`` gleich 20 ist, was sollte ``y`` sein? Verwenden Sie die folgende Formel, um es zu berechnen.

.. image:: img/15_map_format.png

