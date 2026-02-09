.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirte?**

    - **Soporte de expertos**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Accede anticipadamente a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones durante festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

24. Luz Corrediza con 74HC595
=======================================

En esta lección, nos sumergiremos en el mundo del chip de registro de desplazamiento 74HC595. Este potente componente nos permite controlar numerosos LEDs con solo unos pocos pines, lo que lo hace perfecto para implementar efectos de luces corredizas. Al final de esta lección, tendrás una comprensión sólida de cómo funciona el 74HC595, cómo usarlo para desplazar datos binarios y cómo aplicarlo en un experimento práctico de control de LEDs.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/24_flowing_light.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

En esta lección, aprenderás:

* Comprender los principios de funcionamiento del chip 74HC595 y las funciones de sus pines.
* Aprender a usar la función ``shiftOut()`` para desplazar datos.
* Construir un circuito de luces corredizas usando el chip 74HC595 y Arduino.
* Controlar 8 LEDs usando datos binarios y el chip 74HC595 para crear un efecto de luz corrediza.

Aprendiendo el Chip 74HC595
---------------------------------
El chip 74HC595 consta de un registro de desplazamiento de 8 bits y un registro de almacenamiento con salidas paralelas de tres estados. Convierte la entrada serial en salida paralela para que puedas ahorrar puertos de E/S de un MCU.

.. image:: img/24_74hc595.png
    :width: 300
    :align: center

**Funciones de los Pines**

.. image:: img/24_74hc595_pin.png
    :width: 500
    :align: center

* **Q0-Q7**: Pines de salida de datos paralelos de 8 bits, capaces de controlar directamente 8 LEDs o 8 pines de una pantalla de 7 segmentos.
* **Q7'**: Pin de salida en serie, conectado al pin DS de otro 74HC595 para conectar varios 74HC595 en serie.
* **MR**: Pin de reinicio, activo en nivel bajo.
* **SHcp**: Entrada de secuencia de tiempo del registro de desplazamiento. En el flanco de subida, los datos en el registro de desplazamiento se mueven sucesivamente un bit; por ejemplo, los datos en Q1 se mueven a Q2, y así sucesivamente. En el flanco de bajada, los datos en el registro de desplazamiento permanecen sin cambios.
* **STcp**: Entrada de secuencia de tiempo del registro de almacenamiento. En el flanco de subida, los datos en el registro de desplazamiento se transfieren al registro de almacenamiento.
* **CE**: Pin de habilitación de salida, activo en nivel bajo.
* **DS**: Pin de entrada de datos en serie.
* **VCC**: Voltaje de alimentación positivo.
* **GND**: Tierra.

**Principio de Funcionamiento**

Cuando MR (pin10) está en nivel alto y OE (pin13) en nivel bajo, los datos se ingresan en el flanco de subida de SHcp y pasan al registro de almacenamiento en el flanco de subida de STcp.

* Registro de Desplazamiento

    * Supongamos que queremos ingresar los datos binarios 1110 1110 en el registro de desplazamiento del 74HC595.
    * Los datos se ingresan desde el bit 0 del registro de desplazamiento.
    * Cada vez que el reloj del registro de desplazamiento tiene un flanco de subida, los bits en el registro de desplazamiento se desplazan un paso. Por ejemplo, el bit 7 acepta el valor anterior en el bit 6, el bit 6 obtiene el valor del bit 5, etc.

.. image:: img/24_74hc595_shift.png
    :width: 600
    :align: center

* Registro de Almacenamiento

    * Cuando el registro de almacenamiento está en el estado de flanco de subida, los datos del registro de desplazamiento se transferirán al registro de almacenamiento.
    * El registro de almacenamiento está directamente conectado a los 8 pines de salida; Q0 ~ Q7 podrán recibir un byte de datos.
    * El llamado registro de almacenamiento significa que los datos pueden existir en este registro y no desaparecerán con una sola salida.
    * Los datos permanecerán válidos e inalterados siempre que el 74HC595 esté alimentado continuamente.
    * Cuando llegan nuevos datos, los datos en el registro de almacenamiento serán sobrescritos y actualizados.

.. image:: img/24_74hc595_storage.png
    :width: 600
    :align: center

Construyendo el Circuito
-----------------------------

