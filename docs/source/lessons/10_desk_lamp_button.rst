.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte de expertos**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Obtén acceso anticipado a anuncios y adelantos de nuevos productos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

10. Lámpara de escritorio ON/OFF
====================================

En esta lección, ampliarás tu proyecto anterior añadiendo una característica práctica a tu lámpara de escritorio regulable: un botón conmutable. Esta mejora simula un escenario real en el que las lámparas de escritorio se encienden o apagan y luego se ajustan para controlar el brillo mediante un regulador, imitando más de cerca la funcionalidad cotidiana.

.. image:: img/10_desk_lamp_button.jpg
    :width: 500
    :align: center

* Aprende a usar el Monitor Serial para mostrar datos en tiempo real.
* Implementa el modo ``INPUT_PULLUP`` para gestionar entradas de botones de forma eficiente.
* Entiende cómo detectar cambios de un estado a otro.
* Explora las características de las señales digitales y analógicas.
* Usa sentencias condicionales (``if else``).

Construye el Circuito
------------------------------------

**Componentes necesarios**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rojo
     - 1 * Resistencia de 220Ω
     - 1 * Potenciómetro
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Botón
     - 1 * Cable USB
     - 1 * Protoboard
     - Cables jumper
   * - |list_button| 
     - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 


**Pasos de Construcción**

1. Comienza con el circuito de la lámpara de escritorio de la lección anterior.

.. image:: img/9_dimmer_led1_pin9.png
    :width: 500
    :align: center

2. Inserta el botón en la protoboard cruzando la separación central, con los pines en los agujeros 6E, 8E, 6J y 8J.

.. note::

    Si no estás seguro de cómo insertar el botón, prueba ambas orientaciones. En una de las posiciones, el espaciado entre pines será ligeramente demasiado estrecho para encajar.

.. image:: img/10_desk_lamp_button_button.png
    :width: 500
    :align: center

3. Conecta el pin inferior izquierdo del botón al pin digital 7 en el Arduino Uno R3 con un cable jumper largo, insertando un extremo en el agujero 8J y el otro en el pin 7.

.. image:: img/10_desk_lamp_button_p7.png
    :width: 500
    :align: center

4. Conecta el pin superior derecho del botón al riel negativo de la protoboard con un cable jumper corto, insertando un extremo en el agujero 6A y el otro en el riel negativo.

.. image:: img/10_desk_lamp_button_gnd.png
    :width: 500
    :align: center


Creación del Código
------------------------

**Imprimiendo el Estado del Botón**

1. Abre el sketch que guardaste anteriormente, ``Lesson9_Desk_Lamp``. Selecciona "Guardar como..." desde el menú "Archivo", y renómbralo como ``Lesson10_Desk_Lamp_Button``. Haz clic en "Guardar".

2. En la lección 8, usamos un botón con una resistencia de pull-down de 10K manualmente conectada entre GND y el botón. Sin embargo, en este circuito, no conectamos una resistencia. En su lugar, podemos utilizar la función de pull-up del software de Arduino. Necesitas configurar el pin conectado al botón como entrada y también configurarlo en ``PULLUP``.

.. code-block:: Arduino
    :emphasize-lines: 6

    int potValue = 0;

    void setup() {
        // Configura el código aquí, se ejecuta una vez:
        pinMode(9, OUTPUT);        // Configura el pin 9 como salida
        pinMode(7, INPUT_PULLUP);  // Configura el pin 7 como entrada con resistencia pull-up interna
    }

3. Para utilizar el Monitor Serial, debes incluir un comando que inicie la comunicación serial en el Arduino Uno R3. 

Este comando generalmente se coloca en la sección ``void setup()`` del sketch. El comando ``Serial.begin(baud)`` inicia la comunicación serial, donde ``baud`` representa la tasa de transferencia de datos por segundo entre la computadora y el Arduino Uno R3. Las tasas de baud comunes son 9600 y 115200 bits por segundo.

.. code-block:: Arduino
    :emphasize-lines: 7

    int potValue = 0;

    void setup() {
        // Configura el código aquí, se ejecuta una vez:
        pinMode(9, OUTPUT);        // Configura el pin 9 como salida
        pinMode(7, INPUT_PULLUP);  // Configura el pin 7 como entrada con resistencia pull-up interna
        Serial.begin(9600);        // Configura la comunicación serial a 9600 baudios
    }


