.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusive Einblicke.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Gewinnspielen und saisonalen Aktionen teil.

    👉 Bereit, mit uns zu entdecken und zu erschaffen? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

18. Licht-Alarm
========================

.. image:: img/18_light_alarm.png
    :width: 600
    :align: center

Stell dir eine Szene direkt aus einem Film vor:
In einem schwach beleuchteten Museum nähert sich ein geschickter Dieb lautlos einem unbezahlbaren Gemälde.
Er bewegt sich leise, um den Diebstahl in der Dunkelheit durchzuführen.
Doch in dem Moment, in dem er das Gemälde berührt, lösen eine Reihe von raffinierten Sensoren Alarm aus, die den gesamten Raum erhellen.
Der Dieb wird sofort von der Sicherheit vor Ort gefasst und der geplante Kunstraub wird verhindert.
Das ist kein Film, sondern ein reales Beispiel für Sensortechnologie in modernen Sicherheitssystemen.

Wie wird das erreicht? Es wird ein Fotowiderstand oder ein fortschrittlicherer Lichtsensor in der Nähe des Rahmens des Gemäldes angebracht. Jede Bewegung des Gemäldes oder das Blockieren des Lichts verändert die Lichtverhältnisse, was das Alarmsystem auslöst.

Lass uns nun ein simuliertes Lichtalarmsystem mit einem Fotowiderstand und einem Summer bauen, einverstanden?

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/18_light_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion wirst du lernen:

* Die Funktionsweise und Eigenschaften eines Fotowiderstands.
* Wie man ein einfaches Lichtalarmsystem baut.


Den Schaltkreis aufbauen
----------------------------

**Benötigte Bauteile**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Fotowiderstand
     - 1 * 10KΩ Widerstand
     - 1 * Aktiver Summer
   * - |list_uno_r3| 
     - |list_photoresistor| 
     - |list_10kohm| 
     - |list_active_buzzer| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Verbindungskabel
     - 1 * Multimeter
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_meter|



**Schritt-für-Schritt-Anleitung**

1. Beginne mit einem Fotowiderstand.

.. image:: img/17_photoresistor.png
    :width: 100
    :align: center

Ein Fotowiderstand oder auch Fotodiode ist ein lichtgesteuerter variabler Widerstand. Der Widerstand eines Fotowiderstands nimmt mit zunehmender Lichtintensität ab; anders ausgedrückt, er zeigt Fotoleitfähigkeit.

Fotowiderstände können als widerstandsbasierte Halbleiter in lichtempfindlichen Detektorschaltungen sowie in licht- und dunkelgesteuerten Schaltungen verwendet werden. Im Dunkeln kann der Widerstand eines Fotowiderstands mehrere Megaohm (MΩ) betragen, während er bei Licht auf einige Hundert Ohm sinken kann.

Das Kit enthält einen Widerstand mit einem Nennwert von 10K bei 25°C. Nun verwende ein Multimeter, um den Widerstand des Fotowiderstands unter normalen Lichtverhältnissen, bei Beleuchtung und in der Dunkelheit zu messen.

2. Da der Nennwiderstand des Fotowiderstands 10K beträgt, stelle das Multimeter auf den Messbereich von 20 Kiloohm (20K) ein.

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

3. Setze den Fotowiderstand in das Steckbrett an den Positionen 10E und 11E ein. Die Pins sind nicht richtungsgebunden und können beliebig eingefügt werden.

.. image:: img/17_light_alarm_photoresistor.png
    :width: 500
    :align: center

4. Berühre nun die beiden Pins des Fotowiderstands mit den roten und schwarzen Prüfspitzen des Multimeters.

.. image:: img/17_light_alarm_test.png
    :width: 500
    :align: center

5. Lies den Widerstandswert unter dem aktuellen Umgebungslicht ab und notiere ihn in der folgenden Tabelle.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kiloohm)
   * - Normales Licht
     - *5,48*
   * - Helles Licht
     -
   * - Dunkelheit
     -

6. Lass nun einen Freund helfen, indem er eine Taschenlampe oder eine andere Lichtquelle direkt auf den Fotowiderstand richtet. Notiere den Widerstandswert, der nur ein paar Hundert Ohm betragen könnte. Daher solltest du das Multimeter auf 2K oder sogar auf 200 Ohm einstellen, um eine genauere Messung zu erhalten.

.. note::

    Wir haben die Widerstandseinheit in der Tabelle auf Kiloohm gesetzt. 1 Kiloohm (kΩ) = 1000 Ohm.

    Wenn du den 200-Ohm-Bereich wählst und eine Messung von 164,5 Ohm erhältst, konvertiere den Wert in 0,16 Kiloohm (gerundet auf zwei Dezimalstellen) und trage den umgerechneten Wert in die Tabelle ein.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kiloohm)
   * - Normales Licht
     - *≈5.48*
   * - Helles Licht
     - *≈0.16*
   * - Dunkelheit
     - 

