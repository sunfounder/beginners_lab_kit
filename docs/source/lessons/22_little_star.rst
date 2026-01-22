.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein, gemeinsam mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Sonderrabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Aktionen zu Feiertagen teil.

    👉 Bereit, mit uns zu erkunden und zu erschaffen? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

22. Spiele "Twinkle, Twinkle, Little Star"
===============================================
In dieser Lektion tauchen wir in die faszinierende Verbindung von Musik und Technologie ein. Du wirst lernen, wie unterschiedliche Tonhöhen durch Frequenzänderungen erzeugt werden und wie dieses Prinzip mithilfe eines Mikrocontrollers wie Arduino zur Steuerung eines Summers angewendet werden kann. Am Ende dieser Lektion wirst du nicht nur die Grundlagen musikalischer Frequenzen verstehen, sondern auch in der Lage sein, ein Arduino zu programmieren, das eine einfache Melodie abspielt.

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/22_little_star.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:

* Lernen, wie musikalische Tonhöhen bestimmten Frequenzen entsprechen.
* Das Programmieren vereinfachen, indem du Arrays verwendest, um musikalische Noten zu speichern und zu manipulieren.
* Ein Programm schreiben und ausführen, das einen passiven Summer steuert, um "Twinkle, Twinkle, Little Star" abzuspielen.

Musikalische Frequenzen und Klangerzeugung
----------------------------------------------
.. image:: img/7_sound.png
  :width: 400
  :align: center

Verschiedene Musikinstrumente erzeugen unterschiedliche Tonhöhen durch Änderung der Frequenz.
Zum Beispiel bewirkt das Anschlagen der Tasten eines Klaviers, dass die entsprechenden Saiten schnell vibrieren und spezifische Tonhöhen erzeugen.
Wissenschaftler und Musiker haben verschiedene Methoden zur Musikstimmung und Tonhöhenstandards entwickelt, indem sie diese Schwingungsfrequenzen genau messen.

Wenn du ein Arduino oder einen anderen Mikrocontroller steuerst, um ein elektrisches Signal an einen Summer zu senden, vibriert die Membran des Summers schnell entsprechend der Frequenz des Signals und erzeugt so einen Ton. Ein Signal, das auf 440 Hz eingestellt ist, erzeugt zum Beispiel den Standardton "A4", der als Referenzpunkt in der Musikstimmung dient.
Je nach Erhöhung oder Verringerung der Frequenz steigt oder sinkt die erzeugte Tonhöhe, wodurch in der musikalischen Komposition ein Bereich von tiefen bis hohen Tönen erreicht wird.

In der westlichen Musik umfasst eine Oktave 12 Halbtöne, von C bis B, und kehrt dann zu einem höheren C zurück.

Zum Beispiel liegt die Frequenz des mittleren C (C4) bei etwa 261,63 Hz. Die Frequenz eines Tons kann mithilfe der folgenden Formel berechnet werden:

.. image:: img/7_music_format.png

wobei f_0 der Referenzton (meist A4 mit einer Frequenz von 440 Hz) ist und n die Anzahl der Halbtöne vom Referenzton zum Zielton angibt (positive Zahlen bedeuten eine Erhöhung, negative eine Verringerung).
Mit dieser Formel können wir die Frequenz jedes Tons berechnen.

Hier ist eine Tabelle mit Frequenzen:

* C (C4): 262 Hz (actually close to 261.63 Hz, rounded to 262)
* D (D4): 294 Hz
* E (E4): 330 Hz
* F (F4): 349 Hz
* G (G4): 392 Hz
* A (A4): 440 Hz
* B (B4): 494 Hz

Nun werden wir die Geheimnisse der Noten mithilfe eines Arduino und eines Summers erforschen. Lass uns den passiven Summer die ersten zwei Zeilen von "Twinkle, Twinkle, Little Star" spielen lassen:

.. note::

  Die Melodie von "Twinkle, Twinkle, Little Star" basiert auf einfachen Notenkombinationen,
  und die Melodie dieses Liedes ist eine Variation von "Ah vous dirai-je, Maman" des französischen Komponisten Wolfgang Amadeus Mozart,
  was sie besonders für Anfänger geeignet macht.

  Hier ist die Grundpartitur von "Twinkle, Twinkle, Little Star", die jede Note enthält:

  .. code-block:: 

    C C G G A A G
    F F E E D D C
    G G F F E E D
    G G F F E E D
    C C G G A A G
    F F E E D D C

Aufbau des Schaltkreises
----------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Breadboard
     - 1 * Passiver Summer
     - Jumper-Kabel
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_passive_buzzer| 
     - |list_wire| 
   * - 1 * USB-Kabel
     -
     - 
     - 
   * - |list_usb_cable| 
     -
     - 
     - 



**Schritt-für-Schritt-Aufbau**

