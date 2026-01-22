.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein und vernetze dich mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Sneak Peeks.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!


8. Ampel mit Fußgänger-Taste
===============================================

Willkommen zur nächsten Phase unserer Arduino-Reise. In der vorherigen Lektion haben wir ein grundlegendes Ampelsystem aufgebaut, das den Verkehr mit roten, gelben und grünen Lichtern steuert. Jetzt fügen wir eine interaktive Komponente hinzu, die die Komplexität der realen Welt widerspiegelt: einen Fußgängerschalter. Diese Funktion fügt eine menschliche Interaktion in unser elektronisches Kreuzungssystem ein und ermöglicht ein dynamisches Zusammenspiel zwischen Gehwegen und Fahrbahnen an belebten Kreuzungen.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/8_traffic_light_button.mp4" type="video/mp4">
        Dein Browser unterstützt den Video-Tag nicht.
    </video>

In dieser Lektion lernst du:

* Verstehen, wie Tasten funktionieren und welche Rolle sie in Schaltungen spielen.
* Erlernen der Verwendung von ``digitalRead()``, um den Zustand von Eingabepins zu erkennen.
* Implementieren von ``if``-Anweisungen, um bedingte Verhaltensweisen in Ampelsystemen zu schaffen.

Während wir dieses Projekt vertiefen, werden wir nicht nur den technischen Aufbau erkunden, sondern auch die Logik und Programmierung, die solche Systeme effizient in der Steuerung von Fußgänger- und Fahrzeugverkehr ermöglichen.

Den Schaltkreis aufbauen
-----------------------------

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
   * - 1 * Taster
     - 1 * Steckbrett
     - 3 * 220Ω Widerstand
     - 1 * 10K Ohm Widerstand
   * - |list_button| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * USB-Kabel
     - Verbindungsdrähte
     - 1 * Multimeter
     - 
   * - |list_usb_cable| 
     - |list_wire| 
     - |list_meter|
     - 


**Schritt-für-Schritt-Aufbau**

Folge dem Schaltplan oder den unten stehenden Schritten, um deinen Schaltkreis zu bauen.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center  

1. Starte mit der Ampelschaltung aus der vorherigen Lektion.

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

2. Finde einen Taster.

.. image:: img/8_traffic_button.png
    :width: 500
    :align: center

Taster sind allgegenwärtige Komponenten in der Elektronik, die als Schalter zum Schließen oder Öffnen von Schaltkreisen fungieren. Unten siehst du den inneren Aufbau eines Tasters sowie das in Schaltplänen übliche Symbol.

.. image:: img/8_traffic_button_symbol.png
    :width: 500
    :align: center

Obwohl Taster vier Pins haben, sind die Pins 1 und 2 sowie 3 und 4 jeweils miteinander verbunden. Wenn der Taster gedrückt wird, werden alle vier Pins miteinander verbunden und der Stromkreis geschlossen.

3. Stecke den Taster in das Steckbrett, quer über die mittlere Lücke, sodass die Pins in den Löchern 18e, 18f, 20e und 20f sitzen.

.. note::

    Wenn du dir nicht sicher bist, wie du den Taster einstecken sollst, versuche beide Ausrichtungen. In einer Richtung wird der Abstand der Pins etwas zu schmal sein.

.. image:: img/8_traffic_light_button_button.png
    :width: 600
    :align: center

4. Verbinde den oberen rechten Pin des Tasters mit Pin 8 des Arduino Uno R3 mithilfe eines langen Verbindungsdrahts. Stecke ein Ende in Loch 18j und das andere Ende in Pin 8.

.. image:: img/8_traffic_light_button_pin8.png
    :width: 600
    :align: center

5. Platziere einen 10K Ohm Widerstand zwischen den oberen linken Pin des Tasters und der Masse. Verbinde ein Ende mit Loch 18a und das andere mit der negativen Schiene des Steckbretts. Dieser Widerstand zieht Pin 8 auf Masse, wodurch er im ungedrückten Zustand auf LOW stabilisiert wird.

    .. image:: img/8_traffic_light_button_10k.png
        :width: 600
        :align: center

Pin 8 dient als Eingabe, um den Zustand des Tasters zu lesen. Arduino-Boards lesen Spannungen zwischen 0 und ungefähr 5 Volt an den Eingabepins und interpretieren diese als entweder LOW oder HIGH, basierend auf einer Schwellenwertspannung. Um als HIGH gelesen zu werden, muss ein Pin über 3 Volt haben. Für LOW muss er weniger als 1,5 Volt haben.