7. Unter dunklen Bedingungen kann der Widerstand des Fotowiderstands mehrere Megaohm erreichen, daher müssen wir das Multimeter auf den 2-Megaohm-Bereich einstellen.

.. image:: img/multimeter_2mΩ.png
    :width: 300
    :align: center

8. Bedecke den Fotowiderstand vollständig mit einem schwarzen Gegenstand und notiere den gemessenen Widerstand in der Tabelle.

.. note::
    Wir haben die Widerstandseinheit in der Tabelle auf Kiloohm gesetzt. 1 Megaohm (MΩ) = 1000 Kiloohm.

    Wenn du den 2-Megaohm-Bereich wählst und eine Messung von 1,954 Megaohm erhältst, konvertiere den Wert in 1954 Kiloohm, das ist der Wert, den du eintragen solltest.

    Wenn die Messung direkt höher als 2 MΩ ist, wird „1.“ angezeigt, und du kannst direkt 2 Megaohm eintragen oder ein präziseres Multimeter verwenden, um den genauen Wert zu messen.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kiloohm)
   * - Normales Licht
     - *≈5.48*
   * - Helles Licht
     - *≈0.16*
   * - Dunkelheit
     - *≈1954*

Anhand der Messungen haben wir die fotoleitenden Eigenschaften des Fotowiderstands bestätigt: Je stärker das Licht, desto geringer der Widerstand; je schwächer das Licht, desto höher der Widerstand, der bis zu mehreren Megaohm erreichen kann.

9. Setze den Schaltkreis weiter zusammen. Verbinde einen Pin des Fotowiderstands mit der negativen Klemme des Steckbretts und den anderen Pin mit dem A0-Pin des Arduino Uno R3.

.. image:: img/17_light_alarm_a0.png
    :width: 500
    :align: center

10. Setze einen 10K-Widerstand in dieselbe Reihe wie die Verbindung des Fotowiderstands zu A0.

.. image:: img/17_light_alarm_resistor.png
    :width: 500
    :align: center

In diesem Schaltkreis sind der 10K-Widerstand und der Fotowiderstand in Reihe geschaltet, der durch sie fließende Strom ist derselbe. Der 10K-Widerstand fungiert als Schutz, und der A0-Pin liest den Wert nach der Spannungsumwandlung des Fotowiderstands aus.

Wenn das Licht stärker wird, verringert sich der Widerstand des Fotowiderstands, und seine Spannung sinkt, sodass der Wert des A0-Pins abnimmt. Wenn das Licht stark genug ist, wird der Widerstand des Fotowiderstands nahe null sein, und der Wert des A0-Pins wird nahe null sein. Zu diesem Zeitpunkt spielt der 10K-Widerstand eine Schutzrolle, indem er verhindert, dass 5V und GND direkt miteinander verbunden werden.

Wenn du den Fotowiderstand in einer dunklen Umgebung platzierst, wird der Wert des A0-Pins ansteigen. In einer sehr dunklen Umgebung wird der Widerstand des Fotowiderstands unendlich groß, und seine Spannung wird nahe 5V liegen (der 10K-Widerstand wird vernachlässigbar), und der Wert des A0-Pins wird nahe 1023 sein.

11. Verbinde den anderen Pin des 10K-Widerstands mit dem 5V-Pin des Arduino Uno R3.

.. image:: img/17_light_alarm_5v.png
    :width: 500
    :align: center

12. Setze nun, wie in der vorherigen Lektion, den aktiven Summer in das Steckbrett ein, indem du seine Anode mit Pin 9 des R3 und seine Kathode mit der negativen Klemme des Steckbretts verbindest.

.. image:: img/17_light_alarm_buzzer.png
    :width: 500
    :align: center

13. Verbinde schließlich die negative Klemme des Steckbretts mit dem GND-Pin des Arduino Uno R3 mit einem Verbindungskabel.

.. image:: img/17_light_alarm.png
    :width: 500
    :align: center