Diese Lektion verwendet denselben Schaltkreis wie Lektion 21.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Codeerstellung - Array
--------------------------
1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „File“ „New Sketch“ auswählst.
2. Speichere deinen Sketch als ``Lesson22_Array`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Erstelle nun am Anfang des Codes ein Array, in dem die Noten von "Twinkle Twinkle Little Star" gespeichert werden.

.. code-block:: Arduino

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit dem mittleren C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // High C

  // Definiere ein Array, das die Notenfolge der Melodie enthält
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

Ein Array ist eine Datenstruktur, die in der Arduino-Programmierung verwendet wird, um mehrere Elemente desselben Typs zu speichern.
Es ist ein sehr grundlegendes und leistungsstarkes Werkzeug, und wenn es richtig eingesetzt wird, kann es die Programmier-Effizienz und die Leistung erheblich verbessern.
Arrays können Elemente wie Ganzzahlen, Fließkommazahlen und Zeichen speichern.

Ähnlich wie bei der Erstellung von Variablen und Funktionen erfordert auch das Erstellen eines Arrays die Angabe des Array-Typs und des Array-Namens - ``int melody[]``.

Die Elemente innerhalb der geschweiften Klammern ``{}`` werden als Array-Elemente bezeichnet, beginnend bei Index 0. Das heißt, ``melody[0]`` entspricht dem ersten ``c(262)``, und ``melody[13]`` ist ebenfalls ``c(262)``.

4. Gib nun die Elemente an den Indizes 0 und 13 aus dem Array ``melody[]`` im seriellen Monitor aus.

.. code-block:: Arduino
  :emphasize-lines: 17,18

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit dem mittleren C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Hohes C

  // Definiere ein Array, das die Notenfolge der Melodie enthält
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

  void setup() {
    // Setup-Code, der einmal ausgeführt wird:
    Serial.begin(9600);  // Initialisiere die serielle Kommunikation mit 9600 Baud
    Serial.println(melody[0]);
    Serial.println(melody[13]);
  }
  
  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
  }

5. Nachdem du den Code auf das Arduino Uno R3 hochgeladen hast, öffne den seriellen Monitor und du wirst zwei Mal 262 sehen.

.. code-block::

  262
  262

6. Wenn du jedes Element im Array ``melody[]`` einzeln ausgeben möchtest, musst du zuerst die Länge des Arrays kennen. Du kannst die Funktion ``sizeof()`` verwenden, um die Anzahl der Elemente im Array zu berechnen.

.. code-block:: Arduino
  :emphasize-lines: 4

  void setup() {
    // Setup-Code, der einmal ausgeführt wird:
    Serial.begin(9600);  // Initialisiere die serielle Kommunikation mit 9600 Baud
    int notes = sizeof(melody) / sizeof(melody[0]); // Berechne die Anzahl der Elemente
  }

  
* ``sizeof(melody)`` gibt die Gesamtzahl der Bytes an, die von allen Elementen im Array verwendet werden.
* ``sizeof(melody[0])`` gibt die Anzahl der Bytes an, die von einem Element des Arrays verwendet werden.
* Wenn du die Gesamtzahl der Bytes durch die Bytes pro Element teilst, erhältst du die Gesamtanzahl der Elemente im Array.

7. Verwende dann eine ``for``-Schleife, um die Elemente im Array ``melody[]`` nacheinander durchzugehen und mit der Funktion ``Serial.println()`` auszugeben.

.. code-block:: Arduino

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit dem mittleren C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Hohes C

  // Definiere ein Array, das die Notenfolge der Melodie enthält
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };


  void setup() {
    // Setup-Code, der einmal ausgeführt wird:
    Serial.begin(9600);                              // Initialisiere die serielle Kommunikation mit 9600 Baud
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Array melody
    for (int i = 0; i < notes; i = i + 1) {
      // Gib die Frequenz jeder Note im seriellen Monitor aus
      Serial.println(melody[i]);
    }
  }

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
  }

8. Nachdem du den Code auf das Arduino Uno R3 hochgeladen hast, öffne den seriellen Monitor, und du wirst sehen, wie die Elemente des Arrays ``melody[]`` nacheinander ausgegeben werden.

.. code-block::

  262
  262
  392
  392
  440
  440
  392
  349
  349
  330
  ...

**Fragen**

Du kannst auch Berechnungen mit den Elementen im Array durchführen, z. B. durch Ändern zu ``Serial.println(melody[i] * 1.3);``. Welche Werte erhältst du und warum?


Codeerstellung - "Twinkle, Twinkle, Little Star" spielen 
-------------------------------------------------------------

Nun, da wir ein solides Verständnis für das Erstellen von Arrays, den Zugriff auf Array-Elemente und deren Längen- und Operationsberechnungen haben, wenden wir dieses Wissen an, um einen passiven Summer zu programmieren, der „Twinkle, Twinkle, Little Star“ mit gespeicherten Frequenzen und Intervallen abspielt.

1. Öffne den zuvor gespeicherten Sketch ``Lesson22_Array``.

2. Wähle im Menü „Datei“ die Option „Speichern unter...“ und benenne die Datei in ``Lesson22_Little_Star`` um. Klicke auf „Speichern“.


3. Definiere zuerst den Pin für den Summer.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Weist Pin 9 der Konstanten für den Summer zu


4. Erstelle nun ein weiteres Array, um die Dauer der Noten zu speichern.

.. code-block:: Arduino
  :emphasize-lines: 3

  // Lege die Notenfolge und deren Dauer in Millisekunden fest
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

5. Verschiebe nun einen Teil des Codes von ``void setup()`` in ``void loop()``.

.. code-block:: Arduino
  :emphasize-lines: 8-13

  void setup() {
    // Setup-Code, der einmal ausgeführt wird:
    Serial.begin(9600);                              // Initialisiere die serielle Kommunikation mit 9600 Baud
  }

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Array melody
    for (int i = 0; i < notes; i = i + 1) {
      // Gib die Frequenz jeder Note im seriellen Monitor aus
      Serial.println(melody[i]);
    }
  }

6. Kommentiere in der ``for``-Schleife den Code zum Ausdrucken aus und verwende die Funktion ``tone()``, um die Noten abzuspielen.

.. code-block:: Arduino
  :emphasize-lines: 9

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Array melody
    for (int i = 0; i < notes; i = i + 1) {
      // Gib die Frequenz jeder Note im seriellen Monitor aus
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note ab
    }
  }

7. Nachdem jede Note abgespielt wurde, solltest du, um die Melodie natürlicher klingen zu lassen, eine kurze Pause zwischen den Noten einfügen. Hier multiplizieren wir die Dauer der Noten mit 1,30, um das Intervall zu berechnen, damit die Melodie weniger gehetzt klingt.

.. code-block:: Arduino
  :emphasize-lines: 10

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Array melody
    for (int i = 0; i < notes; i = i + 1) {
      // Gib die Frequenz jeder Note im seriellen Monitor aus
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note
      delay(noteDurations[i] * 1.30);                // Warte, bevor die nächste Note gespielt wird
    }
  }

8. Verwende die Funktion ``noTone()``, um den Ton des aktuellen Pins zu stoppen. Dieser Schritt ist notwendig, um sicherzustellen, dass jede Note klar gespielt wird und nicht mit der nächsten verschmilzt.

.. code-block:: Arduino
  :emphasize-lines: 11

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Array melody
    for (int i = 0; i < notes; i = i + 1) {
      // Gib die Frequenz jeder Note im seriellen Monitor aus
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note
      delay(noteDurations[i] * 1.30);                // Warte, bevor die nächste Note gespielt wird
      noTone(buzzerPin);                             // Stoppe die Wiedergabe der Note
    }
  }

9. Dein vollständiger Code wird unten angezeigt. Sobald du den Code auf das Arduino Uno R3 hochgeladen hast, wirst du den Summer "Twinkle Twinkle Little Star" spielen hören.

.. code-block:: Arduino

  int buzzerPin = 9;  // Weist Pin 9 der Konstanten für den Summer zu

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit dem mittleren C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Hohes C

  // Lege die Notenfolge und deren Dauer in Millisekunden fest
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

  void setup() {
    // Setup-Code, der einmal ausgeführt wird:
    Serial.begin(9600);                              // Initialisiere die serielle Kommunikation mit 9600 Baud
  }

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Array melody
    for (int i = 0; i < notes; i = i + 1) {
      // Gib die Frequenz jeder Note im seriellen Monitor aus
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note
      delay(noteDurations[i] * 1.30);                // Warte, bevor die nächste Note gespielt wird
      noTone(buzzerPin);                             // Stoppe die Wiedergabe der Note
    }
  }
  
10. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Frage**

Wenn du den passiven Summer im Schaltkreis durch einen aktiven Summer ersetzt, kannst du dann „Twinkle Twinkle Little Star“ abspielen? Warum?

**Zusammenfassung**

Nun, da die Lektion vorbei ist, haben wir in dieser Stunde gelernt, wie man Arrays verwendet, um Daten zu speichern, Array-Längen zu berechnen, Elemente innerhalb eines Arrays zu indizieren und Operationen auf jedem Element durchzuführen. Indem wir Notenfrequenzen und Zeitintervalle in Arrays gespeichert und diese mithilfe einer for-Schleife durchlaufen haben, konnten wir erfolgreich einen passiven Summer programmieren, um „Twinkle, Twinkle, Little Star“ abzuspielen.

Darüber hinaus haben wir gelernt, wie man die Wiedergabe einer Note mit der Funktion ``noTone()`` unterbricht.

Diese Lektion hat nicht nur unser Verständnis von Array-Operationen und Kontrollstrukturen in der Programmierung vertieft, sondern auch gezeigt, wie diese Konzepte genutzt werden können, um mit elektronischen Bauteilen Musik zu erzeugen und theoretisches Wissen mit praktischen Anwendungen auf unterhaltsame Weise zu verknüpfen.