**Componentes Necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 8 * LEDs
     - 8 * Resistencias de 220Ω
     - 1 * 74HC595
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_74hc595|  
   * - 1 * Protoboard
     - Cables de salto
     - 1 * Cable USB
     - 
   * - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
     - 

**Construcción Paso a Paso**

Sigue el diagrama de cableado o los pasos a continuación para construir tu circuito.

.. image:: img/24_flow_light.png
    :width: 600
    :align: center

1. Inserta 8 LEDs en la protoboard, utilizando cualquier configuración de color que prefieras. Asegúrate de que todos los cátodos (piernas cortas) de los LEDs estén conectados a la línea de tierra en la protoboard, mientras que los ánodos estén conectados a filas separadas.

.. image:: img/24_flow_light_led.png
    :width: 500
    :align: center

2. Conecta una resistencia de 220Ω a cada ánodo de los LEDs.

.. image:: img/24_flow_light_resistor.png
    :width: 500
    :align: center

3. Ubica el chip 74HC595 e insértalo en la protoboard. Asegúrate de que el chip atraviese la separación central.

.. note::

    Presta mucha atención a la orientación del 74HC595 para evitar daños. Puedes identificar la orientación correcta utilizando las siguientes pistas:

    * La etiqueta en el chip está en posición vertical.
    * La muesca en el chip está hacia la izquierda.

.. image:: img/24_flow_light_74hc595.png
    :width: 500
    :align: center

4. Conecta los pines VCC y MR del 74HC595 a la línea positiva en la protoboard.

.. image:: img/24_flow_light_vcc.png
    :width: 500
    :align: center

5. Conecta los pines CE y GND del 74HC595 a la línea negativa en la protoboard.

.. image:: img/24_flow_light_gnd.png
    :width: 500
    :align: center

6. Conecta los pines Q0-Q7 del 74HC595 a las filas en la protoboard que contienen las resistencias de 220Ω.

.. image:: img/24_flow_light_q0_q7.png
    :width: 500
    :align: center

7. Conecta el pin DS del 74HC595 al pin 11 del Arduino Uno R3.

.. image:: img/24_flow_light_pin11.png
    :width: 600
    :align: center

8. Conecta el pin ST_CP del 74HC595 al pin 12 del Arduino Uno R3.

.. image:: img/24_flow_light_pin12.png
    :width: 600
    :align: center

9. Conecta el pin Sh_CP del 74HC595 al pin 8 del Arduino Uno R3.

.. image:: img/24_flow_light_pin8.png
    :width: 600
    :align: center

10. Finalmente, conecta los pines GND y 5V del Arduino Uno R3 a las líneas negativa y positiva en la protoboard, respectivamente.

.. image:: img/24_flow_light.png
    :width: 600
    :align: center

11. La siguiente tabla muestra las conexiones entre los pines del 74HC595 y el Arduino Uno R3.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - Arduino UNO R3
    *   - VCC
        - 5V
    *   - Q0~Q7
        - LEDs 
    *   - DS
        - 11
    *   - CE
        - GND
    *   - ST_CP
        - 12
    *   - SH_CP
        - 8
    *   - MR
        - 5V
    *   - GND
        - GND

Creación del Código - Encender LEDs
--------------------------------------------

El Arduino Uno R3 envía grupos de datos binarios al chip 74HC595.
Los datos binarios forman el núcleo de las computadoras y muchos dispositivos electrónicos, utilizando simples 0s y 1s para procesar datos e instrucciones complejas.
En la informática y electrónica digital, los datos binarios son vitales, ya que constituyen la base para el procesamiento y almacenamiento de información en las computadoras electrónicas.
Aquí, 0 y 1 pueden verse como estados de un interruptor, donde 0 representa apagado (cerrado) y 1 representa encendido (abierto).

Para los números binarios, necesitas entender dos conceptos básicos:

* Bit: Un bit es la unidad básica en el sistema binario, y cada bit puede ser 0 o 1.
* Byte: Un byte está compuesto por 8 bits. Es una unidad común de procesamiento de datos en las computadoras. (¡Y mira, el chip 74HC595 acepta exactamente 1 byte de datos a la vez!)

Los números binarios se ordenan desde el bit menos significativo hasta el más significativo, siendo el bit más a la derecha el menos significativo y el bit más a la izquierda el más significativo.

.. image:: img/24_binary_bit.png
    :width: 500
    :align: center

¡Ahora veamos cómo el 74HC595 recibe datos binarios y los envía a los LEDs!

