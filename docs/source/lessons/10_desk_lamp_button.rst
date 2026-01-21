.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!

10. ON/OFF Desk Lamp
====================================

In this lesson, you'll expand on your previous project by adding a practical feature to your adjustable desk lamp—a switchable button. This enhancement simulates a real-life scenario where desk lamps are turned on or off and then adjusted for brightness using a dimmer, mimicking everyday functionality more closely.

.. image:: img/10_desk_lamp_button.jpg
    :width: 500
    :align: center

* Learn to use the Serial Monitor for real-time data display.
* Implement the ``INPUT_PULLUP`` mode to manage button inputs efficiently.
* Understand how to detect changes from one state to another.
* Explore the characteristics of digital and analog signals
* Utilizing Conditional Statements (``if else``)

Build the Circuit
------------------------------------

**Components Needed**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Red LEDs
     - 1 * 220Ω Resistor
     - 1 * Potentiometer
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Button
     - 1 * USB Cable
     - 1 * Breadboard
     - Jumper Wires
   * - |list_button| 
     - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 



**Building Steps**

1. Start with the desk lamp circuit from the previous lesson.

.. image:: img/9_dimmer_led1_pin9.png
    :width: 500
    :align: center

2. Insert the button into the breadboard across the middle gap, with pins in holes 6E, 8E, 6J and 8J. 

.. note::

    If you're unsure how to insert the button, try both orientations. One way, the pin spacing will be slightly too narrow to fit.

.. image:: img/10_desk_lamp_button_button.png
    :width: 500
    :align: center

3. Connect the button's buttom-left pin to digital pin 7 on the Arduino Uno R3 with a long jumper wire, inserting one end into hole 8J and the other into pin 7.

.. image:: img/10_desk_lamp_button_p7.png
    :width: 500
    :align: center

4. Connect the button's top-right pin to the breadboard's negative rail with a short jumper wire, inserting one end into hole 6A and the other into the negative rail.

.. image:: img/10_desk_lamp_button_gnd.png
    :width: 500
    :align: center


Code Creation
-----------------

**Printing Button State**

1. Open the sketch you saved earlier, ``Lesson9_Desk_Lamp``. Hit "Save As..." from the "File" menu, and rename it to ``Lesson10_Desk_Lamp_Button``. Click "Save".

2. In Lesson 8, we used a button with a manually connected 10K pull-down resistor between GND and the button. However, in this circuit, we did not connect a resistor. Instead, we can use the Arduino software pull-up feature. You need to set the pin connected to the button as input while also setting it to ``PULLUP``.

.. code-block:: Arduino
    :emphasize-lines: 6

    int potValue = 0;

    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 8 as input with an internal pull-up resistor
    }

3. To utilize the Serial Monitor, you must include a command that initiates serial communication on the Arduino Uno R3. 

This command is typically placed in the ``void setup()`` section of the sketch. The command ``Serial.begin(baud)`` starts the serial communication, where ``baud`` represents the rate of data transfer per second between the computer and the Arduino Uno R3. Common baud rates are 9600 and 115200 bits per second.

.. code-block:: Arduino
    :emphasize-lines: 7

    int potValue = 0;

    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }


4. Before entering the ``void loop()``, we also need to create two variables to initialize the states of the button and the LED. The LED should be off when there is no interaction, so set it to LOW. Since the button uses an internal pull-up resistor, it will read as HIGH when not pressed.

.. code-block:: Arduino
    :emphasize-lines: 2,3

    int potValue = 0;  // Variable to store the value read from the potentiometer
    int ledState = LOW;          // Initial state of the LED
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

5. Now, in the ``void loop()``, first read the state of the button using ``digitalRead()`` and store it in the variable ``buttonState``. 

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
    }

6. You are now ready to use the Serial Monitor to print data. You will utilize ``Serial.print()`` to display data and other texts.

Here's how to use it:


    * ``Serial.print(val)`` or ``Serial.print(val, format)``: Prints data to the serial port as human-readable ASCII text. 

    **Parameters**
        - ``Serial``: serial port object.
        - ``val``: the value to print. Allowed data types: any data type.

    **Returns**
        ``print()`` returns the number of bytes written, though reading that number is optional. Data type: size_t.

This command can represent various data types and formats, including numbers, floating points, bytes, and strings. For example:

.. code-block:: Arduino

    Serial.print(78);                // outputs "78"
    Serial.print(78, BIN);           // outputs "1001110"
    Serial.print(1.23456);           // outputs "1.23"
    Serial.print(1.23456, 0);        // outputs "1"
    Serial.print('N');               // outputs "N"
    Serial.print("Hello world.");    // outputs "Hello world."


7. Now, use this command to print a prompt indicating the data about to be printed. This is helpful when differentiating multiple data prints at once.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
    }

8. Now print the value stored in the ``buttonState`` variable. To ensure each output appears on a new line in the Serial Monitor, use ``Serial.println()``, which adds a newline character at the end of the print statement.
    
.. note::

    Note the difference in printing characters or strings (which must be enclosed in quotes) versus variables that are inserted directly.
    
.. code-block:: Arduino
    :emphasize-lines: 14

    int potValue = 0;  // Variable to store the value read from the potentiometer
    int ledState = LOW;          // Initial state of the LED
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
    }

9. At this point, the code is essentially complete. Click "Upload" to upload the code to the Arduino Uno R3.

    .. note::

        Whenever data is transmitted from the board to the computer, you should see the TX LED on your Arduino Uno R3 flashing.

10. Afterward, click on the "Serial Monitor" button in the top right corner of the Arduino IDE.

    .. image:: img/10_dimmer_led_serial.png
        :align: center

11. If you see garbled data displayed, you will need to adjust the baud rate to match the one set in your code.

    .. image:: img/10_dimmer_led_serial_baud.png
        :align: center

