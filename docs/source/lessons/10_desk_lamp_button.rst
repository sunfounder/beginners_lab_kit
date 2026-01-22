.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in Raspberry Pi, Arduino und ESP32 ein und tausche dich mit Gleichgesinnten aus.

    **Warum mitmachen?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte vorzeitigen Zugriff auf neue Produktankündigungen und Vorschauen.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu erschaffen? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

10. EIN/AUS-Schreibtischlampe
====================================

In dieser Lektion wirst du dein vorheriges Projekt erweitern, indem du deiner dimmbaren Schreibtischlampe eine praktische Funktion hinzufügst – einen schaltbaren Knopf. Diese Erweiterung simuliert ein reales Szenario, bei dem Schreibtischlampen ein- oder ausgeschaltet und anschließend in ihrer Helligkeit angepasst werden, um die alltägliche Funktionalität noch besser nachzuahmen.

.. image:: img/10_desk_lamp_button.jpg
    :width: 500
    :align: center

* Lerne, den seriellen Monitor zur Echtzeit-Datenanzeige zu verwenden.
* Setze den ``INPUT_PULLUP``-Modus ein, um Tasten-Eingänge effizient zu verwalten.
* Verstehe, wie Zustandsänderungen erkannt werden.
* Erforsche die Eigenschaften von digitalen und analogen Signalen.
* Verwende bedingte Anweisungen (``if else``).

Schaltung aufbauen
------------------------------------

**Benötigte Komponenten**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * 220Ω Widerstand
     - 1 * Potentiometer
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Taste
     - 1 * USB-Kabel
     - 1 * Breadboard
     - Jumperkabel
   * - |list_button| 
     - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 



**Aufbauschritte**

1. Beginne mit der Schreibtischlampenschaltung aus der vorherigen Lektion.

.. image:: img/9_dimmer_led1_pin9.png
    :width: 500
    :align: center

2. Setze die Taste in das Breadboard, sodass die Pins die Lücke in der Mitte des Breadboards überbrücken, und stecke die Pins in die Löcher 6E, 8E, 6J und 8J.

.. note::

    Wenn du dir unsicher bist, wie du die Taste einsetzen sollst, versuche beide Ausrichtungen. In einer Richtung ist der Pin-Abstand zu gering, um zu passen.

.. image:: img/10_desk_lamp_button_button.png
    :width: 500
    :align: center

3. Verbinde den unteren linken Pin der Taste mit dem digitalen Pin 7 des Arduino Uno R3 mittels eines langen Jumperkabels. Stecke ein Ende in Loch 8J und das andere Ende in Pin 7.

.. image:: img/10_desk_lamp_button_p7.png
    :width: 500
    :align: center

4. Verbinde den oberen rechten Pin der Taste mit der negativen Schiene des Breadboards mittels eines kurzen Jumperkabels. Stecke ein Ende in Loch 6A und das andere Ende in die negative Schiene.

.. image:: img/10_desk_lamp_button_gnd.png
    :width: 500
    :align: center


Code-Erstellung
-----------------

**Den Tastenzustand ausgeben**

1. Öffne den Sketch, den du zuvor gespeichert hast, ``Lesson9_Desk_Lamp``. Klicke auf "Speichern unter..." im Menü "Datei" und benenne ihn in ``Lesson10_Desk_Lamp_Button`` um. Klicke auf "Speichern".

2. In Lektion 8 haben wir eine Taste mit einem manuell angeschlossenen 10K-Pull-Down-Widerstand zwischen GND und der Taste verwendet. In dieser Schaltung haben wir jedoch keinen Widerstand angeschlossen. Stattdessen können wir die Pull-up-Funktion der Arduino-Software verwenden. Du musst den mit der Taste verbundenen Pin als Eingang festlegen und zusätzlich auf ``PULLUP`` setzen.

.. code-block:: Arduino
    :emphasize-lines: 6

    int potValue = 0;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);        // Setze Pin 9 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-up-Widerstand
    }

3. Um den seriellen Monitor zu nutzen, musst du einen Befehl hinzufügen, der die serielle Kommunikation auf dem Arduino Uno R3 startet.

Dieser Befehl wird normalerweise im Abschnitt ``void setup()`` des Sketches platziert. Der Befehl ``Serial.begin(baud)`` startet die serielle Kommunikation, wobei ``baud`` die Übertragungsrate der Daten pro Sekunde zwischen dem Computer und dem Arduino Uno R3 darstellt. Gängige Baudraten sind 9600 und 115200 Bit pro Sekunde.

.. code-block:: Arduino
    :emphasize-lines: 7

    int potValue = 0;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);        // Setze Pin 9 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-up-Widerstand
        Serial.begin(9600);        // Einrichtung der seriellen Kommunikation mit 9600 Baud
    }

