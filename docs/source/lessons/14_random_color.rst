.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in Raspberry Pi, Arduino und ESP32 ein, zusammen mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Vorschauen.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu experimentieren und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

14. Zufällige Farben
========================

Manchmal braucht das Leben eine Prise Überraschung. Wenn du unentschlossen bist, lass das Zufallsprinzip die Führung übernehmen. Diese Lektion zeigt dir, wie du eine RGB-LED in zufälligen Farben aufleuchten lassen kannst – perfekt, wenn du deinen Projekten eine unvorhersehbare Note verleihen möchtest.

Aufbau der Schaltung
-------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB-LED
     - 3 * 220Ω Widerstand
     - Jumper-Kabel
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
     
Diese Lektion verwendet denselben Schaltungsaufbau wie in Lektion 12.

.. image:: img/12_mix_color_bb_4.png
    :width: 600
    :align: center

Erstellung des Codes
------------------------

In den vorherigen Lektionen hast du die RGB-LED dazu gebracht, gewünschte Farben anzuzeigen. Doch manchmal möchtest du vielleicht keine spezifische Farbe, sondern eine zufällige Farbe, ähnlich wie Bühnenlichter. Wie kann das umgesetzt werden?

**Kennst du die random()-Funktionen?**

In der physischen Welt gibt es überall Zufälligkeiten, aber in der Programmierung werden sogenannte "zufällige" Zahlen meist durch einen deterministischen Algorithmus berechnet. Dieser Algorithmus benötigt in der Regel einen Startpunkt, der als "Seed" bezeichnet wird, wodurch diese Zahlen vorhersagbar werden und somit "Pseudorandom" genannt werden. Das "Pseudo" deutet darauf hin, dass diese Zahlen zufällig erscheinen, jedoch einem Muster folgen.

Interessanterweise können wir auf einem Arduino Uno R3 physikalische Messungen aus der realen Welt als Seed verwenden. Wenn du mit einem Multimeter misst, bemerkst du möglicherweise leichte Schwankungen in den Spannungs- und Stromwerten des Schaltkreises. Diese Schwankungen können unseren Zufallszahlen eine gewisse Unvorhersehbarkeit verleihen.

Arduinos Ansatz für Zufälligkeiten beinhaltet mehrere Funktionen:

* ``randomSeed();``: Initialisiert den Startwert des Zufallszahlengenerators. Diese Funktion sorgt dafür, dass der Startpunkt der Zufallszahlenfolge bei jedem Programmlauf unterschiedlich ist und so verschiedene Zahlenfolgen erzeugt werden.

    **Parameter**
        * ``seed``: Ein Wert, der zum Initialisieren des Zufallszahlengenerators verwendet wird. Dieser Wert vom Typ unsigned long bestimmt den Startpunkt der Zufallsfolge.
    **Rückgabewert**
        Keiner.

* ``long random(long max);``: Erzeugt eine Zufallszahl innerhalb eines bestimmten Bereichs.

    **Parameter**
        ``max``: Die Obergrenze der Zufallszahl (``max`` selbst ist nicht inbegriffen), d.h. die Zufallszahl liegt zwischen 0 (einschließlich) und ``max-1`` (einschließlich).
    
    **Rückgabewert**
        Eine Zahl vom Typ long zwischen 0 und max-1.

* ``long random(long min, long max);``: Erzeugt eine Zufallszahl innerhalb eines bestimmten Bereichs.

    **Parameter**
        ``min``: Die Untergrenze der Zufallszahl (einschließlich).
        ``max``: Die Obergrenze der Zufallszahl (``max`` selbst ist nicht inbegriffen), d.h. die Zufallszahl liegt zwischen min (einschließlich) und max-1 (einschließlich).
    
    **Rückgabewert**
        Eine Zahl vom Typ long zwischen min und max-1.

**Den Code schreiben**

1. Öffne den Sketch, den du zuvor gespeichert hast, ``Lesson13_PWM_Color_Mixing``. 

2. Wähle „Speichern unter...“ im „Datei“-Menü und benenne den Sketch um in ``Lesson14_Random_Colors``. Klicke auf „Speichern“.

3. Rufe ``randomSeed()`` nur einmal in ``void setup()`` auf, um den Seed zu initialisieren. Verwende keinen festen Seed-Wert, da dies dazu führen würde, dass bei jedem Programmlauf dieselbe Zahlenfolge erzeugt wird.

    Wir verwenden ``analogRead(A0)``, um den Wert eines nicht angeschlossenen analogen Pins zu lesen. Da dieser Pin nicht verbunden ist, empfängt er Rauschen, das bei jeder Messung variiert und somit einen guten Seed für ``randomSeed()`` liefert.