12. You will find that when the button is not pressed, it continuously prints "1", and when the button is pressed, it continuously prints "0". This is the characteristic of a digital signal, which has only two states: “0” and “1”.

**Detecting Button State Changes**

In this segment, we're going to learn how a simple button can control an LED by toggling its state from ON to OFF and vice versa. This involves detecting the precise moment the button changes from not being pressed to being pressed.

1. Let's start with the core function that monitors the button press.

Previously, we learned how to determine if a button is pressed by reading its state as ``HIGH`` or ``LOW``. However, this lesson aims to respond to a single press without the need to keep the button held down. This requires us to detect a change in the button's state.

To achieve this, we use an ``if`` statement that compares the button's previous state (``lastButtonState``) with its current state (``buttonState``). The logical operator ``&&`` is used here, meaning both conditions must be true for the block of code within the ``if`` statement to execute.

.. code-block:: Arduino
    :emphasize-lines: 7,8

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
            
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
        }
    }

2. When the button is detected as pressed, we toggle the LED's state. This means if the LED was off, it turns on, and if it was on, it turns off. The ``!`` operator is used to invert the state of the ledState variable.


.. code-block:: Arduino
    :emphasize-lines: 8

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
            
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            ledState = !ledState;                               // Toggle LED state
        }
    }

3. After checking the button's state and updating the LED accordingly, we need to record the current state of the button as the new 'last known state'. This step is crucial for detecting the next state change.

.. code-block:: Arduino
    :emphasize-lines: 10,11

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
        
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            ledState = !ledState;                               // Toggle LED state
        }
        lastButtonState = buttonState;  // Update lastButtonState to the current state
        delay(200);                     // Optional: Simple software debouncing
        }

**Adjusting Brightness with a Potentiometer**

In scenarios where ``ledState`` is ``HIGH``, we want the LED not only to light up but also to have its brightness adjustable by a potentiometer. Here’s how you can implement this functionality:


1. Right after the ``if`` statement that toggles the LED state upon a button press, add another ``if`` statement to check if ``ledState`` is ``HIGH``. If it is, this is where we'll adjust the LED's brightness based on the potentiometer's value.


.. code-block:: Arduino
    :emphasize-lines: 10,12

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
        
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            ledState = !ledState;                               // Toggle LED state
        }
        if (ledState == HIGH) {

        }
        lastButtonState = buttonState;  // Update lastButtonState to the current state
        delay(200);                     // Optional: Simple software debouncing
    }

2. Inside the ``if (ledState == HIGH)`` block, read the potentiometer value to determine the brightness level. Then, apply this value to adjust the LED's brightness using ``analogWrite()``. Also, print this value to the Serial Monitor for real-time feedback.

.. code-block:: Arduino
    :emphasize-lines: 6-9

    // Check if button state has changed from the last loop iteration
    if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
        ledState = !ledState;                               // Toggle LED state
    }
    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Continuously read value from potentiometer when LED is on
        analogWrite(9, potValue / 4);  // Adjust brightness continuously
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    }
    lastButtonState = buttonState;  // Update lastButtonState to the current state
    delay(200);                     // Optional: Simple software debouncing

3. To ensure the LED turns off when ``ledState`` is ``LOW``, add an ``else`` statement following the ``if`` block. This will handle turning off the LED completely when the conditions within the ``if`` are not met.

.. image:: img/if_else.png
    :width: 400
    :align: center


.. code-block:: Arduino
    :emphasize-lines: 6-8

    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Continuously read value from potentiometer when LED is on
        analogWrite(9, potValue / 4);  // Adjust brightness continuously
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    } else {
        analogWrite(9, 0);  // Adjust brightness continuously
    }

**Running the Code**

Now that your code is complete, the full listing is as follows:

.. code-block:: Arduino

    int potValue = 0;            // Variable to store the value read from the potentiometer
    int ledState = LOW;          // Initial state of the LED
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);

        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            ledState = !ledState;                               // Toggle LED state
        }

        if (ledState == HIGH) {
            potValue = analogRead(A0);  // Continuously read value from potentiometer when LED is on
            analogWrite(9, potValue / 4);  // Adjust brightness continuously
            Serial.print("Pot Value: ");
            Serial.println(potValue);
        } else {
            analogWrite(9, 0);  // Adjust brightness continuously
        }

        lastButtonState = buttonState;  // Update lastButtonState to the current state
        delay(200);                     // Optional: Simple software debouncing
    }

1. After selecting the correct board and port, click "Upload" to upload the code to your Arduino.

2. Open the Serial Monitor to view the output data. You will notice that the button state prints "1" continuously when not pressed and "0" for the moment the button is pressed. At the same time, the value from the potentiometer will also be printed. As you rotate the potentiometer, you'll observe in the Serial Monitor that the higher the value, the brighter the LED becomes, and vice versa.
    
.. image:: img/10_dimmer_led_serial_tool.png
    :align: center

.. note::

    From this, you should clearly understand:

    - Digital signals only have two states: 0 and 1.
    - Analog signals, however, have a range, which in this case is from 0 to 1023.

3. Finally, remember to save your code and tidy up your workspace.

**Question**

1. What would happen if you set digital pin 7 to INPUT only? Why?

.. code-block::
    :emphasize-lines: 3

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

2. If pin 7 is set only to ``INPUT``, what adjustments would need to be made to the circuit?

**Summary**

By the end of this lesson, you'll have a fully functional ON/OFF desk lamp controlled via a simple user interface. You will have mastered how to integrate and manipulate various electronic components and Arduino programming techniques to create a practical and interactive electronic device. This project not only reinforces foundational concepts in electronics and programming but also gives you a functional piece to add to your collection of DIY projects.
