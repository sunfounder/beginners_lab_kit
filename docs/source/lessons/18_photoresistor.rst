.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!

18. Light Alarm
========================

.. image:: img/18_light_alarm.png
    :width: 600
    :align: center

Imagine a scene straight out of a movie:
In a dimly lit museum, a cunning thief quietly approaches a priceless painting.
He moves stealthily, attempting to carry out his theft under the cover of night.
However, the moment he touches the painting, a series of sophisticated sensors are triggered,
setting off alarms throughout the gallery, instantly illuminating the surrounding area.
The thief is quickly apprehended by on-site security personnel, preventing a potential art heist in its tracks.
This isn't a movie; this is a real-life example of sensor technology at work in modern security systems.

How is this achieved? This involves placing a photoresistor or a more sophisticated light sensor near the frame of the painting. Any attempt to move the painting or block it alters the light conditions, thus triggering the alarm system.

Now, let's build a simulated light alarm system using a photoresistor and a buzzer, shall we?

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/18_light_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In this lesson, you will learn:

* The working principles and characteristics of a photoresistor.
* How to build a simple light alarm system.


Building the Circuit
-----------------------

**Components Needed**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Photoresistor
     - 1 * 10KΩ Resistor
     - 1 * Active Buzzer
   * - |list_uno_r3| 
     - |list_photoresistor| 
     - |list_10kohm| 
     - |list_active_buzzer| 
   * - 1 * USB Cable
     - 1 * Breadboard
     - Jumper Wires
     - 1 * Multimeter
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_meter|



**Building Step-by-Step**

1. Start with a Photoresistor.

.. image:: img/17_photoresistor.png
    :width: 100
    :align: center

A photoresistor or photocell is a light-controlled variable resistor. The resistance of a photoresistor decreases with increasing incident light intensity; in other words, it exhibits photoconductivity.

Photoresistors can be used as resistive semiconductors in light-sensitive detector circuits and in light-activated and dark-activated switching circuits. In darkness, the resistance of a photoresistor can be as high as several megaohms (MΩ), while in lighted conditions, it can drop to a few hundred ohms.

The kit includes a resistor rated at 10K at 25°C. Now, use a multimeter to measure the resistance of the photoresistor under normal light, illuminated, and dark conditions.

2. Since the rated resistance of the photoresistor is 10K, set the multimeter to measure resistance in the 20 kilo-ohm (20K) range.

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

3. Insert the photoresistor into the breadboard at positions 10E and 11E. The pins are non-directional and can be inserted freely.

.. image:: img/17_light_alarm_photoresistor.png
    :width: 500
    :align: center

4. Now, touch the two pins of the photoresistor with the red and black test leads of the multimeter.

.. image:: img/17_light_alarm_test.png
    :width: 500
    :align: center

5. Read the resistance value under the current ambient light and record it in the table below.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Environment
     - Resistance (kilohm)
   * - Normal Light
     - *5.48*
   * - Bright Light
     -
   * - Darkness
     -

6. Now, have a friend help by shining a flashlight or another light source directly on the photoresistor, record the resistance value, which might be just a few hundred ohms. Therefore, you might need to set the multimeter to 2K, or even to 200 ohms for a more precise reading.

.. note::

    We've set the resistance unit in the table to kilohms. 1 kilohm (kΩ) = 1000 ohms.

    If you chose the 200 ohm range and got a reading of 164.5 ohms, convert it to 0.16 kilohms (rounding recommended to two decimal places), and enter the converted value in the table.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Environment
     - Resistance (kilohm)
   * - Normal Light
     - *≈5.48*
   * - Bright Light
     - *≈0.16*
   * - Darkness
     - 

7. For dark conditions, the resistance of the photoresistor can reach several megaohms, so we need to set the multimeter to the 2 megaohm position.

.. image:: img/multimeter_2mΩ.png
    :width: 300
    :align: center

8. Completely cover the photoresistor with a black object, then record the measured resistance in the table.

.. note::
    We have set the resistance unit in the table to kilohms. 1 megohm (MΩ) = 1000 kilohms.

    If you chose the 2 megaohm range and obtained a reading of 1.954 megohms, convert it to 1954 kilohms, which is the value you should enter.

    If the reading is directly higher than 2MΩ, it will display "1.", at which point you can directly enter 2 megohms, or you might consider using a more precise multimeter to measure the exact value.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Environment
     - Resistance (kilohm)
   * - Normal Light
     - *≈5.48*
   * - Bright Light
     - *≈0.16*
   * - Darkness
     - *≈1954*

From the measurements, we have confirmed the photoconductive properties of the photoresistor: the stronger the light, the lower the resistance; the dimmer the light, the higher the resistance, which can reach several megaohms.

9. Continue building the circuit. Connect one pin of the photoresistor to the negative terminal of the breadboard and the other pin to the A0 pin on the Arduino Uno R3.

.. image:: img/17_light_alarm_a0.png
    :width: 500
    :align: center

10. Insert a 10K resistor in the same row as the photoresistor's connection to A0.

.. image:: img/17_light_alarm_resistor.png
    :width: 500
    :align: center

In this circuit, the 10K resistor and the photoresistor are connected in series, and the current passing through them is the same. The 10K resistor acts as a protection, and the A0 pin reads the value after the voltage conversion of the photoresistor.

