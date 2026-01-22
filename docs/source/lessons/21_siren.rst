.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder para Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Accesos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy mismo!

21. Sonido de Sirena
=========================

En este proyecto de Arduino, exploraremos cómo crear un sistema de sirena mediante programación e integración de hardware electrónico.

Los sonidos de sirena utilizan un patrón de frecuencia y tono específico, caracterizado por rápidos aumentos y descensos en el tono, que no solo son fácilmente reconocibles sino también distintos de otros sonidos cotidianos. Estos cambios de tono pueden generar una sensación de urgencia, ya que a menudo se asocian con señales de advertencia o situaciones peligrosas en la naturaleza.

Ajustando la frecuencia de un zumbador pasivo, podemos simular los tonos característicos ascendentes y descendentes de una sirena.

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/21_siren_sound.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

En esta lección, aprenderás:

* Cómo funcionan los zumbadores pasivos
* Cómo controlar un zumbador pasivo usando la función ``tone()``
* Cómo utilizar el bucle ``for`` en programación
* Cómo implementar un sonido de sirena

Entendiendo las propiedades del sonido
------------------------------------------

El sonido es un fenómeno ondulatorio que se propaga a través de medios como el aire, agua o sólidos como energía vibratoria. Entender las propiedades físicas del sonido nos puede ayudar a comprender mejor y controlar cómo se comporta el sonido en diferentes entornos.
A continuación, algunas propiedades clave del sonido:

.. image:: img/7_siren.png
    :width: 500
    :align: center


**Frecuencia**



La frecuencia se refiere al número de ciclos de vibración por unidad de tiempo, 
típicamente expresada en Hertz (Hz). La frecuencia determina el tono del sonido: 
frecuencias más altas suenan más agudas, frecuencias más bajas suenan más graves. 
El rango audible para los humanos es de aproximadamente 20 Hz a 20,000 Hz.

**Amplitud**

La amplitud es la intensidad de la vibración de una onda sonora, y determina el 
volumen del sonido. Mayor amplitud significa un sonido más fuerte; menor amplitud, 
un sonido más suave. En física, la amplitud está directamente relacionada con la 
energía de la onda sonora, mientras que en la vida cotidiana solemos utilizar 
decibelios (dB) para describir el volumen.

**Timbre**

El timbre describe la textura o "color" del sonido, lo que nos permite distinguir sonidos 
de diferentes fuentes aunque tengan el mismo tono y volumen. Por ejemplo, aunque un violín 
y un piano toquen la misma nota, podemos diferenciarlos por su timbre.

En este proyecto, exploraremos solo la influencia de la frecuencia en el sonido.

Montaje del circuito
-----------------------

**Componentes necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Protoboard
     - 1 * Zumbador pasivo
     - Cables de conexión
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_passive_buzzer| 
     - |list_wire| 
   * - 1 * Cable USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 



**Paso a paso**

En lecciones anteriores, utilizamos un zumbador activo. En esta lección, usaremos un zumbador pasivo. El circuito es el mismo, pero la forma de programarlo para que funcione es diferente.

1. Localiza un zumbador pasivo, que tiene una placa de circuito expuesta en su parte trasera.

.. image:: img/7_beep_2.png

2. Aunque hay un signo de "+" en el zumbador pasivo, no es un dispositivo polarizado. Insértalo en cualquier dirección en los agujeros 15F y 18F de la protoboard.

.. image:: img/16_morse_code_buzzer.png
    :width: 500
    :align: center

3. Conecta un pin del zumbador pasivo al pin GND del Arduino Uno R3.

.. image:: img/16_morse_code_gnd.png
    :width: 500
    :align: center

4. Conecta el otro pin del zumbador pasivo al pin 5V del Arduino Uno R3. El zumbador no emitirá sonido, lo que lo diferencia de un zumbador activo, que sí sonaría al conectarlo de esta manera.

.. image:: img/16_morse_code_5v.png
    :width: 500
    :align: center

5. Ahora, retira el cable insertado en el pin 5V y conéctalo al pin 9 del Arduino Uno R3, para que el zumbador pueda ser controlado por código.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Creación de código - Hacer sonar el zumbador pasivo
-------------------------------------------------------

