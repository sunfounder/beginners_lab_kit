.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Sneak Peeks.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!


7. Lass uns Ampeln bauen!
=============================

.. .. image:: img/5_traffic_light_pic.png
..     :width: 400
..     :align: center

Willkommen zu dieser Lektion! In dieser spannenden Lektion schlagen wir die Brücke zwischen theoretischen Konzepten und praktischer Anwendung in Elektronik und Programmierung. Wir tauchen in den Prozess ein, wie man Pseudo-Code—eine vereinfachte Form der Programmiersprache—in funktionale Arduino-Skizzen umwandelt. Diese Übung simuliert die Funktionsweise von Ampeln und bietet dir praktische Erfahrungen in der Programmierung und im Schaltungsdesign. Durch das Verstehen und Umsetzen von Pseudo-Code gewinnst du tiefere Einblicke in die Logik hinter der Steuerung elektronischer Geräte mit Code.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/7_traffic_light.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion lernst du:

* Pseudo-Code zu schreiben und zu interpretieren, um die Funktionalität elektronischer Schaltungen zu planen.
* Pseudo-Code in Arduino-Skizzen zu konvertieren, um Ampelsimulationen zu steuern.
* Ein Ampelsystem mit LEDs und einem Arduino-Board zu bauen und zu programmieren.

Mit diesen Fähigkeiten wirst du in der Lage sein, einfache elektronische Systeme zu entwerfen, zu programmieren und zu debuggen, was dir den Weg zu komplexeren Projekten ebnet.

Vorbereitung der Ampeln
------------------------------------
Bereit, deine eigene Ampel mit einem Arduino zu erstellen? Hier ist, was wir brauchen:

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * Gelbe LED
     - 1 * Grüne LED
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_yellow_led| 
     - |list_green_led| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - 3 * 220Ω Widerstand
     - Verbindungsdrähte
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_wire| 



**Schritt-für-Schritt-Aufbau**

Lass uns alles zusammenbauen, wie bei einem LEGO-Set!

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

1. Verbinde einen 220Ω Widerstand mit dem Steckbrett. Ein Ende sollte am Minuspol sein, das andere Ende in Loch 1B.

.. image:: img/7_traffic_light_resistor.png
    :width: 600
    :align: center

2. Füge eine grüne LED zum Steckbrett hinzu. Die Anode (das lange Bein) sollte in Loch 1F sein. Die Kathode (das kurze Bein) sollte in Loch 1E sein.

.. image:: img/7_traffic_light_green.png
    :width: 600
    :align: center

3. Verbinde die grüne LED mit Pin 3 des Arduino Uno R3. Setze ein Verbindungsdraht in Loch 1J und das andere Ende des Drahtes in Pin 3 des Arduino Uno R3.

.. image:: img/7_traffic_light_pin3.png
    :width: 600
    :align: center

4. Nimm einen weiteren 220Ω Widerstand und verbinde ein Ende mit dem Minuspol und das andere Ende mit Loch 6B.

.. image:: img/7_traffic_light_yellow_resistor.png
    :width: 600
    :align: center

5. Nimm eine gelbe LED. Die Anode der LED (das lange Bein) sollte in Loch 6F sein, die Kathode (das kurze Bein) in Loch 6E.

.. image:: img/7_traffic_light_yellow.png
    :width: 600
    :align: center

6. Verbinde die gelbe LED mit Pin 4 des Arduino Uno R3.

.. image:: img/7_traffic_light_pin4.png
    :width: 600
    :align: center

7. Verbinde die rote LED auf die gleiche Weise. Die rote LED wird mit Pin 5 des Arduino Uno R3 verbunden.

.. image:: img/7_traffic_light_red.png
    :width: 600
    :align: center

8. Ups! Wir haben fast vergessen, die Schaltung zu erden. Verbinde die negative Seite des Steckbretts mit einem GND-Pin des Arduino Uno R3 mithilfe eines schwarzen Drahtes. Jetzt ist alles bereit!

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

.. note::

    Es gibt drei GND-Pins am Arduino Uno R3. Du kannst jeden von ihnen verwenden; sie funktionieren alle gleich.

Und so hast du ein vollständiges Ampelsystem aufgebaut! Jede Farbe wird durch einen eigenen Schalter auf dem R3 gesteuert, der anzeigt, wann Autos anhalten, warten oder fahren dürfen. Ist es nicht großartig, etwas zu bauen, das wie echte Ampeln funktioniert? Super gemacht!

Schreiben von Pseudo-Code für eine Ampel
----------------------------------------------

Nun ist es an der Zeit, deinen LEDs eine Funktion zu geben. In dieser Aktivität wirst du sie so programmieren, dass sie wie eine Ampel funktionieren und den Verkehrsfluss an einer belebten Kreuzung steuern.