4. Antes de entrar en el ``void loop()``, también necesitamos crear dos variables para inicializar los estados del botón y del LED. El LED debe estar apagado cuando no haya interacción, por lo que se configura en LOW. Dado que el botón usa una resistencia pull-up interna, se leerá como HIGH cuando no esté presionado.

.. code-block:: Arduino
    :emphasize-lines: 2,3

    int potValue = 0;  // Variable para almacenar el valor leído del potenciómetro
    int ledState = LOW;          // Estado inicial del LED
    int lastButtonState = HIGH;  // La lectura previa del pin de entrada

    void setup() {
        pinMode(9, OUTPUT);        // Configura el pin 9 como salida
        pinMode(7, INPUT_PULLUP);  // Configura el pin 7 como entrada con resistencia pull-up interna
        Serial.begin(9600);        // Configura la comunicación serial a 9600 baudios
    }

5. Ahora, en el ``void loop()``, primero lee el estado del botón usando ``digitalRead()`` y almacénalo en la variable ``buttonState``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
    }

6. Ahora estás listo para usar el Monitor Serial para imprimir datos. Utilizarás ``Serial.print()`` para mostrar datos y otros textos.

Así es como se utiliza:


    * ``Serial.print(val)`` o ``Serial.print(val, format)``: Imprime datos en el puerto serial como texto ASCII legible para humanos.

    **Parámetros**
        - ``Serial``: objeto del puerto serial.
        - ``val``: el valor a imprimir. Tipos de datos permitidos: cualquier tipo de dato.

    **Devuelve**
        ``print()`` devuelve el número de bytes escritos, aunque leer ese número es opcional. Tipo de dato: size_t.

Este comando puede representar varios tipos de datos y formatos, incluidos números, puntos flotantes, bytes y cadenas. Por ejemplo:

.. code-block:: Arduino

    Serial.print(78);                // muestra "78"
    Serial.print(78, BIN);           // muestra "1001110"
    Serial.print(1.23456);           // muestra "1.23"
    Serial.print(1.23456, 0);        // muestra "1"
    Serial.print('N');               // muestra "N"
    Serial.print("Hello world.");    // muestra "Hello world."

7. Ahora, usa este comando para imprimir un mensaje que indique los datos que están a punto de imprimirse. Esto es útil para diferenciar múltiples impresiones de datos al mismo tiempo.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
        Serial.print("Button State: ");
    }

8. Ahora imprime el valor almacenado en la variable ``buttonState``. Para asegurar que cada salida aparezca en una nueva línea en el Monitor Serial, usa ``Serial.println()``, que añade un carácter de nueva línea al final de la declaración de impresión.

.. note::

    Nota la diferencia entre imprimir caracteres o cadenas (que deben ir entre comillas) y variables, que se insertan directamente.

.. code-block:: Arduino
    :emphasize-lines: 14

    int potValue = 0;  // Variable para almacenar el valor leído del potenciómetro
    int ledState = LOW;          // Estado inicial del LED
    int lastButtonState = HIGH;  // la lectura previa del pin de entrada

    void setup() {
        pinMode(9, OUTPUT);        // Configurar el pin 9 como salida
        pinMode(7, INPUT_PULLUP);  // Configurar el pin 7 como entrada con resistencia pull-up interna
        Serial.begin(9600);        // Configurar la comunicación serial a 9600 baudios
    }

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Imprimir el estado actual del botón
    }

9. En este punto, el código está esencialmente completo. Haz clic en "Subir" para cargar el código en el Arduino Uno R3.

    .. note::

        Cada vez que se transmita un dato de la placa a la computadora, deberías ver el LED TX de tu Arduino Uno R3 parpadeando.

10. Luego, haz clic en el botón "Monitor Serial" en la esquina superior derecha del IDE de Arduino.

    .. image:: img/10_dimmer_led_serial.png
        :align: center

11. Si ves datos ilegibles, necesitarás ajustar la velocidad en baudios para que coincida con la configurada en tu código.

    .. image:: img/10_dimmer_led_serial_baud.png
        :align: center

12. Verás que cuando el botón no está presionado, imprime continuamente "1", y cuando el botón está presionado, imprime continuamente "0". Esta es la característica de una señal digital, que solo tiene dos estados: “0” y “1”.

**Detectando Cambios de Estado del Botón**

