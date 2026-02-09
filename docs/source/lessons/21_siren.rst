.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Sneak Peeks.
    - **Sonderrabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu erkunden und zu erschaffen? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

21. Sirenenton
=========================

In diesem Arduino-Projekt erkunden wir, wie man ein Sirenensystem durch Programmierung und Integration von elektronischer Hardware erstellt.

Sirenenklänge verwenden ein spezifisches Frequenz- und Tonmuster, das durch schnelle Anstiege und Abfälle der Tonhöhe gekennzeichnet ist. Dies macht sie nicht nur leicht erkennbar, sondern unterscheidet sie auch von anderen alltäglichen Geräuschen. Diese Tonhöhenwechsel erzeugen oft ein Gefühl der Dringlichkeit, da sie in der Natur häufig mit Warnsignalen oder gefährlichen Situationen in Verbindung gebracht werden.

Durch die Anpassung der Frequenz eines passiven Summers können wir die charakteristischen auf- und absteigenden Tonhöhen eines Sirenentons simulieren.

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="../_static/video/21_siren_sound.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion lernst du:

* Wie passive Summer funktionieren
* Wie man einen passiven Summer mit der tone()-Funktion ansteuert
* Wie man die for-Schleife in der Programmierung verwendet
* Wie man einen Sirenenton umsetzt

Verständnis der Klangeigenschaften
---------------------------------------

Schall ist ein Wellenphänomen, das sich als vibrierende Energie durch Medien wie Luft, Wasser oder Feststoffe ausbreitet. Das Verständnis der physikalischen Eigenschaften von Schall hilft uns, besser zu begreifen, wie sich Schall in verschiedenen Umgebungen verhält.
Hier sind einige wichtige physikalische Eigenschaften von Schall:

.. image:: img/7_siren.png
    :width: 500
    :align: center

**Frequenz**

Die Frequenz bezieht sich auf die Anzahl der Schwingungszyklen pro Zeiteinheit, typischerweise in Hertz (Hz) angegeben.
Die Frequenz bestimmt die Tonhöhe des Klangs: Höhere Frequenzen klingen höher, tiefere Frequenzen klingen tiefer. Der hörbare Bereich des Menschen reicht ungefähr von 20 Hz bis 20.000 Hz.

**Amplitude**
Die Amplitude ist die Stärke der Schwingung einer Schallwelle, die die Lautstärke des Klangs bestimmt.
Eine größere Amplitude bedeutet einen lauteren Klang, eine kleinere Amplitude einen leiseren Klang.
In der Physik ist die Amplitude üblicherweise direkt mit der Energie einer Schallwelle verbunden, während wir im alltäglichen Sprachgebrauch oft Dezibel (dB) zur Beschreibung der Lautstärke verwenden.

**Klangfarbe**
Die Klangfarbe beschreibt die Textur oder „Farbe“ des Klangs, die es uns ermöglicht, Geräusche verschiedener Quellen zu unterscheiden, selbst wenn sie die gleiche Tonhöhe und Lautstärke haben.
Zum Beispiel können wir einen Unterschied zwischen einer Violine und einem Klavier erkennen, auch wenn beide das gleiche musikalische Stück spielen, dank ihrer unterschiedlichen Klangfarbe.

In diesem Projekt erforschen wir nur den Einfluss der Frequenz auf den Klang.



Aufbau des Schaltkreises
---------------------------

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

In den vorherigen Lektionen haben wir aktive Summer verwendet. In dieser Lektion verwenden wir einen passiven Summer. Der Schaltkreis ist derselbe, jedoch unterscheidet sich der Programmieransatz zur Ansteuerung.

1. Finde einen passiven Summer, der auf seiner Rückseite eine offene Platine hat.

.. image:: img/7_beep_2.png

2. Obwohl auf dem passiven Summer ein '+'-Zeichen zu sehen ist, handelt es sich nicht um ein polarisiertes Bauteil. Stecke ihn in beliebiger Richtung in die Löcher 15F und 18F des Breadboards.