4. Bevor du in die ``void loop()``-Funktion eintrittst, müssen wir zwei Variablen erstellen, um die Zustände der Taste und der LED zu initialisieren. Die LED sollte ausgeschaltet sein, wenn keine Interaktion stattfindet, also setze sie auf LOW. Da die Taste einen internen Pull-up-Widerstand verwendet, wird sie als HIGH gelesen, wenn sie nicht gedrückt wird.

.. code-block:: Arduino
    :emphasize-lines: 2,3

    int potValue = 0;  // Variable zur Speicherung des vom Potentiometer gelesenen Werts
    int ledState = LOW;          // Anfangszustand der LED
    int lastButtonState = HIGH;  // Vorherige Lesung vom Eingangs-Pin

    void setup() {
        pinMode(9, OUTPUT);        // Setze Pin 9 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-up-Widerstand
        Serial.begin(9600);        // Einrichtung der seriellen Kommunikation mit 9600 Baud
    }

5. Nun liest du im ``void loop()``-Abschnitt zuerst den Zustand des Knopfes mit ``digitalRead()`` und speicherst ihn in der Variable ``buttonState``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
    }

6. Du bist jetzt bereit, den seriellen Monitor zu verwenden, um Daten anzuzeigen. Du kannst ``Serial.print()`` nutzen, um Daten und andere Texte auszugeben.

Hier ist, wie du es verwendest:


    * ``Serial.print(val)`` oder ``Serial.print(val, format)``: Gibt Daten als lesbaren ASCII-Text an die serielle Schnittstelle aus.

    **Parameter**
        - ``Serial``: Serielles Port-Objekt.
        - ``val``: Der auszugebende Wert. Erlaubte Datentypen: jeder Datentyp.

    **Rückgabewert**
        ``print()`` gibt die Anzahl der geschriebenen Bytes zurück, aber das Lesen dieser Zahl ist optional. Datentyp: size_t.

Dieser Befehl kann verschiedene Datentypen und Formate darstellen, darunter Zahlen, Gleitkommazahlen, Bytes und Zeichenketten. Zum Beispiel:

.. code-block:: Arduino

    Serial.print(78);                // Gibt "78" aus
    Serial.print(78, BIN);           // Gibt "1001110" aus
    Serial.print(1.23456);           // Gibt "1.23" aus
    Serial.print(1.23456, 0);        // Gibt "1" aus
    Serial.print('N');               // Gibt "N" aus
    Serial.print("Hello world.");    // Gibt "Hello world." aus

7. Verwende diesen Befehl, um eine Nachricht zu drucken, die die anstehenden Daten ankündigt. Das hilft, mehrere Datenabdrucke zu unterscheiden.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
        Serial.print("Button State: ");
    }

8. Drucke nun den Wert, der in der Variable ``buttonState`` gespeichert ist. Damit jede Ausgabe im seriellen Monitor in einer neuen Zeile erscheint, verwende ``Serial.println()``, das ein Zeilenumbruchzeichen am Ende der Ausgabe hinzufügt.

.. note::

    Beachte den Unterschied beim Drucken von Zeichen oder Zeichenketten (die in Anführungszeichen gesetzt werden müssen) gegenüber Variablen, die direkt eingefügt werden.

.. code-block:: Arduino
    :emphasize-lines: 14

    int potValue = 0;  // Variable zur Speicherung des vom Potentiometer gelesenen Werts
    int ledState = LOW;          // Anfangszustand der LED
    int lastButtonState = HIGH;  // Die vorherige Lesung vom Eingangs-Pin

    void setup() {
        pinMode(9, OUTPUT);        // Setze Pin 9 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-up-Widerstand
        Serial.begin(9600);        // Einrichtung der seriellen Kommunikation mit 9600 Baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
        Serial.print("Knopfzustand: ");
        Serial.println(buttonState);  // Drucke den aktuellen Zustand des Knopfes
    }

9. An diesem Punkt ist der Code im Wesentlichen fertig. Klicke auf "Hochladen", um den Code auf das Arduino Uno R3 zu übertragen.

    .. note::


        Wann immer Daten von der Platine zum Computer übertragen werden, sollte die TX-LED auf deinem Arduino Uno R3 blinken.

10. Klicke danach auf den "Serieller Monitor"-Button in der oberen rechten Ecke der Arduino IDE.

    .. image:: img/10_dimmer_led_serial.png
        :align: center

11. Wenn du wirre Daten siehst, musst du die Baudrate so einstellen, dass sie der im Code eingestellten Baudrate entspricht.

    .. image:: img/10_dimmer_led_serial_baud.png
        :align: center

12. Du wirst feststellen, dass beim Nichtdrücken der Taste kontinuierlich "1" ausgegeben wird und beim Drücken "0". Dies ist typisch für ein digitales Signal, das nur zwei Zustände hat: „0“ und „1“.

