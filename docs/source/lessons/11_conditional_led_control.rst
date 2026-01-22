.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte de expertos**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Obtén acceso anticipado a anuncios y adelantos de nuevos productos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

11. Control de Arrays de LEDs con Potenciómetro
===================================================

¡Bienvenido a esta lección! Aquí exploraremos cómo dominar las sentencias condicionales para controlar arrays de LEDs de manera dinámica. Basándonos en nuestros conocimientos previos sobre circuitos simples de LEDs, esta lección te introduce a la lógica condicional más compleja, permitiendo que los LEDs respondan a diferentes niveles de entrada desde un potenciómetro. Este curso es ideal tanto para principiantes que están aprendiendo a programar sentencias condicionales como para programadores experimentados que desean profundizar su comprensión de las estructuras if-else if-else.

Al final de esta lección, no solo sabrás cómo programar los LEDs para que se enciendan en secuencia, sino que también comprenderás cómo usar estos patrones de iluminación para representar visualmente diferentes umbrales de entrada.

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/11_control_leds.mp4" type="video/mp4">
        Tu navegador no soporta la etiqueta de video.
    </video>


Construir el Circuito
------------------------------------

**Componentes necesarios**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 3 * LEDs rojos
     - 3 * Resistencias de 220Ω
     - 1 * Potenciómetro
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Cable USB
     - 1 * Protoboard
     - Cables jumper
     - 1 * Multímetro
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_meter|


**Pasos de Construcción**

Sigue el diagrama de cableado o los pasos a continuación para armar tu circuito.

.. image:: img/11_conditional_led_control_p9.png
    :width: 500
    :align: center

1. Conecta un potenciómetro a la protoboard. Inserta sus tres pines en los agujeros 30G, 29F, 28G.

.. note::
    El potenciómetro tiene una etiqueta "P 103", que indica su rango de resistencia. Inserta el potenciómetro en la protoboard como se muestra, con el lado etiquetado hacia ti.

.. image:: img/11_dimmer_test_pot.png
    :width: 500
    :align: center

2. Inserta un cable jumper en el agujero 28J y conéctalo al terminal negativo de la protoboard.

.. image:: img/11_conditional_led_control_pot_gnd.png
    :width: 500
    :align: center

3. Luego, inserta un cable jumper entre el agujero 29J y el pin A0 del Arduino Uno R3.

.. image:: img/11_conditional_led_control_a0.png
    :width: 500
    :align: center

4. Finalmente, conecta el potenciómetro a 5V insertando un cable jumper entre el agujero 30J de la protoboard y el pin de 5V del Arduino Uno R3.

.. image:: img/11_conditional_led_control_5v.png
    :width: 500
    :align: center

5. Conecta el pin GND del Arduino Uno R3 al terminal negativo de la protoboard utilizando un cable jumper largo.

.. image:: img/11_conditional_led_control_gnd.png
    :width: 500
    :align: center

6. Saca tres LEDs de cualquier color. Inserta sus ánodos (pines más largos) en los agujeros 15A, 11A y 7A respectivamente, y sus cátodos (pines más cortos) en el terminal negativo de la protoboard.

.. image:: img/11_conditional_led_control_3led.png
    :width: 500
    :align: center

7. Coloca una resistencia de 220 ohmios entre los agujeros 15E y 15G.

.. image:: img/11_conditional_led_control_1resistor.png
    :width: 500
    :align: center

8. De manera similar, inserta una resistencia de 220 ohmios entre los agujeros 11E y 11G, y otra entre los agujeros 7E y 7G.

.. image:: img/11_conditional_led_control_2resistor.png
    :width: 500
    :align: center

9. Conecta el agujero 15J de la protoboard al pin 11 del Arduino Uno R3 con un cable.

.. image:: img/11_conditional_led_control_p11.png
    :width: 500
    :align: center

10. Conecta el agujero 11J de la protoboard al pin 10 del Arduino Uno R3 con un cable.

.. image:: img/11_conditional_led_control_p10.png
    :width: 500
    :align: center

11. Conecta el agujero 7J de la protoboard al pin 9 del Arduino Uno R3 con un cable. Tu circuito ahora está completo.

.. image:: img/11_conditional_led_control_p9.png
    :width: 500
    :align: center

    
Creación de Código
-----------------------

**Escribir Pseudocódigo**