.. image:: img/16_morse_code_buzzer.png
    :width: 500
    :align: center

3. Verbinde einen Pin des passiven Summers mit dem GND-Pin des Arduino Uno R3.

.. image:: img/16_morse_code_gnd.png
    :width: 500
    :align: center

4. Verbinde den anderen Pin des passiven Summers mit dem 5V-Pin des Arduino Uno R3. Der Summer wird keinen Ton von sich geben, was ihn von einem aktiven Summer unterscheidet, der in dieser Konfiguration einen Ton erzeugen würde.

.. image:: img/16_morse_code_5v.png
    :width: 500
    :align: center

5. Nun entferne das Kabel, das im 5V-Pin steckt, und stecke es in Pin 9 des Arduino Uno R3, damit der Summer mit Code gesteuert werden kann.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center



Code-Erstellung - Den passiven Summer ertönen lassen
---------------------------------------------------------

Wie wir beim Anschließen gelernt haben, reicht es nicht aus, einfach nur eine hohe oder niedrige Spannung an einen passiven Summer anzulegen, um einen Ton zu erzeugen. In der Arduino-Programmierung wird die Funktion ``tone()`` verwendet, um einen passiven Summer oder andere Audioausgabegeräte zu steuern und einen Ton mit einer bestimmten Frequenz zu erzeugen.

    * ``tone()``: Erzeugt eine Rechteckwelle mit der angegebenen Frequenz (und einem Tastverhältnis von 50%) an einem Pin. Eine Dauer kann angegeben werden, andernfalls läuft die Welle weiter, bis ``noTone()`` aufgerufen wird.

    **Syntax**

        * ``tone(pin, frequency)``
        * ``tone(pin, frequency, duration)``

    **Parameter**

        * ``pin``: Der Arduino-Pin, an dem der Ton erzeugt wird.
        * ``frequency``: Die Frequenz des Tons in Hertz. Erlaubte Datentypen: unsigned int.
        * ``duration``: Die Dauer des Tons in Millisekunden (optional). Erlaubte Datentypen: unsigned long.

    **Rückgabewert**
        Keiner


