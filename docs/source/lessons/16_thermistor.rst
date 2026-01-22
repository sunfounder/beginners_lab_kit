.. note::

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 con otros apasionados.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos exclusivos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones especiales de temporada.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy!

16. Alarma de Temperatura
=============================

En esta lección, exploraremos el papel crítico de la gestión de la temperatura en la seguridad alimentaria. No todos los alimentos necesitan refrigeración o congelación; incluso productos estables como papas fritas, pan y ciertas frutas requieren un almacenamiento adecuado a temperatura ambiente para mantener su calidad y seguridad. Al construir un sistema de monitoreo de temperatura, aprenderemos cómo mantener los alimentos dentro de rangos de temperatura seguros, activando una alarma cuando las temperaturas se desvíen de estos límites. Este proyecto práctico no solo ayuda a proteger los alimentos, sino que también sirve como una excelente introducción a la monitorización ambiental con aplicaciones del mundo real.

.. .. imagen:: img/16_temperature.jpg
..     :width: 400
..     :align: center

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/16_temp_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Al final de esta lección, serás capaz de:

* Comprender la importancia del control de temperatura en la seguridad alimentaria.
* Construir un circuito con un termistor para monitorear cambios de temperatura.
* Escribir un programa en Arduino para leer datos de temperatura desde un termistor.
* Usar lógica en la programación para desencadenar acciones (como encender un LED o activar una alarma) basadas en los datos de temperatura.
* Aplicar conceptos de resistencia eléctrica y conversión de temperatura en escenarios prácticos.

Construyendo el Circuito
-----------------------------

**Componentes Necesarios**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Resistencias de 220Ω
     - 1 * Resistencia de 10KΩ
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Termistor
     - 1 * Protoboard
     - Cables Jumper
     - 1 * Cable USB
   * - |list_thermistor| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
   * - 1 * Multímetro
     - 
     - 
     - 
   * - |list_meter| 
     - 
     - 
     - 

**Instrucciones Paso a Paso**

Este circuito se construye sobre el de la lección 12, añadiendo un termistor.

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

1. Basado en el circuito de la lección 12, quita el cable jumper que conecta el pin GND del Arduino Uno R3 al pin GND del LED RGB y luego insértalo en el terminal negativo de la protoboard. Luego, conecta un cable jumper desde el terminal negativo hasta el pin GND del LED RGB.

.. image:: img/16_temperature_alarm_gnd.png
    :width: 500
    :align: center

2. Inserta el termistor en los agujeros 6E y 8E. Los pines no tienen polaridad, por lo que se pueden insertar en cualquier dirección.

.. image:: img/16_temperature_alarm_thermistor.png
    :width: 500
    :align: center

Un termistor es un tipo especial de resistencia cuya resistencia varía con la temperatura. Este dispositivo es muy útil, ya que nos ayuda a detectar y medir la temperatura, permitiendo su control en varios proyectos y dispositivos electrónicos.

Este es el símbolo electrónico del termistor.

.. image:: img/16_thermistor_symbol.png
    :width: 300
    :align: center

Existen dos tipos fundamentales de termistores:

* **Termistores NTC**: La resistencia disminuye al aumentar la temperatura. Se utilizan comúnmente como sensores de temperatura o limitadores de corriente de irrupción en circuitos.
* **Termistores PTC**: La resistencia aumenta al aumentar la temperatura. Se usan frecuentemente como fusibles rearmables en circuitos para proteger contra sobrecorriente.

En este kit usamos un **NTC**.

Ahora usa un multímetro para medir la resistencia de este termistor y verifica si realmente disminuye cuando aumenta la temperatura.

3. Como la resistencia nominal del termistor es de 10K, ajusta el multímetro para medir resistencias en el rango de 20 kilo-ohmios (20K).

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

4. Ahora, toca los dos pines del termistor con las puntas de prueba roja y negra del multímetro.

.. image:: img/16_temperature_alarm_test.png
    :width: 500
    :align: center

5. Lee el valor de resistencia a la temperatura actual y regístralo en la siguiente tabla.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Ambiente
     - Resistencia (kilohmios)
   * - Temperatura actual
     - *9.37*
   * - Temperatura más alta
     - 
   * - Temperatura más baja
     - 

6. Ahora puedes pedirle a un amigo que te ayude a sostener el termistor, o usar algo más para aumentar la temperatura alrededor del termistor (sin agua, sin fuego, ¡seguridad primero!). Registra el valor de resistencia del termistor en ese momento en la tabla.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Ambiente
     - Resistencia (kilohmios)
   * - Temperatura actual
     - *9.37*
   * - Temperatura más alta
     - *6.10*
   * - Temperatura más baja
     - 