En este segmento, aprenderemos cómo un botón simple puede controlar un LED alternando su estado de ENCENDIDO a APAGADO y viceversa. Esto implica detectar el momento preciso en que el botón cambia de no estar presionado a estarlo.

1. Comencemos con la función principal que monitorea la pulsación del botón.

Anteriormente, aprendimos cómo determinar si un botón está presionado leyendo su estado como ``HIGH`` o ``LOW``. Sin embargo, esta lección pretende responder a una única pulsación sin necesidad de mantener presionado el botón. Esto requiere detectar un cambio en el estado del botón.

Para lograrlo, usamos una sentencia ``if`` que compara el estado anterior del botón (``lastButtonState``) con su estado actual (``buttonState``). El operador lógico ``&&`` se usa aquí, lo que significa que ambas condiciones deben ser verdaderas para que el bloque de código dentro de la sentencia ``if`` se ejecute.

.. code-block:: Arduino
    :emphasize-lines: 7,8

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Imprimir el estado actual del botón
            
        // Comprobar si el estado del botón ha cambiado desde la última iteración del bucle
        if (lastButtonState == HIGH && buttonState == LOW) {  // Se detectó pulsación de botón
        }
    }

2. Cuando se detecta que el botón ha sido presionado, alternamos el estado del LED. Esto significa que si el LED estaba apagado, se encenderá, y si estaba encendido, se apagará. El operador ``!`` se utiliza para invertir el estado de la variable ledState.

.. code-block:: Arduino
    :emphasize-lines: 8

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Imprimir el estado actual del botón
            
        // Comprobar si el estado del botón ha cambiado desde la última iteración del bucle
        if (lastButtonState == HIGH && buttonState == LOW) {  // Se detectó pulsación de botón
            ledState = !ledState;                               // Alternar estado del LED
        }
    }

3. Después de verificar el estado del botón y actualizar el LED en consecuencia, necesitamos registrar el estado actual del botón como el nuevo 'estado conocido'. Este paso es crucial para detectar el próximo cambio de estado.

.. code-block:: Arduino
    :emphasize-lines: 10,11

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Imprimir el estado actual del botón
        
        // Verificar si el estado del botón ha cambiado desde la última iteración del bucle
        if (lastButtonState == HIGH && buttonState == LOW) {  // Se detectó una pulsación
            ledState = !ledState;                               // Alternar estado del LED
        }
        lastButtonState = buttonState;  // Actualizar lastButtonState al estado actual
        delay(200);                     // Opcional: Debouncing simple por software
    }

**Ajustando el Brillo con un Potenciómetro**

En escenarios donde ``ledState`` es ``HIGH``, queremos que el LED no solo se encienda, sino que también tenga su brillo ajustable mediante un potenciómetro. Así es como puedes implementar esta funcionalidad:

1. Justo después de la declaración ``if`` que alterna el estado del LED al presionar el botón, agrega otra declaración ``if`` para verificar si ``ledState`` está en ``HIGH``. Si lo está, ajustaremos el brillo del LED basado en el valor del potenciómetro.

.. code-block:: Arduino
    :emphasize-lines: 10,12

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Imprimir el estado actual del botón
        
        // Verificar si el estado del botón ha cambiado desde la última iteración del bucle
        if (lastButtonState == HIGH && buttonState == LOW) {  // Se detectó una pulsación
            ledState = !ledState;                               // Alternar estado del LED
        }
        if (ledState == HIGH) {

        }
        lastButtonState = buttonState;  // Actualizar lastButtonState al estado actual
        delay(200);                     // Opcional: Debouncing simple por software
    }

2. Dentro del bloque ``if (ledState == HIGH)``, lee el valor del potenciómetro para determinar el nivel de brillo. Luego, aplica este valor para ajustar el brillo del LED usando ``analogWrite()``. Además, imprime este valor en el Monitor Serial para obtener retroalimentación en tiempo real.

.. code-block:: Arduino
    :emphasize-lines: 6-9

    // Verificar si el estado del botón ha cambiado desde la última iteración del bucle
    if (lastButtonState == HIGH && buttonState == LOW) {  // Se detectó una pulsación
        ledState = !ledState;                               // Alternar estado del LED
    }
    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Leer continuamente el valor del potenciómetro cuando el LED esté encendido
        analogWrite(9, potValue / 4);  // Ajustar brillo continuamente
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    }
    lastButtonState = buttonState;  // Actualizar lastButtonState al estado actual
    delay(200);                     // Opcional: Debouncing simple por software