1. Abre el Arduino IDE y comienza un nuevo proyecto seleccionando "Nuevo Sketch" en el menú "Archivo".
2. Guarda tu sketch como ``Lesson24_Lighting_up_LEDs`` usando ``Ctrl + S`` o haciendo clic en “Guardar”.

3. Controlar el 74HC595 solo requiere tres pines para proporcionar señales de pulso, así que configúralos como OUTPUT.

.. code-block:: Arduino

    const int STcp = 12;  // Pin conectado a ST_CP del 74HC595
    const int SHcp = 8;   // Pin conectado a SH_CP del 74HC595
    const int DS = 11;    // Pin conectado a DS del 74HC595

    void setup() {
        // Configurar pines como salida
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

4. Tu computadora envía datos binarios al pin ``DS`` (Entrada de Datos) del 74HC595, luego usa la señal de reloj del pin ``SH_CP`` (Entrada del Reloj del Registro de Desplazamiento) para desplazar cada bit de datos hacia adelante. Este proceso de transmisión de datos puede implementarse usando la función ``shiftOut()``.

    * ``shiftOut(dataPin, clockPin, bitOrder, value)``: Desplaza un byte de datos un bit a la vez. Comienza desde el bit más significativo (es decir, el más a la izquierda) o el menos significativo (a la derecha). Cada bit se escribe en un pin de datos, después de lo cual se pulsa un pin de reloj (se lleva a alto, luego a bajo) para indicar que el bit está disponible.

    **Parámetros**

        * ``dataPin``: el pin donde se escribe cada bit. Tipos de datos permitidos: int.
        * ``clockPin``: el pin que se alterna una vez que el dataPin ha sido establecido al valor correcto. Tipos de datos permitidos: int.
        * ``bitOrder``: el orden en el que se desplazan los bits; ya sea ``MSBFIRST`` o ``LSBFIRST`` (Bit Más Significativo Primero o Bit Menos Significativo Primero).
        * ``value``: los datos a desplazar. Tipos de datos permitidos: byte.

    **Retorno**
        Ninguno

5. Aquí, intentamos enviar un byte (8 bits) de datos al registro de desplazamiento del 74HC595 usando la función ``shiftOut()``.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop()
    {
        shiftOut(DS, SHcp, MSBFIRST, B11101110);  // Desplazar los datos, comenzando por el MSB
    }

* Esto envía los datos ``B11101110`` (binario, B significa binario) al registro de desplazamiento del 74HC595, comenzando desde el bit más significativo.
* Cada vez que el pin ``SH_CP`` recibe una señal de borde ascendente (el momento en que el voltaje va de bajo a alto), los bits en el registro de desplazamiento se desplazan un paso.
* Por ejemplo, el bit 7 acepta el valor anterior en el bit 6, el bit 6 recibe el valor del bit 5, y así sucesivamente.

.. image:: img/24_74hc595_shift.png
    :width: 500
    :align: center

6. Después de que todos los bits de datos se hayan ingresado a través del pin DS y se hayan desplazado a sus posiciones correctas usando múltiples señales de reloj, el siguiente paso es copiar estos datos del registro de desplazamiento a un registro de almacenamiento.

.. code-block:: Arduino
    :emphasize-lines: 2,7

    void loop() {
        digitalWrite(STcp, LOW);  // Establecer ST_CP (Pin de Latch) en bajo mientras se transmite
        
        // Enviar datos al registro de desplazamiento usando MSBFIRST (Bit Más Significativo Primero)
        shiftOut(DS, SHcp, MSBFIRST, B11101110);
        
        digitalWrite(STcp, HIGH);  // Establecer ST_CP en alto para guardar los datos en los pines de salida
        
        delay(1000);  // Esperar un segundo antes de repetir
    }

* Cuando el pin ``ST_CP`` recibe una señal de borde ascendente, los datos en el registro de desplazamiento se copian al registro de almacenamiento.
* Una vez que los datos se copian al registro de almacenamiento, los LEDs conectados a los pines de salida correspondientes (Q0 ~ Q7) se encenderán o se mantendrán apagados según si los datos son 1 o 0.

.. image:: img/24_74hc595_storage_1data.png
    :width: 300
    :align: center

7. Aquí está tu código completo. Ahora puedes cargar este código en el Arduino Uno R3. Después de eso, verás que los LEDs conectados a Q0 y Q4 estarán apagados mientras los demás LEDs están encendidos.

.. code-block:: Arduino

    const int STcp = 12;  // Pin conectado a ST_CP del 74HC595
    const int SHcp = 8;   // Pin conectado a SH_CP del 74HC595
    const int DS = 11;    // Pin conectado a DS del 74HC595

    void setup() {
        // Configurar pines como salida
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        digitalWrite(STcp, LOW);  // Establecer ST_CP en bajo mientras se transmite
        shiftOut(DS, SHcp, MSBFIRST, B11101110);  // Desplazar los datos, comenzando por el MSB
        digitalWrite(STcp, HIGH);  // Establecer ST_CP en alto para guardar los datos
        delay(1000);  // Esperar un segundo
    }

**Pregunta**

¿Qué sucede si cambiamos ``MSBFIRST`` a ``LSBFIRST`` en ``shiftOut(DS, SHcp, MSBFIRST, B11101110);``? ¿Por qué?


Creación del Código - Luces Corredizas
---------------------------------------------

¿Cómo podríamos implementar un efecto de luces corredizas, donde los LEDs se encienden uno por uno?

1. Abre el sketch que guardaste anteriormente, ``Lesson24_Lighting_up_LEDs``.

2. Haz clic en "Guardar Como..." en el menú "Archivo" y renómbralo como ``Lesson24_Flowing_Light``. Haz clic en "Guardar".

3. Aquí queremos configurar un efecto de luces corredizas, donde los LEDs se enciendan uno por uno. Escribiremos los estados de encendido/apagado de esta secuencia de luces en un arreglo.

.. code-block:: Arduino
    :emphasize-lines: 4

    const int STcp = 12;  // Pin conectado a ST_CP del 74HC595
    const int SHcp = 8;   // Pin conectado a SH_CP del 74HC595
    const int DS = 11;    // Pin conectado a DS del 74HC595
    int datArray[] = {B00000000, B00000001, B00000011, B00000111, B00001111, B00011111, B00111111, B01111111, B11111111};

4. Luego, usa un bucle ``for`` para llamar secuencialmente a este arreglo.

.. code-block:: Arduino
    :emphasize-lines: 3,5

    void loop()
    {
        for (int num = 0; num <= 8; num++) {
            digitalWrite(STcp, LOW);                      // Mantén ST_CP en bajo mientras se transmite
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Desplazar los datos, MSB primero
            digitalWrite(STcp, HIGH);                     // Elevar ST_CP para guardar los datos
            delay(1000);                                  // Esperar un segundo
        }
    }

5. A continuación se muestra tu código completo. Ahora puedes cargar este código en el Arduino Uno R3, y verás que los LEDs se encienden uno por uno, como una luz corrediza.

.. code-block:: Arduino

    const int STcp = 12;  // Pin conectado a ST_CP del 74HC595
    const int SHcp = 8;   // Pin conectado a SH_CP del 74HC595
    const int DS = 11;    // Pin conectado a DS del 74HC595
    int datArray[] = {B00000000, B00000001, B00000011, B00000111, B00001111, B00011111, B00111111, B01111111, B11111111};

    void setup ()
    {
        // Configurar pines como salida
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop()
    {
        for (int num = 0; num <= 8; num++) {
            digitalWrite(STcp, LOW);                      // Mantén ST_CP en bajo mientras se transmite
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Desplazar los datos, MSB primero
            digitalWrite(STcp, HIGH);                     // Elevar ST_CP para guardar los datos
            delay(1000);                                  // Esperar un segundo
        }
    }

6. Finalmente, recuerda guardar tu código y ordenar tu área de trabajo.

**Pregunta**

Si quisiéramos tener tres LEDs encendidos a la vez y que parezca que "fluyen", ¿cómo deberían modificarse los elementos del arreglo ``datArray[]``?

**Resumen**

En esta lección, exploramos la estructura y funcionalidad del chip 74HC595, aprendiendo cómo desplazar datos binarios a través de su registro de desplazamiento y construir un experimento de luces corredizas. Usando la función ``shiftOut()`` para controlar la transmisión de datos binarios, logramos gestionar con éxito el encendido secuencial de 8 LEDs para lograr un efecto de luces corredizas. Con este nuevo conocimiento, ahora deberías ser capaz de usar el chip 74HC595 de manera efectiva para agregar deslumbrantes características de iluminación a tus propios proyectos.