7. Puedes colocar el termistor al aire libre o abanicarlo para reducir la temperatura a su alrededor. Registra la resistencia medida en ese momento en la tabla.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Ambiente
     - Resistencia (kilohmios)
   * - Temperatura actual
     - *9.37*
   * - Temperatura más alta
     - *6.10*
   * - Temperatura más baja
     - *12.49*

A través de estas mediciones, podemos ver que cuanto mayor es la temperatura ambiente, menor es la resistencia.

8. Ahora puedes continuar construyendo el circuito. Conecta un extremo del termistor a una resistencia de 10K, y el otro extremo de la resistencia de 10K al terminal negativo de la protoboard.

.. image:: img/16_temperature_alarm_resistor.png
    :width: 500
    :align: center

9. Conecta el otro extremo de la protoboard al pin de 5V del Arduino Uno R3.

.. image:: img/16_temperature_alarm_5v.png
    :width: 500
    :align: center

10. Finalmente, conecta el pin común del fotorresistor y la resistencia de 10K al pin A0 del Arduino Uno R3.

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

Comprendiendo el Cálculo de la Temperatura
----------------------------------------------
**Acerca de la Fórmula de la Temperatura**

La resistencia de un termistor NTC varía con la temperatura. Esta relación se describe comúnmente mediante la Ecuación de Steinhart-Hart, como se muestra a continuación:

.. image:: img/16_format_steinhart.png
    :width: 400
    :align: center

Aquí, los parámetros a, b y c son los llamados parámetros de Steinhart–Hart, que deben especificarse para cada dispositivo. T es la temperatura absoluta y R es la resistencia.

Además de la Ecuación de Steinhart-Hart, muchas aplicaciones prácticas también utilizan una fórmula simplificada basada en el modelo del parámetro beta para calcular rápidamente la temperatura. Este modelo supone que la relación entre la resistencia y la temperatura puede aproximarse mediante una relación exponencial más simple, lo que simplifica el proceso de cálculo y lo hace adecuado para monitoreo rápido de temperatura en aplicaciones de ingeniería.

.. image:: img/16_format_3.png
    :width: 400
    :align: center

* **T** es la temperatura del termistor en Kelvin.
* **T0** es una temperatura de referencia, generalmente 25°C (273.15 + 25 en Kelvin).
* **B** es el parámetro beta del material, el coeficiente beta del termistor NTC utilizado en este kit es 3950.
* **R** es la resistencia que medimos.
* **R0** es la resistencia a la temperatura de referencia T0, la resistencia del termistor NTC en este kit a 25°C es de 10 kilohmios.

Después de convertir las fórmulas anteriores, la temperatura en Kelvin se calcula como: ``T=1/(ln(R/R0)/B+1/T0)``, y restamos 273.15 para convertirla a Celsius.

**¿Cómo medir la resistencia?**

Conectamos el termistor y una resistencia de 10K en serie en nuestro circuito.

.. image:: img/16_thermistor_sch.png
    :width: 200
    :align: center

El voltaje en el pin A0, que medimos, dividido por la resistencia en serie (la resistencia de 10K), nos indica la corriente que fluye a través del circuito. Esta corriente también se puede obtener dividiendo el voltaje total por la resistencia total del circuito (resistencia en serie + termistor):

.. image:: img/16_format_1.png
    :width: 400
    :align: center

* **Vsupply**: El voltaje suministrado al circuito.
* **Rseries**: El valor de la resistencia en serie.
* **Vmeasured**: El voltaje a través de la resistencia de 10K, también el voltaje en el pin A0.

A partir de esto, podemos reorganizar la fórmula para encontrar la resistencia del termistor:

.. image:: img/16_format_2.png
    :width: 400
    :align: center

En nuestro código, usamos la función ``analogRead()`` para leer el voltaje en el pin A0. La relación entre el voltaje **Vmeasured** y el valor analógico leído es:

.. code-block::

    (Analog value at A0) / 1023.0 = Vmeasured / Vsupply

Usando la fórmula anterior, calculamos la resistencia del termistor:

.. code-block::

    R_thermistor =R_series x (1023.0 / (Analog value at A0) - 1)