.. code-block:: Arduino
    :emphasize-lines: 9

    void setup() {
        // Einmaliger Setup-Code:
        pinMode(9, OUTPUT);   // Blauen Pin der RGB-LED als Ausgang festlegen
        pinMode(10, OUTPUT);  // Grünen Pin der RGB-LED als Ausgang festlegen
        pinMode(11, OUTPUT);  // Roten Pin der RGB-LED als Ausgang festlegen
            
        // Initialisierung des Zufalls-Seeds basierend auf einem nicht verbundenen analogen Pin
        // Dies sorgt für unterschiedliche Zufallszahlenfolgen bei jedem Reset
        randomSeed(analogRead(A0));
    }

4. Entferne nun im ``void loop()`` den ursprünglichen Code. Verwende die Funktion ``random()``, um zufällige Werte zu generieren, die in den Variablen ``redValue``, ``greenValue`` und ``blueValue`` gespeichert werden.

.. code-block:: Arduino
    :emphasize-lines: 3-5

    void loop(){
        // Zufällige Werte für jede Farbkomponente generieren
        int redValue = random(0, 256);   // Zufälliger Wert zwischen 0 und 255
        int greenValue = random(0, 256); // Zufälliger Wert zwischen 0 und 255
        int blueValue = random(0, 256);  // Zufälliger Wert zwischen 0 und 255
    }

5. Gib die generierten RGB-Werte in die Funktion ``setColor()`` ein, um die RGB-LED zum Leuchten zu bringen. Verwende auch die Funktion ``delay()``, um festzulegen, wie lange die Farbe angezeigt wird.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        // Zufällige Werte für jede Farbkomponente zwischen 0 und 255 generieren
        int redValue = random(0, 256);    // Zufälligen Rotwert generieren
        int greenValue = random(0, 256);  // Zufälligen Grünwert generieren
        int blueValue = random(0, 256);   // Zufälligen Blauwert generieren

        // Die zufälligen Farbwerte auf die RGB-LED anwenden
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // 1 Sekunde warten
    }


6. Dein vollständiger Code ist nun bereit. Du kannst ihn auf das Arduino Uno R3 hochladen, und die RGB-LED zeigt jede Sekunde eine zufällige Farbe an.

.. code-block:: Arduino
    :emphasize-lines: 19,20

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Blauen Pin der RGB-LED als Ausgang festlegen
        pinMode(10, OUTPUT);  // Grünen Pin der RGB-LED als Ausgang festlegen
        pinMode(11, OUTPUT);  // Roten Pin der RGB-LED als Ausgang festlegen
        
        // Initialisierung des Zufalls-Seeds basierend auf einem nicht verbundenen analogen Pin
        // Dies sorgt für unterschiedliche Zufallszahlenfolgen bei jedem Reset
        randomSeed(analogRead(A0));
    }

    void loop() {
        // Zufällige Werte für jede Farbkomponente zwischen 0 und 255 generieren
        int redValue = random(0, 256);    // Zufälligen Rotwert generieren
        int greenValue = random(0, 256);  // Zufälligen Grünwert generieren
        int blueValue = random(0, 256);   // Zufälligen Blauwert generieren

        // Die zufälligen Farbwerte auf die RGB-LED anwenden
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // 1 Sekunde warten
    }

    // Funktion, um die Farbe der RGB-LED festzulegen
    void setColor(int red, int green, int blue) {
        // PWM-Wert für Rot, Grün und Blau auf die RGB-LED schreiben
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

7. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Frage**

1. Wenn du den Code von ``randomSeed(analogRead(A0))`` auf ``randomSeed(0)`` änderst, wie werden sich die Farben der RGB-LED ändern und warum?

2. In welchen Situationen wird Zufälligkeit im Alltag zur Problemlösung eingesetzt, abgesehen von der zufälligen Auswahl von Farben zur Dekoration und dem Ziehen von Lotteriezahlen?

**Zusammenfassung**

Am Ende dieser Lektion wirst du nicht nur gelernt haben, wie Zufälligkeit in der Programmierung funktioniert und wie du sie manipulieren kannst, um lebendige, unerwartete visuelle Effekte zu erzeugen, sondern auch die einfache Schönheit der Zufälligkeit im Alltag schätzen gelernt haben. Programmierung kann so unvorhersehbar sein wie das Leben selbst, und mit den richtigen Werkzeugen kannst du diese Unvorhersehbarkeit auf kreative und funktionale Weise nutzen.