Ampeln erfordern eine präzise Steuerung, um die Farben in einer festen Reihenfolge zu wechseln, was es zu einem idealen Projekt für den Einstieg in die Arduino-Programmierung macht. Um unsere Ampel perfekt zu machen, müssen wir dem Arduino klar sagen, welche Aufgaben er ausführen soll.

Die Kommunikation zwischen Menschen erfolgt durch Zuhören, Sprechen, Lesen, Schreiben, Gesten oder Gesichtsausdrücke. Die Kommunikation mit Mikrocontrollern (wie dem auf deinem Arduino-Board) erfolgt durch das Schreiben von Code.

Wir können dem Arduino nicht einfach in natürlicher Sprache sagen: "Mach eine Ampel". Aber wir können natürliche Sprache verwenden, um einen "Pseudo-Code" zu schreiben, der uns bei der eigentlichen Code-Entwicklung unterstützt.

.. note::
    
    Beim Schreiben von Pseudo-Code gibt es kein richtig oder falsch. Je detaillierter dein Pseudo-Code, desto einfacher wird es, ihn in ein funktionierendes Programm zu übersetzen.

Denke darüber nach, was passieren muss, damit deine Schaltung wie eine Ampel funktioniert. Schreibe den Pseudo-Code auf, der beschreibt, wie deine Ampel funktionieren soll. Nutze einfaches Deutsch.

Hier sind einige Leitfragen für deinen Pseudo-Code:

* Sollten zwei oder mehr Lichter gleichzeitig an sein?
* In welcher Reihenfolge sollten die Lichter wechseln?
* Was passiert mit den anderen Lichtern, wenn eines leuchtet?
* Was passiert, nachdem das dritte Licht ausgeschaltet wurde?
* Wie lange sollte jedes Licht an bleiben?

Hier sind ein paar Beispiele für Pseudo-Code:

.. code-block::

    1) Set all LED pins to output.
    2) Start main loop.
    a) Turn off all lights.
    b) Turn on green light for 10 seconds.
    c) Turn off all lights.
    d) Turn on yellow light for 3 seconds.
    e) Turn off all lights.
    f) Turn on red light for 10 seconds.
    3) Return to the start of the loop.

.. code-block::

    Setup:
        Define all LED pins as output
    Main Loop:
        Turn on green light
        Turn off red and yellow lights
        Wait 10 seconds
        Turn on yellow light
        Turn off red and green lights
        Wait 3 seconds
        Turn on red light
        Turn off green and yellow lights
        Wait 10 seconds

Pseudo-Code hat kein festes Format, was dir hilft, deine Gedanken zu klären und sie logisch zu ordnen. Diese logische Reihenfolge nennt man einen Algorithmus.
Du benutzt täglich Algorithmen, vielleicht ohne es zu merken. Ein Algorithmus ist wie ein Rezept; in der Programmierung sind die Zutaten Schlüsselwörter und Befehle, und die Kochschritte sind der Algorithmus.
Ein Algorithmus ist eine Reihe von Schritten oder Anweisungen. Wenn ein Algorithmus aus Pseudo-Code in die Arduino-Programmiersprache übersetzt wird, weist er das Arduino-Board genau an, was zu tun ist und wann.

.. note::
    
    Es kann hilfreich sein, Klebezettel oder Indexkarten zu verwenden, wenn du Pseudo-Code schreibst. Schreibe jeden Schritt deines Algorithmus auf einen separaten Zettel. So kannst du Schritte leicht neu anordnen, einfügen oder entfernen.


Umwandeln von Pseudo-Code in eine Arduino-Skizze
-----------------------------------------------------

Nun ist es an der Zeit, den Code zu verfeinern und zusätzliche ``digitalWrite()``- und ``delay()``-Befehle nach Bedarf hinzuzufügen. Hier ist eine Anleitung zur Strukturierung deines Codes: Deine ``void loop()``-Funktion sollte separate Segmente für die grünen, gelben und roten LEDs enthalten, wobei jede von einer eigenen Verzögerungszeit gefolgt wird. Nicht alle Verzögerungen müssen gleich lang sein. Aktualisiere deine Code-Kommentare, um klarzustellen, was jede Zeile bewirkt.

1. Öffne die Skizze, die du zuvor gespeichert hast, ``Lesson6_Blink_LED``. Klicke auf „Speichern unter...“ im „Datei“-Menü und benenne sie in ``Lesson7_Traffic_Light`` um. Klicke auf "Speichern".

2. Gemäß unserem Pseudo-Code setze alle drei Pins in ``void setup()`` auf Ausgang. Kopiere den ``pinMode()``-Befehl zweimal, füge ihn darunter ein und passe die Pinnummern entsprechend an.

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void setup() {
            // Setup code here, to run once:
            pinMode(3, OUTPUT); // set pin 3 as output
            pinMode(4, OUTPUT); // set pin 4 as output
            pinMode(5, OUTPUT); // set pin 5 as output
        }