.. note::

    Si las fórmulas parecen complicadas, ¡solo recuerda las finales y estarás listo!

    La resistencia del termistor se puede obtener a través de la siguiente fórmula:

    .. code-block::

        R_thermistor = R_series x (1023.0 / (Valor analógico en A0) - 1)

    Luego, calcula la temperatura en Kelvin usando la siguiente fórmula:
    .. code-block::

        T=1/(ln(R/R0)/B+1/T0)

    * **T0**: 273.15 + 25.
    * **B**: 3950.
    * **R** es la resistencia que medimos.
    * **R0**: 10 kilohmios.

    Finalmente, convierte a Celsius usando la siguiente fórmula:

    .. code-block::

        Tc = T - 273.15

    
Creación de Código
----------------------

**Obteniendo la Temperatura**

1. Abre el IDE de Arduino y comienza un nuevo proyecto seleccionando "New Sketch" desde el menú "File".
2. Guarda tu sketch como ``Lesson16_Temperature_Alarm`` usando ``Ctrl + S`` o haciendo clic en "Save".

3. En lecciones anteriores, referenciamos directamente los pines del LED RGB en nuestro código; aquí, los definimos como constantes.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // Configuración de pines
    const int tempSensorPin = A0;  // Entrada analógica del termistor NTC
    const int redPin = 11;         // Pin digital del LED rojo
    const int greenPin = 10;       // Pin digital del LED verde
    const int bluePin = 9;         // Pin digital del LED azul

    void setup() {
        // Configuración inicial del código
    }

Usar constantes en lugar de variables, que permanecen sin cambios a lo largo del programa, brinda claridad y facilita el mantenimiento. Esto permite utilizar nombres significativos en lugar de números, y los cambios solo requieren ajustes en la declaración, no en todo el código. Las constantes siguen las mismas reglas de nomenclatura que las variables, evitando palabras reservadas o comandos del IDE de Arduino.

4. Antes de utilizar el termistor, también necesitamos definir más constantes para almacenar parámetros relacionados con el circuito.

.. note::

    Verás que hay constantes de tipo ``int`` y de tipo ``float``. Entonces, ¿cuál es la diferencia entre estos dos tipos de constantes?

  * ``const int``: Una constante ``int`` (abreviatura de entero) almacena números enteros. Este tipo no soporta fracciones ni puntos decimales. Generalmente ocupa 16 o 32 bits de memoria, dependiendo del sistema.
  * ``const float``: Una constante ``float`` (abreviatura de punto flotante) almacena números que pueden tener partes fraccionarias. Se utiliza cuando se necesita más precisión, como en mediciones o cálculos que requieren valores decimales. Un ``float`` ocupa típicamente 32 bits de memoria y puede representar un rango más amplio de números que un ``int``.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // Configuración de pines
    const int tempSensorPin = A0;  // Entrada analógica del termistor NTC
    const int redPin = 10;         // Pin digital del LED rojo
    const int greenPin = 11;       // Pin digital del LED verde
    const int bluePin = 12;        // Pin digital del LED azul

    // Constantes para el cálculo de temperatura
    const float beta = 3950.0;               // Valor Beta del termistor NTC
    const float seriesResistor = 10000;      // Valor de la resistencia en serie (ohmios)
    const float roomTempResistance = 10000;  // Resistencia del NTC a 25°C
    const float roomTemp = 25 + 273.15;      // Temperatura ambiente en Kelvin

5. En ``void setup()``, configura los pines del LED RGB como salidas y establece la velocidad de comunicación serial a 9600 baudios.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    void setup() {
        // Inicializar los pines del LED como salidas
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);
        
        // Iniciar la comunicación serial a 9600 baudios
        Serial.begin(9600);
    }

6. Primero, necesitas leer el valor analógico del pin A0 en ``void loop()``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leer el valor del termistor
    }

7. A continuación, calcula la resistencia del termistor utilizando la fórmula derivada previamente para convertir los valores analógicos a voltaje.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leer el valor del termistor
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcular la resistencia del termistor
    }

8. Luego, calcula la temperatura en Kelvin utilizando la fórmula mostrada a continuación:

.. code-block:: Arduino
    :emphasize-lines: 6

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leer el valor del termistor
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcular la resistencia del termistor

        // Calcular la temperatura en Kelvin usando la ecuación del parámetro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    }

9. Resta 273.15 de la temperatura en Kelvin para convertirla a Celsius, y luego imprime el resultado en el monitor serial utilizando la función ``Serial.println()``.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leer el valor del termistor
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcular la resistencia del termistor

        // Calcular la temperatura en Kelvin usando la ecuación del parámetro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // Convertir a Celsius
        Serial.println(tempC);         // Mostrar la temperatura en Celsius en el monitor serial
    }

10. En este punto, puedes subir el código a tu Arduino Uno R3 y obtener los valores de temperatura actuales en grados Celsius.

