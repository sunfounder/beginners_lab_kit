.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein, gemeinsam mit anderen Technikbegeisterten.

    **Warum solltest du beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Vorschauen.
    - **Exklusive Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu gestalten? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

6. LED Blinken
======================
Willkommen zu dieser Lektion, in der du lernst, die digitalen Pins des Arduino Uno R3 zu steuern, um eine LED programmatisch ein- und auszuschalten – eine Fähigkeit, die sowohl in der Heim- als auch in der Industrieelektronik von grundlegender Bedeutung ist.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/6_blink_led.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion lernst du:

* Skizzen mit der Arduino IDE zu erstellen und zu speichern.
* Die Funktionen ``pinMode()`` und ``digitalWrite()`` zu nutzen, um Schaltungselemente zu steuern.
* Skizzen auf den Arduino Uno R3 hochzuladen und ihre Echtzeiteffekte zu verstehen.
* Die Funktion ``delay()`` in Skizzen zu implementieren, um das Verhalten von Schaltungen zu steuern.

Am Ende dieser Lektion wirst du in der Lage sein, eine Schaltung zu bauen, die nicht nur eine LED zum Leuchten bringt, sondern sie auch in von dir festgelegten Intervallen blinken lässt. Dies vermittelt dir ein grundlegendes Verständnis darüber, wie Software mit Hardware interagiert.

Schaltung aufbauen
--------------------------------

**Benötigte Komponenten**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * 220Ω Widerstand
     - Verbindungskabel
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - 1 * Multimeter
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     - 

**Schritt-für-Schritt Aufbau**

Nimm die Schaltung, die in :ref:`2_first_circuit` aufgebaut wurde, und wechsle das Kabel vom 5V-Pin zu Pin 3, wie im Bild unten gezeigt.

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center

Falls du die vorherige Schaltung abgebaut hast, kannst du sie nach diesen Schritten wieder aufbauen:

1. Schließe den 220-Ohm-Widerstand an das Steckbrett an. Ein Draht sollte im negativen Anschluss, der andere Draht in Loch 1B stecken.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Füge eine rote LED auf dem Steckbrett hinzu. Die Anode der LED (das lange Bein) sollte in Loch 1F stecken, die Kathode (das kurze Bein) in Loch 1E. Manchmal ist es schwer, Anode und Kathode anhand der Beinlänge zu unterscheiden. Denke daran, dass die Kathodenseite der LED eine flache Kante an der farbigen Linse hat, während die Anode eine runde Kante hat.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Verwende ein kurzes Verbindungskabel, um die LED mit der Stromquelle zu verbinden. Ein Ende des Kabels sollte in Loch 1J stecken, das andere im positiven Anschluss.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Verbinde den positiven Anschluss des Steckbretts mit Pin 3 des Arduino Uno R3.

.. image:: img/6_led_circuit_3.png
    :width: 600
    :align: center

5. Verbinde den negativen Anschluss des Steckbretts mit einem der GND-Pins auf dem Arduino Uno R3. Die Masse-Pins sind mit "GND" gekennzeichnet.

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center


LED zum Leben erwecken
-----------------------------

Nun ist es an der Zeit, die LED in Betrieb zu nehmen! Anstatt direkt in das Blink-Beispiel des Arduino einzutauchen, erstellen wir von Grund auf eine neue Skizze. Los geht's!

**1. Eine Skizze erstellen und speichern**

1. Starte die Arduino IDE. Gehe zum Menü „Datei“ und wähle „Neue Skizze“, um frisch anzufangen. Du kannst alle anderen geöffneten Skizzenfenster schließen.

    .. image:: img/6_blink_ide_new.png
        :align: center

2. Ordne das Fenster der Arduino IDE nebeneinander mit diesem Online-Tutorial an, sodass du beide gleichzeitig sehen kannst. Es könnte ein wenig klein aussehen, aber es erspart dir das ständige Wechseln zwischen den Fenstern.

    .. image:: img/6_blink_ide_tutorials.png

3. Speichere deine Skizze. Klicke im Menü „Datei“ auf „Speichern“ oder drücke ``Strg + S``.

    .. image:: img/6_blink_ide_save.png