3. In ``void loop()``, schalte zuerst die grüne LED ein und die anderen beiden LEDs aus. Kopiere also die ``digitalWrite()``-Befehle zweimal und ändere die Pinnummern auf 4 und 5, wobei du ``HIGH`` in ``LOW`` für die LEDs änderst, die ausgeschaltet werden sollen, und aktualisiere die Kommentare, um das aktuelle Szenario widerzuspiegeln. Der modifizierte Code lautet wie folgt:

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void loop() {
            // put your main code here, to run repeatedly:
            digitalWrite(3, HIGH);  // Light up the LED on pin 3
            digitalWrite(4, LOW);   // Switch off the LED on pin 4
            digitalWrite(5, LOW);   // Switch off the LED on pin 5
            delay(3000);           // Wait for 3 seconds
        }

4. Du möchtest vielleicht, dass die grüne LED länger leuchtet. In unserem Verkehrssystem könnte dies etwa eine Minute sein, aber hier simulieren wir es mit 10 Sekunden.

    .. code-block:: Arduino
        :emphasize-lines: 6

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // LED an Pin 3 einschalten
            digitalWrite(4, LOW);   // LED an Pin 4 ausschalten
            digitalWrite(5, LOW);   // LED an Pin 5 ausschalten
            delay(10000);           // 10 Sekunden warten
        }

5. Nun lass die gelbe LED aufleuchten und die anderen beiden LEDs ausschalten. Kopiere und füge erneut die 4 Zeilen aus ``void loop()`` ein, setze Pin 4 auf HIGH und die anderen auf LOW. Ändere die Verzögerung für die gelbe LED auf 3 Sekunden.

    .. code-block:: Arduino
        :emphasize-lines: 7-10

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // LED an Pin 3 einschalten
            digitalWrite(4, LOW);   // LED an Pin 4 ausschalten
            digitalWrite(5, LOW);   // LED an Pin 5 ausschalten
            delay(10000);           // 10 Sekunden warten
            digitalWrite(3, LOW);   // LED an Pin 3 ausschalten
            digitalWrite(4, HIGH);  // LED an Pin 4 einschalten
            digitalWrite(5, LOW);   // LED an Pin 5 ausschalten
            delay(3000);            // 3 Sekunden warten
        }

6. Schließlich lass die rote LED für 10 Sekunden leuchten und schalte die anderen beiden LEDs aus. Dein vollständiger Code sieht wie folgt aus:

    .. code-block:: Arduino

        void setup() {
            // Setup code here, to run once:
            pinMode(3, OUTPUT); // set pin 3 as output
            pinMode(4, OUTPUT); // set pin 4 as output
            pinMode(5, OUTPUT); // set pin 5 as output
        }
        
        void loop() {
            // put your main code here, to run repeatedly:
            digitalWrite(3, HIGH);  // Light up the LED on pin 3
            digitalWrite(4, LOW);   // Switch off the LED on pin 4
            digitalWrite(5, LOW);   // Switch off the LED on pin 5
            delay(10000);           // Wait for 10 seconds
            digitalWrite(3, LOW);   // Switch off the LED on pin 3
            digitalWrite(4, HIGH);  // Light up the LED on pin 4
            digitalWrite(5, LOW);   // Switch off LED on pin 5
            delay(3000);            // Wait for 3 seconds
            digitalWrite(3, LOW);   // Switch off the LED on pin 3
            digitalWrite(4, LOW);   // Switch off the LED on pin 4
            digitalWrite(5, HIGH);  // Light up LED on pin 5
            delay(10000);           // Wait for 10 seconds
        }

**Frage**

Schau dir die Kreuzungen in deiner Umgebung an. Wie viele Ampeln gibt es normalerweise? Wie koordinieren sie sich gegenseitig?

**Zusammenfassung**

Herzlichen Glückwunsch zum Abschluss der Lektion 7! Du hast erfolgreich Pseudo-Code in ein voll funktionsfähiges, Arduino-gesteuertes Ampelsystem übersetzt. Hier eine kurze Zusammenfassung dessen, was du erreicht hast:

* Pseudo-Code Beherrschen: Du hast gelernt, wie man Pseudo-Code verwendet, um die Abläufe eines elektronischen Systems zu planen und deine logischen Denk- und Planungsfähigkeiten verbessert.
* Von Pseudo-Code zu echtem Code: Du hast erfahren, wie ein strukturierter Ansatz im Pseudo-Code zu einer effektiven und genauen Arduino-Programmierung führt.
* Praktische Anwendung: Durch den Aufbau und die Programmierung eines Ampelsystems hast du gezeigt, wie Software direkt Hardware steuern kann.

Diese Lektion hat sowohl deine technischen Fähigkeiten als auch dein analytisches Denken geschärft und dich auf komplexere Projekte in Elektronik und Programmierung vorbereitet. Nutze diese Fähigkeiten weiter, um noch mehr Möglichkeiten in der Technik zu erschließen!