1. El pseudocódigo sirve como un boceto del programa, escrito en lenguaje sencillo para facilitar la comprensión. Tu tarea es crear un pseudocódigo para un array de LEDs que reaccione a un potenciómetro. A medida que aumenta el valor del potenciómetro, se encenderán más LEDs. Antes de escribir el pseudocódigo, responde estas preguntas:

.. code-block::

    - ¿Cómo lee el Arduino el valor del potenciómetro?
    - ¿Cómo se puede controlar cada LED individualmente?
    - ¿En cuántos rangos debería dividirse el valor del potenciómetro?
    - ¿Qué debería mostrar cada LED en estos rangos?

2. Escribe tu pseudocódigo para el array de LEDs en la sección en blanco provista en tu manual.

**Imprimir los valores del potenciómetro**

3. Para convertir tu pseudocódigo en un sketch funcional, abre el IDE de Arduino y comienza un nuevo proyecto seleccionando “Nuevo Sketch” en el menú “Archivo”.
4. Guarda tu sketch como ``Lesson11_LED_Array`` usando ``Ctrl + S`` o haciendo clic en “Guardar”.

5. Al igual que en lecciones anteriores, crea una variable antes del ``void setup()`` para almacenar el valor del potenciómetro y recuerda agregar comentarios que coincidan con la funcionalidad del código.

.. code-block:: Arduino
    :emphasize-lines: 1

    int potValue = 0;            // Variable para almacenar el valor leído del potenciómetro

    void setup() {
        // Código que se ejecuta una vez:

    }

6. Dado que los LEDs son dispositivos de salida, deberás configurar los pines digitales 9, 10 y 11 como OUTPUTs. Recuerda incluir comentarios.

.. code-block:: Arduino
    :emphasize-lines: 5,6,7

    int potValue = 0;            // Variable para almacenar el valor leído del potenciómetro

    void setup() {
        // Código que se ejecuta una vez:
        pinMode(9, OUTPUT);  // Configurar pin 9 como salida
        pinMode(10, OUTPUT); // Configurar pin 10 como salida
        pinMode(11, OUTPUT); // Configurar pin 11 como salida
    }

7. Inicia la comunicación serial configurando la velocidad en baudios a 9600.

.. code-block:: Arduino
    :emphasize-lines: 8

    int potValue = 0;            // Variable para almacenar el valor leído del potenciómetro

    void setup() {
        // Código que se ejecuta una vez:
        pinMode(9, OUTPUT);  // Configurar pin 9 como salida
        pinMode(10, OUTPUT); // Configurar pin 10 como salida
        pinMode(11, OUTPUT); // Configurar pin 11 como salida
        Serial.begin(9600);  // Iniciar comunicación serial a 9600 baudios
    }

8. Dentro del ``void loop()``, después de leer el valor del potenciómetro, guárdalo en la variable ``potValue`` e imprímelo en el monitor serial.

.. code-block:: Arduino
    :emphasize-lines: 12-15

    int potValue = 0;            // Variable para almacenar el valor leído del potenciómetro

    void setup() {
        pinMode(9, OUTPUT);  // Configurar pin 9 como salida
        pinMode(10, OUTPUT); // Configurar pin 10 como salida
        pinMode(11, OUTPUT); // Configurar pin 11 como salida
        Serial.begin(9600);  // Iniciar comunicación serial a 9600 baudios
    }

    void loop() {
        // Código principal que se ejecuta repetidamente:
        potValue = analogRead(A0);     // Leer valor del potenciómetro
        Serial.print("Pot Value: ");  // Mostrar la lectura
        Serial.println(potValue);      // Imprimir el valor del potenciómetro
        delay(100);
    }

9. Valida y compila tu código si es necesario.

10. Una vez que el código se haya cargado en el Arduino Uno R3, notarás que al girar el potenciómetro, el valor mostrado en el monitor serial varía entre 0 y 1023. Este rango es ideal, aunque debido a variaciones de fabricación, tu potenciómetro podría mostrar un rango de 50 a 1000. Solo recuerda este rango como referencia.


**Controlar LEDs con los valores del potenciómetro**

Para encender cada LED secuencialmente según el valor del potenciómetro, necesitarás varias condiciones. Puedes usar ``if`` para especificar acciones para diferentes rangos de valores del potenciómetro:
  
  - Por debajo de 200: Apaga todos los LEDs.
  - Entre 200 y 600: Enciende el primer LED.
  - Entre 600 y 1000: Enciende dos LEDs.
  - Por encima de 1000: Enciende todos los LEDs.