4. Du kannst deine Skizze im Standardverzeichnis oder an einem anderen Ort speichern. Nenne deine Skizze sinnvoll, z. B. ``Lesson6_Light_up_LED``, und klicke auf „Speichern“.

    * Benenne deine Skizze nach ihrer Funktion, um sie später leicht wiederzufinden.
    * Arduino-Skizzen-Dateinamen dürfen keine Leerzeichen enthalten.
    * Wenn du wesentliche Änderungen vornimmst, speichere sie am besten als neue Version (z.B. V1), um ein Backup zu haben.
    
    .. image:: img/6_blink_ide_name.png

5. Deine neue Skizze besteht aus zwei Hauptteilen: ``void setup()`` und ``void loop()``, Funktionen, die in allen Arduino-Skizzen verwendet werden.

    * ``void setup()`` läuft einmal, wenn das Programm startet, und legt die Anfangsbedingungen fest.
    * ``void loop()`` läuft wiederholt und führt kontinuierlich Aktionen aus.
    * Befehle für jede Funktion werden innerhalb ihrer geschweiften Klammern ``{}`` platziert.
    * Jede Zeile, die mit ``//`` beginnt, ist ein Kommentar. Diese dienen deinen Notizen und beeinflussen die Programmausführung nicht.

    .. code-block:: Arduino

        void setup() {
        // Setup code here, to run once:

        }

        void loop() {
        // put your main code here, to run repeatedly:

        }

**2. Auswahl des Boards und des Ports**

1. Verbinde dein Arduino Uno R3 mit dem Computer über ein USB-Kabel. Du wirst sehen, dass die Stromanzeige am Arduino aufleuchtet.

    .. image:: img/1_connect_uno_pc.jpg
        :width: 600
        :align: center


2. Lass die IDE wissen, dass wir ein **Arduino Uno** verwenden. Gehe zu **Werkzeuge** -> **Board** -> **Arduino AVR Boards** -> **Arduino Uno**.

    .. image:: img/6_blink_ide_board.png
        :width: 600
        :align: center


3. Wähle in der Arduino IDE den Port aus, an den dein Arduino angeschlossen ist.

    .. note::

        * Sobald ein Port ausgewählt ist, merkt sich die Arduino IDE diesen Standard, sobald das Arduino über USB angeschlossen wird.
        * Falls ein anderes Arduino-Board angeschlossen ist, musst du möglicherweise einen neuen Port auswählen.
        * Prüfe immer den Port zuerst, wenn es Verbindungsprobleme gibt.

    .. image:: img/6_blink_ide_port.png
        :width: 600
        :align: center

**3. Den Code schreiben**

1. In unserem Projekt nutzen wir den digitalen Pin 3 auf dem Board, um eine LED zu steuern. Jeder Pin kann entweder als Ausgang arbeiten, der 5 Volt ausgibt, oder als Eingang, der die eingehende Spannung liest. Um die LED zu konfigurieren, setzen wir den Pin mit der Funktion ``pinMode(pin, mode)`` als Ausgang.

Schauen wir uns die Syntax von ``pinMode()`` genauer an:

    * ``pinMode(pin, mode)``: Legt fest, ob ein bestimmter Pin als ``INPUT`` oder ``OUTPUT`` arbeiten soll.

    **Parameter**
        - ``pin``: Die Nummer des Pins, den du konfigurieren möchtest.
        - ``mode``: ``INPUT``, ``OUTPUT`` oder ``INPUT_PULLUP``.

    **Rückgabewert**
        Keiner
    
2. Jetzt ist es Zeit, unsere erste Codezeile in der Funktion ``void setup()`` hinzuzufügen.

    .. note::

        - Arduino-Code ist case-sensitiv. Stelle sicher, dass du die Funktionen genau so schreibst, wie sie sein sollen.
        - Beachte, dass der Befehl mit einem Semikolon endet. In der Arduino IDE muss jede Anweisung mit einem Semikolon abgeschlossen werden.
        - Kommentare im Code sind nützlich, um sich daran zu erinnern, was eine bestimmte Zeile oder ein Abschnitt macht.

    .. code-block:: Arduino
        :emphasize-lines: 3

        void setup() {
            // Setup-Code, der einmal ausgeführt wird:
            pinMode(3, OUTPUT); // Pin 3 als Ausgang setzen
        }
    
        void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:

        }