.. code-block::

    26.28
    26.19
    26.19
    26.28
    26.28
    
**Cambiar el Color del LED RGB**

Ahora, cambiemos el color del LED RGB en función de la temperatura medida por el termistor.

Por ejemplo, establecemos tres rangos de temperatura:

* Por debajo de 10 grados, el LED RGB muestra color verde, lo que indica que la temperatura es cómoda.
* Entre 10 y 20 grados, el LED RGB muestra color amarillo, señalando precaución con la temperatura actual.
* Por encima de 21 grados, el LED RGB muestra color rojo, indicando que la temperatura es demasiado alta y se necesitan medidas.

11. Para controlar el LED RGB, utilizaremos la función ``setColor()`` creada en lecciones anteriores.

.. code-block:: Arduino

    // Función para configurar el color del LED RGB
    void setColor(int red, int green, int blue) {
        // Escribir los valores PWM para rojo, verde y azul en el LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

12. Ahora, utilizamos una declaración ``if else if`` para controlar el color del LED RGB en función de las diferentes temperaturas.

.. code-block:: Arduino
    :emphasize-lines: 12-18

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leer el valor del termistor
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcular la resistencia del termistor

        // Calcular la temperatura en Kelvin usando la ecuación del parámetro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // Convertir a Celsius
        Serial.println(tempC);         // Mostrar la temperatura en Celsius en el Monitor Serial

        // Ajustar el color del LED según la temperatura
        if (tempC < 10) {
            setColor(0, 0, 255);  // Frío: azul
        } else if (tempC >= 10 && tempC <= 21) {
            setColor(0, 255, 0);  // Cómodo: verde
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // Caliente: rojo
        }
        delay(1000);  // Retraso de 1 segundo antes de la siguiente lectura
    }

13. Tu código completo está listo. Ahora puedes subir el código a tu Arduino Uno R3 para ver los efectos.


.. code-block:: Arduino

    // Configuración de pines
    const int tempSensorPin = A0;  // Entrada analógica del termistor NTC
    const int redPin = 10;         // Pin digital del LED rojo
    const int greenPin = 11;       // Pin digital del LED verde
    const int bluePin = 12;        // Pin digital del LED azul

    // Constantes para el cálculo de la temperatura
    const float beta = 3950.0;               // Valor Beta del termistor NTC
    const float seriesResistor = 10000;      // Valor de la resistencia en serie (ohmios)
    const float roomTempResistance = 10000;  // Resistencia del NTC a 25°C
    const float roomTemp = 25 + 273.15;      // Temperatura ambiente en Kelvin

    void setup() {
        // Inicializar los pines del LED como salidas
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);

        // Iniciar la comunicación serial a 9600 baudios
        Serial.begin(9600);
    }

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Leer el valor del termistor
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Calcular la resistencia del termistor

        // Calcular la temperatura en Kelvin usando la ecuación del parámetro Beta
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);

        float tempC = tempK - 273.15;  // Convertir a Celsius
        Serial.println(tempC);         // Mostrar la temperatura en Celsius en el Monitor Serial

        // Ajustar el color del LED según la temperatura
        if (tempC < 10) {
            setColor(0, 0, 255);  // Frío: azul
        } else if (tempC >= 10 && tempC <= 21) {
            setColor(0, 255, 0);  // Cómodo: verde
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // Caliente: rojo
        }
        delay(1000);  // Retraso de 1 segundo antes de la siguiente lectura
    }

    // Función para configurar el color del LED RGB
    void setColor(int red, int green, int blue) {
        // Escribir el valor PWM para rojo, verde y azul en el LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }


14. Finalmente, recuerda guardar tu código y ordenar tu espacio de trabajo.

**Pregunta**

1. En el código, se calculan las temperaturas en Kelvin y Celsius. Si también quieres conocer la temperatura en Fahrenheit, ¿qué deberías hacer?

2. ¿Puedes pensar en otras situaciones o lugares donde un sistema de monitoreo de temperatura como el que construimos hoy podría ser útil?

**Resumen**

En la lección de hoy, construimos un sistema de alarma de temperatura que utiliza un termistor para monitorear la temperatura de un área de almacenamiento de alimentos no perecederos. Aprendimos a leer y convertir los valores de resistencia del termistor en lecturas de temperatura en Celsius. A través de nuestra programación, también configuramos condiciones para cambiar el color de un LED RGB en función de la temperatura, proporcionando una alerta visual para temperaturas que son demasiado bajas, ideales o demasiado altas.