Code-Erstellung
----------------------
1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „Datei“ die Option „Neue Skizze“ auswählst.
2. Speichere deine Skizze als ``Lesson18_Light_Alarm`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Erstelle vor der Funktion ``void setup()`` Konstanten für den Fotowiderstand und den Summer sowie einen konstanten Schwellenwert, der den Alarm auslöst, wenn der Messwert des Fotowiderstands darunter liegt.

.. code-block:: Arduino
    :emphasize-lines: 1,2,3

    const int sensorPin = A0;   // Weist Pin A0 der Konstanten für den Fotowiderstand zu
    const int buzzerPin = 9;    // Weist Pin 9 der Konstanten für den Summer zu
    const int threshold = 300;  // Setzt den Schwellenwert

    void setup() {
        // Hier kommt der Setup-Code, der einmal ausgeführt wird:
    }

4. Erstellen Sie außerdem eine Variable, um den vom Fotowiderstand gelesenen Wert zu speichern.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int sensorPin = A0;   // Weist den Pin A0 dem Fotowiderstand zu
    const int buzzerPin = 9;    // Weist den Pin 9 dem Buzzer zu
    const int threshold = 300;  // Setzt den Schwellenwert fest

    int sensorValue = 0;  // Um den Wert des Fotowiderstands zu speichern

    void setup() {
        // Hier kommt der Code, der einmalig ausgeführt wird:
    }

5. Setzen Sie im ``void setup()`` den Buzzer als Ausgang und starten Sie die serielle Kommunikation, um die Werte des Fotowiderstands zu überwachen.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void setup() {
        // Hier kommt der Code, der einmalig ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt den Buzzer-Pin als Ausgang
        Serial.begin(9600);          // Initialisiert die serielle Kommunikation mit 9600 Baud
    }

6. Verwenden Sie in der ``void loop()`` die Funktion ``analogRead()``, um den Wert des Fotowiderstands zu lesen und diesen in der Variablen ``sensorValue`` zu speichern. Geben Sie diesen Wert anschließend im seriellen Monitor aus. Denken Sie daran, ein Zeitintervall für jede Messung festzulegen.

.. code-block:: Arduino
    :emphasize-lines: 3,4,5

    void loop() {
        // Hier kommt der Hauptcode, der wiederholt ausgeführt wird:
        sensorValue = analogRead(sensorPin);  // Liest den analogen Wert des Fotowiderstands
        Serial.println(sensorValue);          // Gibt den Wert des Fotowiderstands im seriellen Monitor aus
        delay(100);                           // Wartet 0,1 Sekunden
    }

7. Wenn die Umgebung von dunkel zu hell wechselt, sinkt der Widerstand des Fotowiderstands und damit der Wert am Pin A0. Verwenden Sie nun eine ``if``-Anweisung, um zu prüfen, ob der Wert des Fotowiderstands unter dem ``threshold`` liegt. Wenn dies der Fall ist, wird der Buzzer eingeschaltet, andernfalls ausgeschaltet.

.. code-block:: Arduino
    :emphasize-lines: 7-12

    void loop() {
        // Hier kommt der Hauptcode, der wiederholt ausgeführt wird:
        sensorValue = analogRead(sensorPin);  // Liest den analogen Wert des Fotowiderstands
        Serial.println(sensorValue);          // Gibt den Wert des Fotowiderstands im seriellen Monitor aus
        delay(100);                           // Wartet 0,1 Sekunden

        // Überprüft, ob der Wert unter dem Schwellenwert liegt
        if (sensorValue < threshold) {
            digitalWrite(buzzerPin, HIGH);  // Wenn der Wert unter dem Schwellenwert liegt, Buzzer einschalten
        } else {
            digitalWrite(buzzerPin, LOW);   // Wenn nicht, Buzzer ausschalten
        }
    }

8. Hier ist Ihr vollständiger Code. Sie können jetzt auf „Upload“ klicken, um den Code auf das Arduino Uno R3 hochzuladen.

.. code-block:: Arduino

    const int sensorPin = A0;   // Weist den Pin A0 dem Fotowiderstand zu
    const int buzzerPin = 9;    // Weist den Pin 9 dem Buzzer zu
    const int threshold = 300;  // Setzt den Schwellenwert fest

    int sensorValue = 0;  // Um den Wert des Fotowiderstands zu speichern

    void setup() {
        // Hier kommt der Code, der einmalig ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt den Buzzer-Pin als Ausgang
        Serial.begin(9600);          // Initialisiert die serielle Kommunikation mit 9600 Baud
    }

    void loop() {
        // Hier kommt der Hauptcode, der wiederholt ausgeführt wird:
        sensorValue = analogRead(sensorPin);  // Liest den analogen Wert des Fotowiderstands
        Serial.println(sensorValue);          // Gibt den Wert des Fotowiderstands im seriellen Monitor aus
        delay(100);                           // Wartet 0,1 Sekunden

        // Überprüft, ob der Wert unter dem Schwellenwert liegt
        if (sensorValue < threshold) {
            digitalWrite(buzzerPin, HIGH);  // Wenn der Wert unter dem Schwellenwert liegt, Buzzer einschalten
        } else {
            digitalWrite(buzzerPin, LOW);   // Wenn nicht, Buzzer ausschalten
        }
    }

9. Speichern Sie abschließend Ihren Code und räumen Sie Ihren Arbeitsplatz auf.



**Frage**

Gerissene Diebe könnten in der Nacht zuschlagen, und wenn ein Gemälde verschwindet, kann es sein, dass der Fotowiderstand keine Änderung des Lichts erkennt und somit keinen Alarm auslöst. Was kann getan werden, um diesen Mangel zu beheben?