**4. Den Code verifizieren**

Bevor wir unsere Schaltung aktivieren, sollten wir den Code verifizieren. Dies überprüft, ob die Arduino IDE deine Befehle in Maschinensprache übersetzen kann.

1. Um deinen Code zu verifizieren, klicke auf das **Häkchen-Symbol** oben links im Fenster.

    .. image:: img/6_blink_ide_verify.png
        :width: 600
        :align: center

2. Wenn dein Code maschinenlesbar ist, erscheint unten eine Nachricht, die angibt, dass der Code erfolgreich kompiliert wurde. Dieser Bereich zeigt auch, wie viel Speicherplatz dein Programm verwendet.

    .. image:: img/6_blink_ide_verify_done.png
        :width: 600
        :align: center

3. Wenn es einen Fehler in deinem Code gibt, siehst du eine orangefarbene Fehlermeldung. Die IDE hebt oft die Stelle hervor, an der das Problem auftreten könnte, typischerweise in der Nähe der markierten Zeile. Beispielsweise wird bei einem fehlenden Semikolon der Fehler nach der betroffenen Zeile hervorgehoben.

    .. image:: img/6_blink_ide_verify_error.png
        :width: 600
        :align: center

4. Wenn du auf Fehler stößt, ist es Zeit für das Debugging – das Finden und Beheben von Fehlern im Code. Überprüfe häufige Probleme wie:

    - Ist das ``M`` in ``pinMode`` groß geschrieben?
    - Hast du ``OUTPUT`` komplett in Großbuchstaben geschrieben?
    - Hast du die Klammern in der Funktion ``pinMode`` korrekt gesetzt?
    - Hast du die Funktion ``pinMode`` mit einem Semikolon beendet?
    - Ist die Rechtschreibung korrekt? Wenn du Fehler findest, korrigiere sie und verifiziere den Code erneut. Debugge weiter, bis deine Skizze fehlerfrei ist.

Die Arduino IDE hört beim ersten Fehler auf zu kompilieren, sodass du möglicherweise mehrmals verifizieren musst, um alle Fehler zu finden. Es ist eine gute Angewohnheit, deinen Code regelmäßig zu verifizieren.

Debugging ist ein großer Teil des Programmierens. Professionelle Programmierer verbringen oft mehr Zeit mit Debugging als mit dem Schreiben von neuem Code. Fehler sind normal, also lass dich nicht entmutigen. Ein guter Problemlöser zu werden, ist der Schlüssel, um ein großartiger Programmierer zu sein.

**5. Den Sketch fortsetzen**

1. Nun bist du bereit, die Funktion ``void loop()`` zu schreiben. Hier passiert die Hauptaktion deines Sketches oder Programms. Um die LED, die mit dem Arduino Uno R3 verbunden ist, einzuschalten, müssen wir der Schaltung Spannung zuführen, indem wir die Funktion ``digitalWrite()`` verwenden.

    * ``digitalWrite(pin, value)``: Sendet ein ``HIGH`` (5V) oder ``LOW`` (0V) Signal an einen digitalen Pin und ändert den Betriebszustand der Komponente.

    **Parameter**
        - ``pin``: Die Nummer des Arduino-Pins.
        - ``value``: ``HIGH`` oder ``LOW``.
    
    **Rückgabewert**
        Keiner

5. Unter dem Kommentar in der Funktion ``void loop()``, schreibe einen Befehl, um die LED an Pin 3 einzuschalten. Vergiss nicht, den Befehl mit einem Semikolon zu beenden. Verifiziere und debugge deinen Code bei Bedarf.

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Setup-Code, der einmal ausgeführt wird:
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
        }

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);
        }

6. Nach dem ``digitalWrite()``-Befehl, füge einen Kommentar hinzu, der erklärt, was diese Zeile macht. Zum Beispiel:

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Setup-Code, der einmal ausgeführt wird:
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
        }

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // LED an Pin 3 einschalten
        }