Ohne den 10K-Widerstand würde Pin 8 nur mit dem Taster verbunden sein und zwischen 0 und 5V schweben, was dazu führen würde, dass sein Zustand zufällig zwischen HIGH und LOW schwankt.

Der 10K-Widerstand, der Pin 8 mit Masse verbindet, zieht die Spannung des Pins auf Masse und stellt sicher, dass er als LOW gelesen wird, wenn der Taster nicht gedrückt ist.

6. Zuletzt versorge den Taster mit Strom, indem du die positive Schiene des Steckbretts mit dem 5V-Pin des Arduino Uno R3 mithilfe eines roten Stromkabels verbindest.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center

**Frage:**

Deine Ampel ist eine Mischung aus Reihen- und Parallelschaltungen. Erkläre, welche Teile deines Schaltkreises in Reihe geschaltet sind und warum. Erkläre dann, welche Teile parallel geschaltet sind und warum.


Code-Erstellung
----------------

**Pins initialisieren**

Bisher hast du die Ampel programmiert, um die grünen, gelben und roten LEDs nacheinander aufleuchten zu lassen. In dieser Lektion wirst du den Fußgängertaster so programmieren, dass beim Drücken die roten und gelben LEDs ausgehen, während die grüne LED blinkt und anzeigt, dass es sicher ist, die Straße zu überqueren.

1. Öffne das zuvor gespeicherte Sketch, ``Lesson7_Traffic_Light``. Klicke im Menü "Datei" auf "Speichern unter..." und benenne es um in ``Lesson8_Traffic_Light_Button``. Klicke auf "Speichern".

2. Füge in der ``void setup()``-Funktion einen weiteren ``pinMode()``-Befehl hinzu, um Pin 8 als Eingang (``INPUT``) zu deklarieren. Füge dann einen Code-Kommentar hinzu, um diesen neuen Befehl zu erklären.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(3, OUTPUT); // Setze Pin 3 als Ausgang
        pinMode(4, OUTPUT); // Setze Pin 4 als Ausgang
        pinMode(5, OUTPUT); // Setze Pin 5 als Ausgang
        pinMode(8, INPUT);  // Deklariere Pin 8 (Taste) als Eingang
    }
    
    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
        digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
        digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
        delay(10000);           // Warte 10 Sekunden
        digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
        digitalWrite(4, HIGH);  // Schalte die LED an Pin 4 ein
        digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
        delay(3000);            // Warte 3 Sekunden
        digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
        digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
        digitalWrite(5, HIGH);  // Schalte die LED an Pin 5 ein
        delay(10000);           // Warte 10 Sekunden
    }

3. Nach dem Codieren überprüfe dein Sketch und lade den Code auf das Arduino Uno R3 hoch.

**Spannung an Pin 8 messen**

Wir wissen bereits, wie der LED-Teil unseres Schaltkreises aus der vorherigen Lektion funktioniert. Jede LED fungiert als Ausgang und wird durch verschiedene Pins auf dem Arduino Uno R3 gesteuert.

Der an Pin 8 angeschlossene Taster ist jedoch anders. Er ist ein Eingabegerät. Pin 8 liest die eingehende Spannung, anstatt Spannung auszusenden.

Verwende ein Multimeter, um die Spannung an Pin 8 zu testen, wenn der Taster gedrückt und losgelassen wird. Du benötigst möglicherweise Hilfe von einem Freund, um den Taster während der Messung zu drücken.

1. Stelle das Multimeter auf den Gleichspannungsbereich 20 Volt ein.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Miss die Spannung an Pin 8, wenn der Taster nicht gedrückt ist. Berühre mit der roten Prüfspitze des Multimeters Pin 8 und mit der schwarzen Prüfspitze GND.

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

3. Notiere die gemessene Spannung in der Tabelle.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Tasterzustand
     - Pin 8 Spannung
     - Zustand
   * - Nicht gedrückt
     - *0,00 Volt*
     - 
   * - Gedrückt
     -
     - 

4. Bitte deinen Freund, dir beim Drücken des Tasters zu helfen, und miss weiterhin die Spannung an Pin 8.

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