Sin embargo, gestionar estas condiciones por separado puede ser ineficiente, ya que el Arduino necesita verificar cada una en cada ciclo del bucle.

Para optimizar esto, utiliza la estructura ``if-else if``:

.. code-block:: Arduino

    if (condition 1) {
        // Execute if condition 1 is true
    }
    else if (condition 2) {
        // Execute if condition 2 is true
    }
    else if (condition 3) {
        // Execute if condition 3 is true
    }
    else {
        // Execute if none of the conditions are true
    }


.. image:: img/if_else_if.png
    :width: 500
    :align: center


En una estructura ``if-else if``, se prueba la primera condición. Si es verdadera, se ejecutan los comandos asociados y se saltan todas las demás condiciones (aunque algunas de ellas también sean verdaderas). Si la primera condición es falsa, se prueba la segunda condición en la estructura. Si la segunda condición es verdadera, se ejecutan los comandos asociados a esta condición y luego se omiten las demás. Si es falsa, se prueba la tercera condición, y así sucesivamente. En algunos escenarios, puede haber múltiples condiciones verdaderas. Por lo tanto, el orden de las condiciones es importante. Solo se ejecutarán los comandos asociados con la primera condición verdadera.


11. Primero, apaga los tres LEDs si el valor del potenciómetro es menor de 200. Añade una declaración if y luego usa la función digitalWrite() para establecer los pines 9, 10 y 11 en LOW para apagar los LEDs.

.. code-block:: Arduino
    :emphasize-lines: 7-11 
    
    void loop() {
        // Código principal que se ejecuta repetidamente:
        potValue = analogRead(A0);    // Leer el valor del potenciómetro
        Serial.print("Pot Value: ");  // Mostrar la lectura
        Serial.println(potValue);     // Imprimir el valor del potenciómetro
        delay(100);
        if (potValue < 200) {     // Si potValue es menor de 200
            digitalWrite(9, LOW);   // Apagar el LED en el pin 9
            digitalWrite(10, LOW);  // Apagar el LED en el pin 10
            digitalWrite(11, LOW);  // Apagar el LED en el pin 11
        }
    }

 
12. Añade una declaración ``else if`` para encender el primer LED cuando el valor analógico del potenciómetro esté por debajo de 600.

.. code-block:: Arduino
    :emphasize-lines: 5-9 
    
    if (potValue < 200) {         // Si potValue es menor de 200
        digitalWrite(9, LOW);       // Apagar el LED en el pin 9
        digitalWrite(10, LOW);      // Apagar el LED en el pin 10
        digitalWrite(11, LOW);      // Apagar el LED en el pin 11
    } else if (potValue < 600) {  // Si potValue es menor de 600
        digitalWrite(9, HIGH);      // Encender el LED en el pin 9
        digitalWrite(10, LOW);      // Apagar el LED en el pin 10
        digitalWrite(11, LOW);      // Apagar el LED en el pin 11
    }


13. Para encender dos LEDs cuando el valor esté por debajo de 1000, inserta otra condición ``else if`` como esta:

.. code-block:: Arduino
    :emphasize-lines: 10-14 
    
    if (potValue < 200) {         // Si potValue es menor de 200
        digitalWrite(9, LOW);       // Apagar el LED en el pin 9
        digitalWrite(10, LOW);      // Apagar el LED en el pin 10
        digitalWrite(11, LOW);      // Apagar el LED en el pin 11
    } else if (potValue < 600) {  // Si potValue es menor de 600
        digitalWrite(9, HIGH);      // Encender el LED en el pin 9
        digitalWrite(10, LOW);      // Apagar el LED en el pin 10
        digitalWrite(11, LOW);      // Apagar el LED en el pin 11
    }
    else if (potValue < 1000) {  // Si potValue es menor de 1000
        digitalWrite(9, HIGH);     // Encender el LED en el pin 9
        digitalWrite(10, HIGH);    // Encender el LED en el pin 10
        digitalWrite(11, LOW);     // Apagar el LED en el pin 11
    }    

14. Finalmente, modifica los comandos dentro del bloque ``else`` para encender los tres LEDs usando ``digitalWrite()``. Este bloque contiene los comandos que se ejecutan cuando ninguna de las otras condiciones es verdadera. En otras palabras, si el valor ``potValue`` del potenciómetro es mayor o igual a 1000, los comandos dentro de ``else {}`` se ejecutarán. Tu bloque ``else`` debería verse así:

.. code-block:: Arduino
    :emphasize-lines: 6-8 

    else if (potValue < 1000) {  // Si potValue es menor de 1000
        digitalWrite(9, HIGH);     // Encender el LED en el pin 9
        digitalWrite(10, HIGH);    // Encender el LED en el pin 10
        digitalWrite(11, LOW);     // Apagar el LED en el pin 11
    } else {
        digitalWrite(9, HIGH);   // Encender el LED en el pin 9
        digitalWrite(10, HIGH);  // Encender el LED en el pin 10
        digitalWrite(11, HIGH);  // Encender el LED en el pin 11
    }

15. Tu código completo es el siguiente. Haz clic en "Subir" para enviar el código a tu Arduino Uno R3.

.. code-block:: Arduino

    int potValue = 0;  // Variable para almacenar el valor leído del potenciómetro

    void setup() {
        pinMode(9, OUTPUT);   // Configurar el pin 9 como salida
        pinMode(10, OUTPUT);  // Configurar el pin 10 como salida
        pinMode(11, OUTPUT);  // Configurar el pin 11 como salida
        Serial.begin(9600);   // Iniciar la comunicación serial a 9600 baudios
    }

    void loop() {
        // Código principal que se ejecuta repetidamente:
        potValue = analogRead(A0);    // Leer el valor del potenciómetro
        Serial.print("Pot Value: ");  // Mostrar la lectura
        Serial.println(potValue);     // Imprimir el valor del potenciómetro
        delay(100);
        if (potValue < 200) {          // Si potValue es menor de 200
            digitalWrite(9, LOW);        // Apagar el LED en el pin 9
            digitalWrite(10, LOW);       // Apagar el LED en el pin 10
            digitalWrite(11, LOW);       // Apagar el LED en el pin 11
        } else if (potValue < 600) {   // Si potValue es menor de 600
            digitalWrite(9, HIGH);       // Encender el LED en el pin 9
            digitalWrite(10, LOW);       // Apagar el LED en el pin 10
            digitalWrite(11, LOW);       // Apagar el LED en el pin 11
        } else if (potValue < 1000) {  // Si potValue es menor de 1000
            digitalWrite(9, HIGH);       // Encender el LED en el pin 9
            digitalWrite(10, HIGH);      // Encender el LED en el pin 10
            digitalWrite(11, LOW);       // Apagar el LED en el pin 11
        } else {
            digitalWrite(9, HIGH);   // Encender el LED en el pin 9
            digitalWrite(10, HIGH);  // Encender el LED en el pin 10
            digitalWrite(11, HIGH);  // Encender el LED en el pin 11
        }
    }

16. Gira el potenciómetro para comprobar si el array de LEDs funciona como se espera:

   - Si el valor del potenciómetro es inferior a 200, todos los LEDs deberían estar apagados.
   - Si el valor está entre 200 y 600, el primer LED debería estar encendido.
   - Si el valor está entre 600 y 1000, los dos primeros LEDs deberían estar encendidos.
   - Si el valor supera los 1000, todos los LEDs deberían estar encendidos.

**Pregunta**

En el código, determinamos cuántos LEDs encender en función del valor del potenciómetro. ¿Cómo podemos modificar el código para que, al encender los LEDs, su brillo también cambie de acuerdo con el valor del potenciómetro?

**Resumen**

En esta lección completa, has aprendido a crear una pantalla interactiva de LEDs que responde a un potenciómetro. Comenzando con la construcción del circuito, has ensamblado un sistema que incorpora varios LEDs controlados a través de pines digitales, vinculados a un potenciómetro que ajusta sus estados en función de las lecturas. A través de instrucciones paso a paso, has programado con éxito tu Arduino para gestionar diferentes escenarios de iluminación basados en umbrales específicos del potenciómetro, mejorando tu comprensión de las interacciones entre hardware y software.

Este curso te ha proporcionado las habilidades para escribir estructuras condicionales eficientes, lo que permite que tus proyectos reaccionen a cambios precisos en las entradas de sensores. Al experimentar con diferentes condiciones, has visto de primera mano cómo el orden y la estructura de tu código afectan el rendimiento y la eficiencia de tus proyectos electrónicos.