**Erkennen von Zustandsänderungen der Taste**

In diesem Abschnitt lernen wir, wie eine einfache Taste eine LED steuern kann, indem ihr Zustand zwischen EIN und AUS umgeschaltet wird. Dabei wird der Moment erkannt, in dem die Taste von „nicht gedrückt“ zu „gedrückt“ wechselt.

1. Beginnen wir mit der Kernfunktion, die den Tastendruck überwacht.

Zuvor haben wir gelernt, wie man den Zustand einer Taste als ``HIGH`` oder ``LOW`` erkennt. In dieser Lektion geht es jedoch darum, auf einen einzelnen Tastendruck zu reagieren, ohne die Taste gedrückt halten zu müssen. Dafür müssen wir eine Änderung im Zustand der Taste erkennen.

Um dies zu erreichen, verwenden wir eine ``if``-Anweisung, die den vorherigen Zustand der Taste (``lastButtonState``) mit dem aktuellen Zustand (``buttonState``) vergleicht. Der logische Operator ``&&`` wird verwendet, was bedeutet, dass beide Bedingungen zutreffen müssen, damit der Code innerhalb der ``if``-Anweisung ausgeführt wird.

.. code-block:: Arduino
    :emphasize-lines: 7,8

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Drucke den aktuellen Zustand der Taste
            
        // Prüfe, ob sich der Zustand der Taste seit der letzten Iteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
        }
    }

2. Wenn der Tastendruck erkannt wird, schalten wir den Zustand der LED um. Das bedeutet, wenn die LED ausgeschaltet war, wird sie eingeschaltet und umgekehrt. Der ``!``-Operator wird verwendet, um den Zustand der Variable ``ledState`` umzukehren.

.. code-block:: Arduino
    :emphasize-lines: 8

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Drucke den aktuellen Zustand der Taste
            
        // Prüfe, ob sich der Zustand der Taste seit der letzten Iteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
            ledState = !ledState;                               // LED-Zustand umschalten
        }
    }

3. Nachdem wir den Tastendruck überprüft und die LED entsprechend aktualisiert haben, müssen wir den aktuellen Zustand der Taste als neuen „letzten bekannten Zustand“ speichern. Dieser Schritt ist entscheidend, um die nächste Zustandsänderung zu erkennen.

.. code-block:: Arduino
    :emphasize-lines: 10,11

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Drucke den aktuellen Zustand der Taste
        
        // Prüfe, ob sich der Zustand der Taste seit der letzten Iteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
            ledState = !ledState;                               // LED-Zustand umschalten
        }
        lastButtonState = buttonState;  // Aktualisiere lastButtonState auf den aktuellen Zustand
        delay(200);                     // Optional: Einfache Software-Entprellung
        }
        
**Helligkeitsanpassung mit einem Potentiometer**

In Situationen, in denen ``ledState`` auf ``HIGH`` gesetzt ist, soll die LED nicht nur leuchten, sondern ihre Helligkeit soll auch über ein Potentiometer einstellbar sein. So kannst du diese Funktionalität umsetzen:

1. Direkt nach der ``if``-Anweisung, die den LED-Zustand beim Drücken des Knopfes umschaltet, fügst du eine weitere ``if``-Anweisung hinzu, um zu überprüfen, ob ``ledState`` auf ``HIGH`` gesetzt ist. Falls dies der Fall ist, passt du hier die Helligkeit der LED basierend auf dem Wert des Potentiometers an.

.. code-block:: Arduino
    :emphasize-lines: 10,12

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Drucke den aktuellen Zustand des Knopfes

        // Prüfe, ob sich der Zustand des Knopfes seit der letzten Iteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Knopfdruck erkannt
            ledState = !ledState;                               // LED-Zustand umschalten
        }
        if (ledState == HIGH) {

        }
        lastButtonState = buttonState;  // Aktualisiere lastButtonState auf den aktuellen Zustand
        delay(200);                     // Optional: Einfache Software-Entprellung
    }

2. Innerhalb des Blocks ``if (ledState == HIGH)`` liest du den Potentiometerwert, um das Helligkeitsniveau zu bestimmen. Wende diesen Wert dann an, um die Helligkeit der LED mit ``analogWrite()`` anzupassen. Außerdem gibst du diesen Wert auf dem seriellen Monitor aus, um eine Echtzeit-Rückmeldung zu erhalten.

.. code-block:: Arduino
    :emphasize-lines: 6-9

    // Prüfe, ob sich der Zustand des Knopfes seit der letzten Iteration geändert hat
    if (lastButtonState == HIGH && buttonState == LOW) {  // Knopfdruck erkannt
        ledState = !ledState;                               // LED-Zustand umschalten
    }
    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Lese kontinuierlich den Wert des Potentiometers, wenn die LED an ist
        analogWrite(9, potValue / 4);  // Passe die Helligkeit kontinuierlich an
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    }
    lastButtonState = buttonState;  // Aktualisiere lastButtonState auf den aktuellen Zustand
    delay(200);                     // Optional: Einfache Software-Entprellung