5. Wenn der Taster gedrückt wird, notiere die Spannung an Pin 8 in der Tabelle.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Tasterzustand
     - Pin 8 Spannung
     - Zustand
   * - Nicht gedrückt
     - *0,00 Volt*
     - 
   * - Gedrückt
     - *≈4,97 Volt*
     - 

6. Arduino-Boards lesen Spannungen zwischen 0 und etwa 5 Volt an den Eingabepins und interpretieren diese als entweder ``LOW`` oder ``HIGH`` basierend auf einer Schwellenwertspannung. Für einen Pin, um als ``HIGH`` gelesen zu werden, muss er mehr als 3 Volt haben. Um als ``LOW`` gelesen zu werden, muss er weniger als 1,5 Volt haben.

   Basierend auf der gemessenen Spannung fülle den Zustand für Pin 8 aus.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Button State
     - Pin 8 Voltage
     - Pin 8 State
   * - Release
     - *0.00 volts*
     - *LOW*
   * - Press
     - *≈4.97 volts*
     - *HIGH*


**Bedingte Anweisungen**

Die Ampel sollte zwei verschiedene Verhaltensweisen zeigen, je nachdem, ob der Knopf gedrückt wird:

* Wenn der Knopf gedrückt wird, sollte der Code für den Fußgängerüberweg ausgeführt werden, und die grüne LED sollte blinken.
* Wenn der Knopf nicht gedrückt wird, sollte die Ampel wie zuvor programmiert normal funktionieren.

Um diese Verhaltensweisen zu programmieren, wirst du eine neue Codierungsfunktion verwenden, die als bedingte Anweisung bekannt ist.

Bedingte Anweisungen werden manchmal als ``if-then``-Anweisungen oder einfach als ``if``-Anweisung bezeichnet.
Sie ermöglichen es, bestimmte Codezeilen auszuführen, wenn eine bestimmte Bedingung oder ein Szenario zutrifft.

.. image:: img/if.png
    :width: 300
    :align: center

.. note::

    Im Alltag nutzt man oft bedingte Anweisungen, um Entscheidungen zu treffen, wie zum Beispiel:

    .. code-block:: Arduino

        start;
        if kalt;
        dann zieh eine Jacke an;
        ende;
        
In der Arduino-IDE sieht eine bedingte Anweisung so aus:

    .. code-block:: Arduino

        if (Bedingung) {
            Befehle, die ausgeführt werden, wenn die Bedingung wahr ist 
        }

Die ``Bedingung`` steht in Klammern und verwendet Vergleichsoperatoren, um zwei oder mehr Werte zu vergleichen. Diese Werte können Zahlen, Variablen oder Eingaben sein, die in das Arduino Uno R3 kommen.

Hier ist eine Liste der Vergleichsoperatoren und deren Verwendung in der Bedingung eines ``if``-Statements:

.. list-table::
    :widths: 20 20 60
    :header-rows: 1

    *   - Vergleichsoperator
        - Bedeutung
        - Beispiel
    *   - ==
        - Gleich
        - if (digitalRead(8) == HIGH) {etwas tun}
    *   - !=
        - Ungleich
        - if (digitalRead(5) != LOW) {etwas tun}
    *   - <
        - Kleiner als
        - if (distance < 100) {etwas tun}
    *   - >
        - Größer als
        - if (count > 5) {etwas tun}
    *   - <=
        - Kleiner oder gleich
        - if (number <= minValue) {etwas tun}
    *   - >=
        - Größer oder gleich
        - if (number >= maxValue) {etwas tun}

.. note::

    Der Vergleich auf Gleichheit verwendet zwei Gleichheitszeichen (``==``). Ein einzelnes Gleichheitszeichen (``=``) wird zum Zuweisen eines Wertes zu einer Variablen verwendet (in späteren Abschnitten erklärt), während zwei Gleichheitszeichen zum Vergleichen zweier Werte verwendet werden.

Wenn zwei Werte in einer Bedingung verglichen werden, kann das Ergebnis ``True`` oder ``False`` sein. Wenn die Bedingung ``True`` ist, werden die Befehle innerhalb der geschweiften Klammern ausgeführt. Wenn die Bedingung ``False`` ist, werden die Befehle innerhalb der Klammern übersprungen.

In der Programmierung können bedingte Anweisungen einfach oder komplex sein, mit mehreren Bedingungen und Szenarien. Du wirst als Nächstes die grundlegende Form der ``if``-Anweisungen verwenden.