Como aprendimos al conectar el circuito, simplemente proporcionar potencia alta y baja a un zumbador pasivo no lo hará sonar. En la programación de Arduino, la función ``tone()`` se utiliza para controlar un zumbador pasivo u otros dispositivos de salida de audio para generar un sonido a una frecuencia específica.

    * ``tone()``: Genera una onda cuadrada de la frecuencia especificada (y ciclo de trabajo del 50%) en un pin. Se puede especificar una duración; de lo contrario, la onda continuará hasta una llamada a ``noTone()``.

    **Sintaxis**

        * ``tone(pin, frequency)``
        * ``tone(pin, frequency, duration)``

    **Parámetros**

        * ``pin``: el pin de Arduino en el que se genera el tono.
        * ``frequency``: la frecuencia del tono en hertzios. Tipos de datos permitidos: unsigned int.
        * ``duration``: la duración del tono en milisegundos (opcional). Tipos de datos permitidos: unsigned long.

    **Devuelve**
        Nada


1. Abre el IDE de Arduino y comienza un nuevo proyecto seleccionando “Nuevo Sketch” en el menú “Archivo”.
2. Guarda tu sketch como ``Lesson21_Tone`` usando ``Ctrl + S`` o haciendo clic en “Guardar”.

3. Primero, define el pin del zumbador.

.. code-block:: Arduino

    const int buzzerPin = 9;  // Asigna el pin 9 a la constante para el zumbador

    void setup() {
        // Pon tu código de configuración aquí, para que se ejecute una vez:
    }

4. Para comprender completamente el uso de la función ``tone()``, la escribimos en el ``void setup()`` para que el zumbador emita un sonido a una frecuencia específica durante un tiempo determinado.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;  // Asigna el pin 9 a la constante para el zumbador

    void setup() {
        // Pon tu código de configuración aquí, para que se ejecute una vez:
        tone(buzzerPin, 1000, 100);  // Enciende el zumbador a 1000 Hz con una duración de 100 milisegundos
    }

    void loop() {
        // Pon tu código principal aquí, para que se ejecute repetidamente:
    }

5. Ahora puedes cargar el código en el Arduino Uno R3, después de lo cual escucharás un breve "bip" del zumbador pasivo, y luego quedará en silencio.

**Preguntas**

1. Si cambias los pines del código y del circuito a los pines 7 u 8, que no son pines PWM, ¿el zumbador seguirá emitiendo sonido? Puedes probarlo y luego escribir tu respuesta en el cuaderno.

2. Para explorar cómo ``frequency`` y ``duration`` en la función ``tone(pin, frequency, duration)`` afectan el sonido del zumbador, por favor modifica el código en dos condiciones y anota los fenómenos observados en tu cuaderno:

* Manteniendo ``frequency`` en 1000, incrementa gradualmente ``duration`` de 100, 500 a 1000. ¿Cómo cambia el sonido del zumbador y por qué?

* Manteniendo ``duration`` en 100, incrementa gradualmente ``frequency`` de 1000, 2000 a 5000. ¿Cómo cambia el sonido del zumbador y por qué?

Creación de código - Emitir un sonido de sirena
---------------------------------------------------

Anteriormente, aprendimos cómo hacer que un zumbador emita sonido y comprendimos cómo la frecuencia y la duración afectan el sonido. Ahora, si queremos que el zumbador emita un sonido de sirena que suba de tono bajo a alto, ¿cómo procederíamos?

A partir de nuestras exploraciones anteriores, sabemos que usando la función ``tone(pin, frequency)`` podemos hacer que un zumbador pasivo emita sonido. Al aumentar gradualmente la ``frequency``, el tono del sonido del zumbador pasivo será más agudo. Vamos a implementarlo ahora con código.

1. Abre el sketch que guardaste anteriormente, ``Lesson21_Tone``.

2. Haz clic en "Guardar como..." en el menú "Archivo", y renómbralo a ``Lesson21_Siren_Sound``. Haz clic en "Guardar".

3. Escribe la función ``tone()`` en el ``void loop()`` y configura tres frecuencias diferentes. Para escuchar claramente la diferencia entre cada sonido, usa la función ``delay()`` para separarlos.

.. code-block:: Arduino

    const int buzzerPin = 9;  // Asigna el pin 9 a la constante para el zumbador

    void setup() {
        // Pon tu código de configuración aquí, para que se ejecute una vez:
    }

    void loop() {
        // Pon tu código principal aquí, para que se ejecute repetidamente:
        tone(buzzerPin, 100);  // Activa el zumbador a 100 Hz
        delay(500);
        tone(buzzerPin, 300);  // Activa el zumbador a 300 Hz
        delay(500);
        tone(buzzerPin, 600);  // Activa el zumbador a 600 Hz
        delay(500);
    }

4. En este punto, puedes subir el código al Arduino Uno R3 y escucharás que el zumbador repite tres tonos diferentes.

5. Para lograr un aumento de tono más suave, deberíamos establecer intervalos más cortos para la ``frecuencia``, como un intervalo de 10, comenzando desde 100, 110, 120... hasta 1000. Podemos escribir el siguiente código.