**6. Hochladen des Codes**

Nachdem dein Code fehlerfrei und überprüft wurde, ist es Zeit, ihn auf das Arduino Uno R3 hochzuladen und dein Projekt zum Leben zu erwecken.

1. Klicke in der IDE auf die Schaltfläche „Hochladen“. Der Computer kompiliert den Code und überträgt ihn dann auf das Arduino Uno R3. Während der Übertragung sollten einige LEDs auf der Platine blinken, was auf die Kommunikation mit dem Computer hinweist.

.. image:: img/6_blink_ide_upload.png
    :width: 600
    :align: center

2. Eine Nachricht mit „Hochladen abgeschlossen“ bedeutet, dass dein Code keine Probleme aufweist und du das richtige Board und den richtigen Port ausgewählt hast.

.. image:: img/6_blink_ide_upload_done.png
    :width: 600
    :align: center

3. Sobald die Übertragung abgeschlossen ist, läuft der Code, und du solltest sehen, dass die LED auf dem Breadboard aufleuchtet.

**7. Spannung an der LED messen**

Lass uns ein Multimeter verwenden, um die Spannung an Pin 3 zu messen und zu verstehen, was der ``HIGH``-Zustand im Code tatsächlich bedeutet.

1. Stelle das Multimeter auf die 20-Volt-DC-Einstellung ein.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Beginne damit, die Spannung an Pin 3 zu messen. Berühre die rote Prüfspitze des Multimeters an Pin 3 und die schwarze Prüfspitze an GND.

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

3. Trage die gemessene Spannung in der Tabelle für Pin 3 in der Zeile „HIGH“ ein.

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - Zustand
     - Spannung an Pin 3
   * - HIGH
     - *≈4,95 Volt*
   * - LOW
     - 

4. Denke daran, das Multimeter nach der Messung auszuschalten, indem du es auf die "OFF"-Position stellst.

Unsere Messungen zeigen, dass die Spannung an allen drei Pins nahe bei 5V liegt. Dies deutet darauf hin, dass das Setzen eines Pins auf ``HIGH`` im Code bedeutet, dass die Ausgangsspannung an diesem Pin nahe 5V liegt.

Die Pin-Spannung des R3 beträgt 5V. Wenn sie auf ``HIGH`` gesetzt wird, erreicht sie nahezu 5V. Einige Boards arbeiten jedoch mit 3,3V, was bedeutet, dass ihr ``HIGH``-Zustand nahe bei 3,3V liegen würde.

LED blinken lassen
------------------------------
Jetzt, da deine LED leuchtet, ist es Zeit, sie zum Blinken zu bringen.

1. Öffne den Sketch, den du zuvor gespeichert hast, ``Lesson6_Light_up_LED``. Klicke auf „Speichern unter...“ im „Datei“-Menü und benenne ihn in ``Lesson6_Blink_LED`` um. Klicke auf "Speichern".

2. Kopiere in der Funktion ``void loop()`` die ``digitalWrite()``-Befehle und füge sie nach den Originalen ein. Um die LED zum Blinken zu bringen, hast du sie zuvor eingeschaltet; jetzt setze ihren Zustand auf ``LOW``, um sie auszuschalten.

    .. note::
       * Kopieren und Einfügen kann der beste Freund eines Programmierers sein. Repliziere einen fehlerfreien Abschnitt Code an eine neue Stelle und passe die Parameter schnell und effizient an.
       * Denke daran, die Kommentare zu aktualisieren, um besser zur ausgeführten Aktion zu passen.
       * Verwende ``Ctrl+T``, um deinen Code auf einen Klick ordentlich zu formatieren und ihn lesbarer zu machen.

    .. code-block:: Arduino
       :emphasize-lines: 8,9

       void setup() {
            // Setup-Code, der einmal ausgeführt wird:
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
       }

       void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // LED an Pin 3 einschalten
            digitalWrite(3, LOW);   // LED an Pin 3 ausschalten
       }

3. Drücke die Schaltfläche „Hochladen“, um den Sketch auf das Arduino Uno R3 zu übertragen. Nach der Übertragung stellst du möglicherweise fest, dass die LED entweder gar nicht blinkt oder so schnell blinkt, dass es nicht wahrnehmbar ist.