3. Um sicherzustellen, dass die LED ausgeschaltet wird, wenn ``ledState`` auf ``LOW`` gesetzt ist, füge nach dem ``if``-Block eine ``else``-Anweisung hinzu. Diese sorgt dafür, dass die LED komplett ausgeschaltet wird, wenn die Bedingungen im ``if``-Block nicht erfüllt sind.

.. image:: img/if_else.png
    :width: 400
    :align: center


.. code-block:: Arduino
    :emphasize-lines: 6-8

    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Lese kontinuierlich den Wert des Potentiometers, wenn die LED an ist
        analogWrite(9, potValue / 4);  // Passe die Helligkeit kontinuierlich an
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    } else {
        analogWrite(9, 0);  // Schalte die LED aus
    }

**Code-Ausführung**

Jetzt, da dein Code vollständig ist, sieht das gesamte Programm wie folgt aus:

.. code-block:: Arduino

    int potValue = 0;            // Variable zur Speicherung des Potentiometerwerts
    int ledState = LOW;          // Anfangszustand der LED
    int lastButtonState = HIGH;  // Der vorherige Lesewert des Eingangs-Pins

    void setup() {
        pinMode(9, OUTPUT);        // Setze Pin 9 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-up-Widerstand
        Serial.begin(9600);        // Einrichtung der seriellen Kommunikation mit 9600 Baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Lese den Zustand des Knopfes
        Serial.print("Button State: ");
        Serial.println(buttonState);

        // Prüfe, ob sich der Zustand des Knopfes seit der letzten Iteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Knopfdruck erkannt
            ledState = !ledState;                               // LED-Zustand umschalten
        }

        if (ledState == HIGH) {
            potValue = analogRead(A0);  // Lese kontinuierlich den Wert des Potentiometers, wenn die LED an ist
            analogWrite(9, potValue / 4);  // Passe die Helligkeit kontinuierlich an
            Serial.print("Pot Value: ");
            Serial.println(potValue);
        } else {
            analogWrite(9, 0);  // Schalte die LED aus
        }

        lastButtonState = buttonState;  // Aktualisiere lastButtonState auf den aktuellen Zustand
        delay(200);                     // Optional: Einfache Software-Entprellung
    }

1. Nachdem du das richtige Board und den richtigen Port ausgewählt hast, klicke auf „Hochladen“, um den Code auf dein Arduino zu übertragen.

2. Öffne den seriellen Monitor, um die Ausgabedaten anzuzeigen. Du wirst bemerken, dass der Knopfzustand kontinuierlich "1" druckt, wenn er nicht gedrückt ist, und "0", wenn er gedrückt wird. Gleichzeitig wird der Wert des Potentiometers ebenfalls ausgegeben. Wenn du das Potentiometer drehst, wirst du feststellen, dass die LED umso heller wird, je höher der Wert ist, und umgekehrt.

.. image:: img/10_dimmer_led_serial_tool.png
    :align: center

.. note::

    Daraus solltest du klar erkennen:

    - Digitale Signale haben nur zwei Zustände: 0 und 1.
    - Analoge Signale hingegen haben einen Bereich, der in diesem Fall von 0 bis 1023 reicht.

3. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Fragen**

1. Was würde passieren, wenn du Pin 7 nur auf INPUT setzen würdest? Warum?

.. code-block::
    :emphasize-lines: 3

    void setup() {
        pinMode(9, OUTPUT);        // Setze Pin 9 als Ausgang
        pinMode(7, INPUT);  // Setze Pin 7 als Eingang ohne internen Pull-up-Widerstand
        Serial.begin(9600);        // Einrichtung der seriellen Kommunikation mit 9600 Baud
    }

2. Wenn Pin 7 nur auf ``INPUT`` gesetzt ist, welche Anpassungen müssten am Schaltkreis vorgenommen werden?

**Zusammenfassung**

Am Ende dieser Lektion hast du eine voll funktionsfähige EIN/AUS-Schreibtischlampe, die über eine einfache Benutzeroberfläche gesteuert wird. Du hast gelernt, wie du verschiedene elektronische Komponenten integrierst und Arduino-Programmiertechniken anwendest, um ein praktisches und interaktives elektronisches Gerät zu entwickeln. Dieses Projekt festigt nicht nur grundlegende Konzepte in Elektronik und Programmierung, sondern liefert dir auch ein funktionales Stück, das du deiner Sammlung von DIY-Projekten hinzufügen kannst.