.. code-block:: Arduino

    void loop() {
        // Pon tu código principal aquí, para que se ejecute repetidamente:
        tone(buzzerPin, 100);  // Activa el zumbador a 100 Hz
        delay(500);
        tone(buzzerPin, 110);  // Activa el zumbador a 110 Hz
        delay(500);
        tone(buzzerPin, 120);  // Activa el zumbador a 120 Hz
        delay(500);
        tone(buzzerPin, 130);  // Activa el zumbador a 130 Hz
        delay(500);
        tone(buzzerPin, 140);  // Activa el zumbador a 140 Hz
        delay(500);
        tone(buzzerPin, 150);  // Activa el zumbador a 150 Hz
        delay(500);
        tone(buzzerPin, 160);  // Activa el zumbador a 160 Hz
        delay(500);
        ...
    }

6. Notarás que si realmente quisieras escribir hasta 1000, este código tendría más de doscientas líneas. En este punto, puedes usar la sentencia ``for``, que se usa para repetir un bloque de instrucciones entre llaves.

    * ``for``: La sentencia ``for`` es útil para cualquier operación repetitiva, y a menudo se usa junto con matrices para operar sobre colecciones de datos/pines. Generalmente, se usa un contador de incremento para controlar la repetición y finalizar el bucle.

    **Sintaxis**

    .. code-block::

        for (inicialización; condición; incremento) {
            // instrucción(es);
        }

    **Parámetros**

        * ``inicialización``: se ejecuta primero y solo una vez.
        * ``condición``: cada vez que pasa por el bucle, se prueba la condición; si es verdadera, se ejecuta el bloque de instrucciones y el incremento, luego se prueba la condición nuevamente. Cuando la condición es falsa, el bucle termina.
        * ``incremento``: se ejecuta cada vez que pasa por el bucle cuando la condición es verdadera.

.. image:: img/for_loop.png
    :width: 400
    :align: center

7. Ahora cambia la función ``void loop()`` como se muestra a continuación, donde ``freq`` comienza en 100 y aumenta de 10 en 10 hasta 1000.

.. code-block:: Arduino
    :emphasize-lines: 3-6

    void loop() {
        // Incrementa gradualmente el tono
        for (int freq = 100; freq <= 1000; freq += 10) {
            tone(buzzerPin, freq);  // Emite un tono
            delay(20);              // Espera antes de cambiar la frecuencia
        }
    }

8. Luego, deja que ``freq`` comience en 1000 y disminuya de 10 en 10 hasta 100, para que puedas escuchar el sonido del zumbador subir y bajar de tono, simulando un sonido de sirena.

.. code-block:: Arduino
    :emphasize-lines: 9-12

    void loop() {
        // Incrementa gradualmente el tono
        for (int freq = 100; freq <= 1000; freq += 10) {
            tone(buzzerPin, freq);  // Emite un tono
            delay(20);              // Espera antes de cambiar la frecuencia
        }

        // Disminuye gradualmente el tono
        for (int freq = 1000; freq >= 100; freq -= 10) {
            tone(buzzerPin, freq);  // Emite un tono
            delay(20);              // Espera antes de cambiar la frecuencia
        }
    }

9. Aquí tienes tu código completo. Ahora puedes hacer clic en "Subir" para cargar el código en el Arduino Uno R3.

.. code-block:: Arduino

    const int buzzerPin = 9;  // Asigna el pin 9 a la constante para el zumbador

    void setup() {
        // Pon tu código de configuración aquí, para que se ejecute una vez:
    }

    void loop() {
        // Incrementa gradualmente el tono
        for (int freq = 100; freq <= 1000; freq += 10) {
            tone(buzzerPin, freq);  // Emite un tono
            delay(20);              // Espera antes de cambiar la frecuencia
        }

        // Disminuye gradualmente el tono
        for (int freq = 1000; freq >= 100; freq -= 10) {
            tone(buzzerPin, freq);  // Emite un tono
            delay(20);              // Espera antes de cambiar la frecuencia
        }
    }

10. Finalmente, recuerda guardar tu código y organizar tu espacio de trabajo.

**Resumen**

En esta lección, exploramos cómo usar un Arduino y un zumbador pasivo para simular el sonido de una sirena. Al discutir las propiedades físicas básicas del sonido, como la frecuencia y el tono, aprendimos cómo estos elementos influyen en la percepción y el efecto del sonido. A través de actividades prácticas, no solo aprendimos a construir circuitos, sino que también dominamos la programación con la función ``tone()`` en Arduino para controlar la frecuencia y la duración del sonido, logrando la simulación de un sonido de sirena que sube y baja de tono.