4. Um das Blinken visuell wahrnehmbar zu machen, kannst du den Befehl ``delay()`` verwenden, um das Arduino Uno R3 eine von dir festgelegte Zeitspanne in Millisekunden warten zu lassen.

    * ``delay(ms)``: Pausiert das Programm für die angegebene Zeit in Millisekunden. (Es gibt 1000 Millisekunden in einer Sekunde.)

    **Parameter**
        - ``ms``: Die Anzahl der Millisekunden, die das Programm pausiert. Zulässige Datentypen: unsigned long.

    **Rückgabewert**
        Keiner

5. Füge nun den Befehl ``delay(time)`` nach jedem Set von Ein- und Ausschaltbefehlen ein und stelle die Verzögerungszeit auf 3000 Millisekunden (3 Sekunden) ein. Du kannst diese Dauer anpassen, um die LED schneller oder langsamer blinken zu lassen.

    .. note::

        Während dieser Verzögerung kann das Arduino Uno R3 keine weiteren Aufgaben ausführen oder andere Befehle ausführen, bis die Verzögerung endet.
        
    .. code-block:: Arduino
       :emphasize-lines: 10,11

       void setup() {
            // Setup-Code, der einmal ausgeführt wird:
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
       }

       void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // LED an Pin 3 einschalten
            delay(3000);  // 3 Sekunden warten
            digitalWrite(3, LOW);   // LED an Pin 3 ausschalten
            delay(3000);  // 3 Sekunden warten
       }

6. Lade deinen Sketch auf das Arduino Uno R3 hoch. Nach Abschluss sollte deine LED im 3-Sekunden-Takt blinken.

7. Überprüfe, ob alles wie erwartet funktioniert, und speichere dann deinen Sketch.

8. Lass uns das Multimeter verwenden, um die Spannung an den Pins zu messen und zu verstehen, was der ``LOW``-Zustand im Code bedeutet. Stelle das Multimeter auf die 20-Volt-DC-Einstellung ein.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

9. Beginne damit, die Spannung an Pin 3 zu messen. Berühre die rote Prüfspitze des Multimeters an Pin 3 und die schwarze Prüfspitze an GND.

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

10. Wenn alle drei LEDs ausgeschaltet sind, trage die gemessene Spannung für Pin 3 in der Zeile „LOW“ in deine Tabelle ein.

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - Zustand
     - Spannung an Pin 3
   * - HIGH
     - *≈4,95 Volt*
   * - LOW
     - *0,00 Volt*

Unsere Messungen zeigen, dass die Spannung an Pin 3 auf 0V abfällt, wenn die LED ausgeschaltet ist. Dies zeigt, dass das Setzen eines Pins auf „LOW“ im Code die Ausgangsspannung an diesem Pin effektiv auf 0V reduziert und die angeschlossene LED ausschaltet. Dieses Prinzip ermöglicht es uns, den Ein- und Ausschaltzustand der LED mit präzisem Timing zu steuern und so das Verhalten einer Ampel nachzubilden.

**Frage**

Lade den obigen Code hoch, und du wirst sehen, dass die LED in einem 3-Sekunden-Intervall blinkt. Was müsstest du tun, wenn sie nur einmal ein- und ausgeschaltet werden soll?

**Zusammenfassung**

Herzlichen Glückwunsch zum Abschluss dieser Lektion, in der du erfolgreich eine LED zum Blinken gebracht hast, indem du das Arduino Uno R3 programmiert hast. Diese Lektion diente als Einführung in das Schreiben und Hochladen von Arduino-Skizzen, das Setzen von Pin-Modi und das Manipulieren von Ausgängen, um die gewünschten elektrischen Reaktionen zu erzielen. Durch den Aufbau der Schaltung und das Programmieren des Arduino Uno R3 hast du wertvolle Einblicke in die Interaktion zwischen Softwarebefehlen und physikalischem Hardwareverhalten gewonnen.

Deine Fähigkeit, eine LED zu steuern, ist nur der Anfang – stelle dir vor, was du erreichen kannst, wenn du auf diesen Grundlagen aufbaust!