When the light is enhanced, the resistance of the photoresistor decreases, then its voltage decreases, so the value from the A0 pin will decrease; if the light is strong enough, the resistance of the photoresistor will be close to 0, and the value of the A0 pin will be close to 0. At this time, the 10K resistor plays a protective role, preventing a short circuit by keeping the 5V and GND from being directly connected.

If you place the photoresistor in a dark situation, the value of the A0 pin will increase. In a dark enough situation, the resistance of the photoresistor will be infinite, and its voltage will be close to 5V (the 10K resistor becomes negligible), and the value of the A0 pin will be close to 1023.

11. Connect the other pin of the 10K resistor to the 5V pin on the Arduino Uno R3.

.. image:: img/17_light_alarm_5v.png
    :width: 500
    :align: center

12. Next, as in the previous lesson, insert the active buzzer into the breadboard, connecting its anode to pin 9 of the R3 and its cathode to the negative terminal of the breadboard.

.. image:: img/17_light_alarm_buzzer.png
    :width: 500
    :align: center

13. Finally, connect the negative terminal of the breadboard to the GND pin on the Arduino Uno R3 with a jumper wire.


.. image:: img/17_light_alarm.png
    :width: 500
    :align: center

Code Creation
-------------
1. Open the Arduino IDE and start a new project by selecting “New Sketch” from the “File” menu.
2. Save your sketch as ``Lesson18_Light_Alarm`` using ``Ctrl + S`` or by clicking “Save”.

3. Before the ``void setup()``, create constants for the photoresistor and buzzer, as well as a constant threshold value that will trigger the alarm when the photoresistor's reading falls below it.

.. code-block:: Arduino
    :emphasize-lines: 1,2,3

    const int sensorPin = A0;   // Assigns the pin A0 to the constant for the photoresistor
    const int buzzerPin = 9;    // Assigns the pin 9 to the constant for the buzzer
    const int threshold = 300;  // Set the threshold value

    void setup() {
        // put your setup code here, to run once:
    }

4. Additionally, create a variable to store the value read from the photoresistor.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int sensorPin = A0;   // Assigns the pin A0 to the constant for the photoresistor
    const int buzzerPin = 9;    // Assigns the pin 9 to the constant for the buzzer
    const int threshold = 300;  // Set the threshold value

    int sensorValue = 0;  // To store the photoresistor reading

    void setup() {
        // put your setup code here, to run once:
    }

5. In the ``void setup()``, set the buzzer as an output and start serial communication to monitor the readings from the photoresistor.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void setup() {
        // put your setup code here, to run once:
        pinMode(buzzerPin, OUTPUT);  // Set the buzzer pin as an output
        Serial.begin(9600);          // Initialize serial communication at 9600 baud rate
    }

6. In the ``void loop()``, use the ``analogRead()`` function to read from the photoresistor and store the value in the variable ``sensorValue``. Then print this value to the serial monitor. Remember to set a time interval for each data reading.

.. code-block:: Arduino
    :emphasize-lines: 3,4,5

    void loop() {
        // put your main code here, to run repeatedly:
        sensorValue = analogRead(sensorPin);  // Read the analog value from the photoresistor
        Serial.println(sensorValue);          // Print the photoresistor reading to the serial monitor
        delay(100); // Wait 0.1 seconds
    }

7. When the environment shifts from dark to bright, the resistance of the photoresistor decreases, and so does the reading at pin A0. Now use an ``if`` statement to check if the photoresistor's value is below the ``threshold``; if it is, turn the buzzer on, otherwise, turn it off.

.. code-block:: Arduino
    :emphasize-lines: 7-12

    void loop() {
        // put your main code here, to run repeatedly:
        sensorValue = analogRead(sensorPin);  // Read the analog value from the photoresistor
        Serial.println(sensorValue);          // Print the photoresistor reading to the serial monitor
        delay(100);                           // Wait 0.1 seconds

        // Check if the reading is below the threshold
        if (sensorValue < threshold) {
            digitalWrite(buzzerPin, HIGH);  // If below threshold, turn on the buzzer
        } else {
            digitalWrite(buzzerPin, LOW);  // If not below threshold, turn off the buzzer
        }
    }

8. Here is your complete code. You can now click "Upload" to upload the code to the Arduino Uno R3.

.. code-block:: Arduino

    const int sensorPin = A0;   // Assigns the pin A0 to the constant for the photoresistor
    const int buzzerPin = 9;    // Assigns the pin 9 to the constant for the buzzer
    const int threshold = 300;  // Set the threshold value

    int sensorValue = 0;  // To store the photoresistor reading

    void setup() {
        // put your setup code here, to run once:
        pinMode(buzzerPin, OUTPUT);  // Set the buzzer pin as an output
        Serial.begin(9600);          // Initialize serial communication at 9600 baud rate
    }

    void loop() {
        // put your main code here, to run repeatedly:
        sensorValue = analogRead(sensorPin);  // Read the analog value from the photoresistor
        Serial.println(sensorValue);          // Print the photoresistor reading to the serial monitor
        delay(100);                           // Wait 0.1 seconds

        // Check if the reading is below the threshold
        if (sensorValue < threshold) {
            digitalWrite(buzzerPin, HIGH);  // If below threshold, turn on the buzzer
        } else {
            digitalWrite(buzzerPin, LOW);  // If not below threshold, turn off the buzzer
        }
    }

9. Finally, remember to save your code and tidy up your workspace.

**Question**

Cunning thieves might choose to steal at night, and if a painting disappears, 
the photoresistor might not be able to detect any change in light, thus failing to trigger an alarm. What can be done to improve this flaw?