**Knopf nicht gedrückt**

Aufbauend auf unserem Verständnis von bedingten Anweisungen wenden wir dieses Konzept an, um unser Ampelsketch zu erweitern. Da das Drücken eines Knopfes den Verkehrsfluss beeinflusst, fügen wir eine Bedingung hinzu, um den Zustand des Knopfes zu überwachen.

1. Aus unseren früheren Messungen der Spannung an Pin 8 wissen wir, dass, wenn der Knopf nicht gedrückt wird, Pin 8 auf ``LOW`` steht. Wenn also der Zustand von Pin 8 als ``LOW`` gelesen wird, bedeutet dies, dass der Knopf nicht gedrückt ist. Füge nun am Anfang der ``void loop()``-Funktion in deinem vorherigen Code die folgende Anweisung ein:

    .. code-block:: Arduino
        :emphasize-lines: 11,13

        void setup() {
            // Setup-Code, der einmal ausgeführt wird:
            pinMode(3, OUTPUT); // Setze Pin 3 als Ausgang
            pinMode(4, OUTPUT); // Setze Pin 4 als Ausgang
            pinMode(5, OUTPUT); // Setze Pin 5 als Ausgang
            pinMode(8, INPUT);  // Deklariere Pin 8 (Taste) als Eingang
        }

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            if (digitalRead(8) == LOW) {
                
            }

            digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus

            ...

Genau wie der Befehl ``digitalWrite()`` für Ausgangspins verwendet wird, wird der Befehl ``digitalRead()`` für Eingangspins verwendet. ``digitalRead(pin)`` ist der Befehl, um zu lesen, ob ein digitaler Pin ``HIGH`` oder ``LOW`` ist.

Hier ist die Syntax:

    * ``digitalRead(pin)``: Liest den Wert von einem angegebenen digitalen Pin, entweder ``HIGH`` oder ``LOW``.

        **Parameter**
            - ``pin``: Die Nummer des Arduino-Pins, von dem du lesen möchtest
        
        **Rückgabe**
            ``HIGH`` oder ``LOW``

2. Als Nächstes fügst du die Befehle ein, die ausgeführt werden sollen, wenn der Knopf nicht gedrückt wird. Diese Befehle hast du bereits erstellt, um die normale Ampelsteuerung durchzuführen.

    * Du kannst diese Befehle ausschneiden und innerhalb der geschweiften Klammern der ``if``-Anweisung einfügen,
    * Oder du verschiebst einfach die rechte geschweifte Klammer der ``if``-Anweisung nach der letzten Verzögerung.
    * Verwende die Methode, die dir am besten passt. Danach sollte deine ``void loop()``-Funktion in etwa so aussehen:

.. code-block:: Arduino
    :emphasize-lines: 11,24

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(3, OUTPUT); // Setze Pin 3 als Ausgang
        pinMode(4, OUTPUT); // Setze Pin 4 als Ausgang
        pinMode(5, OUTPUT); // Setze Pin 5 als Ausgang
        pinMode(8, INPUT);  // Deklariere Pin 8 (Taste) als Eingang
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(10000);           // Warte 10 Sekunden
            digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
            digitalWrite(4, HIGH);  // Schalte die LED an Pin 4 ein
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(3000);            // Warte 3 Sekunden
            digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, HIGH);  // Schalte die LED an Pin 5 ein
            delay(10000);           // Warte 10 Sekunden
        }
    }

Beachte, wie die Befehle innerhalb der ``if``-Anweisung eingerückt sind. Die Verwendung von Einrückungen hilft, deinen Code übersichtlich zu halten und verdeutlicht, welche Befehle innerhalb einer Funktion ausgeführt werden. Obwohl es ein paar Sekunden mehr in Anspruch nehmen kann, können Einrückungen, Zeilenumbrüche und Code-Kommentare das Erscheinungsbild deines Codes verbessern, was auf lange Sicht von Vorteil sein wird.

Ein häufiger Syntaxfehler ist das Vergessen der erforderlichen Anzahl von geschweiften Klammern. Manchmal wird die rechte Klammer in einer Funktion weggelassen oder zu viele rechte Klammern hinzugefügt. In deinem Sketch benötigt jede linke Klammer eine rechte Klammer. Eine korrekte Einrückung hilft dir auch, falsch platzierte Klammern zu beheben.