1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem Menü „File“ auswählst.
2. Speichere deinen Sketch als ``Lesson21_Tone`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Zuerst definierst du den Pin für den Summer.

.. code-block:: Arduino

    const int buzzerPin = 9;  // Weist Pin 9 der Konstanten für den Summer zu

    void setup() {
        // Hier den Setup-Code einfügen, um ihn einmal auszuführen:
    }

4. Um die Verwendung der ``tone()``-Funktion besser zu verstehen, schreiben wir sie in das ``void setup()``, sodass der Summer einen Ton mit einer bestimmten Frequenz für eine festgelegte Dauer abgibt.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;  // Weist Pin 9 der Konstanten für den Summer zu

    void setup() {
        // Hier den Setup-Code einfügen, um ihn einmal auszuführen:
        tone(buzzerPin, 1000, 100);  // Summer mit 1000 Hz für 100 Millisekunden einschalten
    }

    void loop() {
        // Hier den Hauptcode einfügen, um ihn wiederholt auszuführen:
    }

5. Jetzt kannst du den Code auf das Arduino Uno R3 hochladen, und du wirst einen kurzen "Piep"-Ton vom passiven Summer hören, danach wird er still.

**Fragen**

1. Wenn du die Pins des Codes und der Schaltung auf 7 oder 8 änderst, die keine PWM-Pins sind, wird der Summer dann trotzdem einen Ton abgeben? Du kannst es testen und deine Antwort ins Handbuch schreiben.

2. Um zu erkunden, wie ``frequency`` und ``duration`` in ``tone(pin, frequency, duration)`` den Ton des Summers beeinflussen, modifiziere den Code unter zwei Bedingungen und notiere die beobachteten Phänomene in deinem Handbuch:

* Bei Beibehaltung der ``frequency`` von 1000, erhöhe schrittweise die ``duration`` von 100, 500 auf 1000. Wie verändert sich der Ton des Summers und warum?

* Bei Beibehaltung der ``duration`` von 100, erhöhe schrittweise die ``frequency`` von 1000, 2000 auf 5000. Wie verändert sich der Ton des Summers und warum?



Code-Erstellung - Einen Sirenenton erzeugen
----------------------------------------------

Zuvor haben wir gelernt, wie man einen Summer zum Ertönen bringt, und verstanden, wie Frequenz und Dauer den Ton beeinflussen. Wenn wir nun möchten, dass der Summer einen Sirenenton erzeugt, der von einem tiefen zu einem hohen Ton ansteigt, wie sollten wir vorgehen?

Aus unseren früheren Erkundungen wissen wir, dass die Funktion ``tone(pin, frequency)`` es ermöglicht, einen passiven Summer zum Erklingen zu bringen. Durch schrittweises Erhöhen der ``frequency`` wird die Tonhöhe des Summers höher. Lass uns das nun im Code umsetzen.

1. Öffne den zuvor gespeicherten Sketch ``Lesson21_Tone``. 

2. Wähle im Menü „Datei“ die Option „Speichern unter...“ und benenne die Datei in ``Lesson21_Siren_Sound`` um. Klicke auf „Speichern“.

3. Schreibe die ``tone()``-Funktion in die ``void loop()`` und setze drei verschiedene Frequenzen. Um den Unterschied zwischen den Tönen deutlich zu hören, verwende die ``delay()``-Funktion, um sie zu trennen.

.. code-block:: Arduino

    const int buzzerPin = 9;  // Weist Pin 9 der Konstanten für den Summer zu

    void setup() {
        // Hier den Setup-Code einfügen, um ihn einmal auszuführen:
    }

    void loop() {
        // Hier den Hauptcode einfügen, um ihn wiederholt auszuführen:
        tone(buzzerPin, 100);  // Summer bei 100 Hz einschalten
        delay(500);
        tone(buzzerPin, 300);  // Summer bei 300 Hz einschalten
        delay(500);
        tone(buzzerPin, 600);  // Summer bei 600 Hz einschalten
        delay(500);
    }

4. An diesem Punkt kannst du den Code auf das Arduino Uno R3 hochladen, und du wirst den Summer hören, der drei verschiedene Töne wiederholt.

5. Um einen sanfteren Anstieg der Tonhöhe zu erreichen, sollten wir kürzere Intervalle für ``frequency`` setzen, zum Beispiel in Schritten von 10, beginnend bei 100, 110, 120... bis 1000. Wir können den folgenden Code schreiben.

.. code-block:: Arduino

    void loop() {
        // Hier den Hauptcode einfügen, um ihn wiederholt auszuführen:
        tone(buzzerPin, 100);  // Summer bei 100 Hz einschalten
        delay(500);
        tone(buzzerPin, 110);  // Summer bei 110 Hz einschalten
        delay(500);
        tone(buzzerPin, 120);  // Summer bei 120 Hz einschalten
        delay(500);
        tone(buzzerPin, 130);  // Summer bei 130 Hz einschalten
        delay(500);
        tone(buzzerPin, 140);  // Summer bei 140 Hz einschalten
        delay(500);
        tone(buzzerPin, 150);  // Summer bei 150 Hz einschalten
        delay(500);
        tone(buzzerPin, 160);  // Summer bei 160 Hz einschalten
        delay(500);
        ...
    }

6. Du wirst feststellen, dass der Code über zweihundert Zeilen lang wäre, wenn du wirklich bis 1000 zählen wolltest. An diesem Punkt kannst du die ``for``-Schleife verwenden, die dazu dient, einen Block von Anweisungen, der in geschweifte Klammern eingeschlossen ist, zu wiederholen.

    * ``for``: Die ``for``-Schleife ist nützlich für jede wiederholte Operation und wird oft in Kombination mit Arrays verwendet, um auf Daten/Pins zuzugreifen. Ein Inkrementzähler wird dabei in der Regel verwendet, um die Schleife zu durchlaufen und zu beenden. 

    **Syntax**

    .. code-block::

        for (initialization; condition; increment) {
            // Anweisung(en);
        }

    **Parameter**

        * ``initialization``: wird zuerst und nur einmal ausgeführt.
        * ``condition``: wird bei jedem Durchlauf der Schleife getestet; wenn sie wahr ist, wird der Anweisungsblock ausgeführt, dann das Inkrement durchgeführt und die Bedingung erneut geprüft. Wenn die Bedingung falsch wird, endet die Schleife.
        * ``increment``: wird bei jedem Durchlauf der Schleife ausgeführt, solange die Bedingung wahr ist.

.. image:: img/for_loop.png
    :width: 400
    :align: center


7. Ändere nun die Funktion ``void loop()``, wie unten gezeigt, wobei ``freq`` bei 100 startet und sich in Schritten von 10 bis 1000 erhöht.

.. code-block:: Arduino
    :emphasize-lines: 3-6

    void loop() {
        // Steigere allmählich die Tonhöhe
        for (int freq = 100; freq <= 1000; freq += 10) {
            tone(buzzerPin, freq);  // Erzeuge einen Ton
            delay(20);              // Warte vor dem Frequenzwechsel
        }
    }

8. Lass als Nächstes ``freq`` bei 1000 starten und sich in Schritten von 10 bis 100 verringern, sodass du den Ton des Summers von tief nach hoch und dann von hoch nach tief hören kannst und somit einen Sirenenton simulierst.

.. code-block:: Arduino
    :emphasize-lines: 9-12

    void loop() {
        // Steigere allmählich die Tonhöhe
        for (int freq = 100; freq <= 1000; freq += 10) {
            tone(buzzerPin, freq);  // Erzeuge einen Ton
            delay(20);              // Warte vor dem Frequenzwechsel
        }

        // Verringere allmählich die Tonhöhe
        for (int freq = 1000; freq >= 100; freq -= 10) {
            tone(buzzerPin, freq);  // Erzeuge einen Ton
            delay(20);              // Warte vor dem Frequenzwechsel
        }
    }


9. Hier ist dein vollständiger Code. Du kannst jetzt auf „Upload“ klicken, um den Code auf das Arduino Uno R3 hochzuladen.

.. code-block:: Arduino

    const int buzzerPin = 9;  // Weist Pin 9 der Konstanten für den Summer zu

    void setup() {
        // Hier Setup-Code einfügen, um ihn einmal auszuführen:
    }

    void loop() {
        // Steigere allmählich die Tonhöhe
        for (int freq = 100; freq <= 1000; freq += 10) {
            tone(buzzerPin, freq);  // Erzeuge einen Ton
            delay(20);              // Warte vor dem Frequenzwechsel
        }

        // Verringere allmählich die Tonhöhe
        for (int freq = 1000; freq >= 100; freq -= 10) {
            tone(buzzerPin, freq);  // Erzeuge einen Ton
            delay(20);              // Warte vor dem Frequenzwechsel
        }
    }

10. Speichere schließlich deinen Code und räume deinen Arbeitsplatz auf.

**Zusammenfassung**

In dieser Lektion haben wir untersucht, wie man mit einem Arduino und einem passiven Summer einen Sirenenton simuliert. Durch die Besprechung der grundlegenden physikalischen Eigenschaften von Schall, wie Frequenz und Tonhöhe, haben wir gelernt, wie diese Elemente die Wahrnehmung und Wirkung von Klang beeinflussen. Durch praktische Übungen haben wir nicht nur den Aufbau von Schaltungen erlernt, sondern auch die Programmierung mit der ``tone()``-Funktion auf dem Arduino gemeistert, um die Frequenz und Dauer von Klängen zu steuern und so die Simulation eines Sirenentons zu erreichen, der in der Tonhöhe an- und absteigt.