3. Para asegurarte de que el LED se apague cuando ``ledState`` esté en ``LOW``, agrega una declaración ``else`` después del bloque ``if``. Esto manejará el apagado completo del LED cuando no se cumplan las condiciones dentro del ``if``.

.. image:: img/if_else.png
    :width: 400
    :align: center

.. code-block:: Arduino
    :emphasize-lines: 6-8

    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Leer continuamente el valor del potenciómetro cuando el LED esté encendido
        analogWrite(9, potValue / 4);  // Ajustar brillo continuamente
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    } else {
        analogWrite(9, 0);  // Apagar el LED
    }

**Ejecutando el Código**

Ahora que tu código está completo, el listado completo es el siguiente:

.. code-block:: Arduino

    int potValue = 0;            // Variable para almacenar el valor leído del potenciómetro
    int ledState = LOW;          // Estado inicial del LED
    int lastButtonState = HIGH;  // La lectura previa del pin de entrada

    void setup() {
        pinMode(9, OUTPUT);        // Configurar el pin 9 como salida
        pinMode(7, INPUT_PULLUP);  // Configurar el pin 7 como entrada con resistencia pull-up interna
        Serial.begin(9600);        // Configurar la comunicación serial a 9600 baudios
    }

    void loop() {
        int buttonState = digitalRead(7);  // Leer el estado del botón
        Serial.print("Button State: ");
        Serial.println(buttonState);

        // Verificar si el estado del botón ha cambiado desde la última iteración del bucle
        if (lastButtonState == HIGH && buttonState == LOW) {  // Se detectó una pulsación
            ledState = !ledState;                               // Alternar estado del LED
        }

        if (ledState == HIGH) {
            potValue = analogRead(A0);  // Leer continuamente el valor del potenciómetro cuando el LED esté encendido
            analogWrite(9, potValue / 4);  // Ajustar brillo continuamente
            Serial.print("Pot Value: ");
            Serial.println(potValue);
        } else {
            analogWrite(9, 0);  // Apagar el LED
        }

        lastButtonState = buttonState;  // Actualizar lastButtonState al estado actual
        delay(200);                     // Opcional: Debouncing simple por software
    }

1. Después de seleccionar la placa y el puerto correctos, haz clic en "Subir" para cargar el código en tu Arduino.

2. Abre el Monitor Serial para ver los datos de salida. Notarás que el estado del botón imprime "1" continuamente cuando no está presionado y "0" cuando se presiona. Al mismo tiempo, también se imprimirá el valor del potenciómetro. A medida que gires el potenciómetro, observarás en el Monitor Serial que cuanto mayor sea el valor, más brillante se vuelve el LED, y viceversa.

.. image:: img/10_dimmer_led_serial_tool.png
    :align: center

.. note::

    Con esto, deberías tener claro lo siguiente:

    - Las señales digitales solo tienen dos estados: 0 y 1.
    - Sin embargo, las señales analógicas tienen un rango, que en este caso va de 0 a 1023.

3. Finalmente, recuerda guardar tu código y organizar tu espacio de trabajo.

**Pregunta**

1. ¿Qué sucedería si configuras el pin digital 7 solo como INPUT? ¿Por qué?

.. code-block::
    :emphasize-lines: 3

    void setup() {
        pinMode(9, OUTPUT);        // Configurar el pin 9 como salida
        pinMode(7, INPUT);  // Configurar el pin 7 como entrada con una resistencia pull-up interna
        Serial.begin(9600);        // Configurar la comunicación serial a 9600 baudios
    }

2. Si el pin 7 se configura solo como ``INPUT``, ¿qué ajustes necesitarían hacerse en el circuito?

**Resumen**

Al final de esta lección, tendrás una lámpara de escritorio ON/OFF completamente funcional, controlada a través de una interfaz de usuario simple. Habrás dominado cómo integrar y manipular varios componentes electrónicos y técnicas de programación con Arduino para crear un dispositivo electrónico práctico e interactivo. Este proyecto no solo refuerza conceptos fundamentales en electrónica y programación, sino que también te proporciona una pieza funcional para agregar a tu colección de proyectos DIY.