**Wenn der Knopf gedrückt wird**

Nun ist es an der Zeit, den Code zu schreiben, der es Fußgängern ermöglicht, die Straße zu überqueren, wenn der Knopf gedrückt wird.

Dazu benötigst du eine zweite bedingte Anweisung. Diesmal musst du jedoch den Wert von ``digitalRead()`` für Pin 8 mit ``HIGH`` statt ``LOW`` vergleichen.

Wenn der Knopf gedrückt wird, muss die Ampel den gesamten Fahrzeugverkehr stoppen und anzeigen, dass es sicher ist, die Straße zu überqueren. Um dies zu erreichen, schaltest du die roten und gelben LEDs aus und lässt die grüne LED blinken. Innerhalb der geschweiften Klammern deiner zweiten bedingten Anweisung fügst du drei ``digitalWrite()``-Befehle hinzu:

* Schalte die grüne LED, die mit Pin 3 verbunden ist, ein.
* Schalte die gelbe LED, die mit Pin 4 verbunden ist, aus.
* Schalte die rote LED, die mit Pin 5 verbunden ist, aus.

Lass dann die grüne LED blinken. Denke daran, dass die Blinkfrequenz durch deine ``delay()``-Anweisungen bestimmt wird.

Dein Sketch sollte ungefähr so aussehen:

.. code-block:: Arduino
    :emphasize-lines: 24-31

    void setup() {
        pinMode(3, OUTPUT);  // declare pin 3 (green LED) as output
        pinMode(4, OUTPUT);  // declare pin 4 (yellow LED) as output
        pinMode(5, OUTPUT);  // declare pin 5 (red LED) as output
        pinMode(8, INPUT);   // declare pin 8 (button) as input
    }

    void loop() {
        // Main code to run repeatedly:
        if (digitalRead(8) == LOW) {
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
        if (digitalRead(8) == HIGH) {  //if the button is pressed:
            digitalWrite(3, HIGH);       // Light up the LED on pin 3
            digitalWrite(4, LOW);        // Switch off the LED on pin 4
            digitalWrite(5, LOW);        // Switch off the LED on pin 5
            delay(500);                  // Wait half a second
            digitalWrite(3, LOW);        // Switch off the LED on pin 3
            delay(500);                  // Wait half a second
        }
    }

Lade deinen Code auf das Arduino Uno R3 hoch. Sobald der Sketch vollständig übertragen ist, wird der Code ausgeführt.

Beobachte das Verhalten deiner Ampel. Drücke den Knopf und warte, bis der Zyklus der Ampel abgeschlossen ist. Blinkt das grüne Fußgängersignal? Kehrt die Ampel nach dem Loslassen des Knopfes in den normalen Betriebsmodus zurück? Falls nicht, passe deinen Sketch an und lade ihn erneut auf das R3 hoch.

Wenn du fertig bist, speichere deinen Sketch.

**Frage**

Während des Testens wirst du vielleicht feststellen, dass die grüne LED nur blinkt, solange der Fußgängerschalter gedrückt gehalten wird. Fußgänger können die Straße jedoch nicht überqueren, während sie den Knopf kontinuierlich drücken. Wie kannst du den Code so ändern, dass die grüne LED nach dem Drücken des Fußgängerschalters lange genug leuchtet, um eine sichere Überquerung zu ermöglichen, ohne dass der Knopf ständig gedrückt gehalten werden muss? Schreibe die Pseudo-Code-Lösung in dein Notizbuch.

**Zusammenfassung**

In dieser Lektion haben wir uns mit der Integration eines Fußgängerknopfes in ein Ampelsystem beschäftigt, das eine reale Situation simuliert, in der der Fußgänger- und Fahrzeugverkehr ausgeglichen werden muss. Wir haben die Funktionsweise eines Schalters in einem elektronischen Schaltkreis erkundet und die ``digitalRead()``-Funktion genutzt, um die Eingaben des Schalters zu überwachen. Durch die Implementierung bedingter Anweisungen mit ``if``-Strukturen haben wir die Ampeln so programmiert, dass sie dynamisch auf Fußgängereingaben reagieren, und unser Verständnis interaktiver Systeme vertieft. Diese Lektion hat nicht nur unsere Fähigkeiten in der Arduino-Programmierung gestärkt, sondern auch die praktische Anwendung dieser Technologien im Alltag hervorgehoben.

