.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Únete para profundizar en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Soluciona problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos exclusivos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.


7. ¡Hagamos un Semáforo!
==============================

.. .. image:: img/5_traffic_light_pic.png
..     :width: 400
..     :align: center

¡Bienvenido a esta lección! En esta interesante sesión, conectaremos conceptos teóricos con la aplicación práctica en electrónica y programación. Aprenderemos a convertir pseudocódigo—una forma simplificada de lenguaje de programación—en sketches funcionales para Arduino. Este ejercicio simulará el funcionamiento de un semáforo, ofreciéndote experiencia práctica en programación y diseño de circuitos. Al aprender a interpretar e implementar pseudocódigo, adquirirás una comprensión más profunda de la lógica detrás del control de dispositivos electrónicos mediante código.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/7_traffic_light.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

En esta lección aprenderás a:

* Escribir e interpretar pseudocódigo para planificar la funcionalidad de circuitos electrónicos.
* Convertir pseudocódigo en sketches de Arduino para controlar la simulación de semáforos.
* Construir y programar un sistema de semáforos usando LEDs y una placa Arduino.

Al dominar estas habilidades, estarás equipado para diseñar, programar y resolver problemas en sistemas electrónicos básicos, allanando el camino hacia proyectos más complejos.

Preparando el Semáforo
------------------------------------------

¡Hola! ¿Listo para crear tu propio semáforo con un Arduino? Aquí tienes lo que necesitamos:

**Componentes necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rojo
     - 1 * LED amarillo
     - 1 * LED verde
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_yellow_led| 
     - |list_green_led| 
   * - 1 * Cable USB
     - 1 * Protoboard
     - 3 * Resistencias de 220Ω
     - Cables de conexión
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_wire| 


**Paso a paso**

¡Vamos a armarlo todo, como si fuera un set de LEGO!

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

1. Conecta una resistencia de 220Ω al protoboard. Un extremo debe ir al terminal negativo, y el otro en el orificio 1B.

.. image:: img/7_traffic_light_resistor.png
    :width: 600
    :align: center

2. Añade un LED verde al protoboard. El ánodo del LED (pata larga) debe ir en el orificio 1F. El cátodo (pata corta) debe ir en el orificio 1E.

.. image:: img/7_traffic_light_green.png
    :width: 600
    :align: center

3. Conecta el LED verde al pin 3 del Arduino Uno R3 con un cable. Inserta un cable en el orificio 1J y conecta el otro extremo en el pin 3 del Arduino Uno R3.

.. image:: img/7_traffic_light_pin3.png
    :width: 600
    :align: center

4. Toma otra resistencia de 220Ω, conecta un extremo al terminal negativo y el otro extremo al orificio 6B.

.. image:: img/7_traffic_light_yellow_resistor.png
    :width: 600
    :align: center

5. Toma un LED amarillo. El ánodo del LED (pata larga) debe ir en el orificio 6F. El cátodo (pata corta) debe ir en el orificio 6E.

.. image:: img/7_traffic_light_yellow.png
    :width: 600
    :align: center

6. Conecta el LED amarillo al pin 4 del Arduino Uno R3.

.. image:: img/7_traffic_light_pin4.png
    :width: 600
    :align: center

7. Conecta el LED rojo de la misma manera; el LED rojo se conecta al pin 5 del Arduino Uno R3.

.. image:: img/7_traffic_light_red.png
    :width: 600
    :align: center

8. ¡Oops! Casi olvidamos conectar a tierra el circuito. Conecta el lado negativo del protoboard a un pin GND del Arduino Uno R3 con un cable negro. ¡Ahora está todo listo!

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

.. note::

    Hay tres pines GND en el Arduino Uno R3. Puedes usar cualquiera de ellos; todos funcionan de la misma manera.

¡Y así de simple tienes un semáforo completo! Cada luz de color es controlada por su propio interruptor en el R3, lista para indicar a los autos cuándo detenerse, esperar o avanzar. ¿No es increíble construir algo que funciona como un semáforo real? ¡Buen trabajo!

Escribiendo Pseudocódigo para un Semáforo
----------------------------------------------

Es hora de darle un propósito a tus LEDs. En esta actividad, los programarás para que funcionen como un semáforo, controlando el flujo de tráfico en una intersección concurrida.

Los semáforos requieren un control preciso para cambiar entre los tres colores en una secuencia estricta, lo que lo convierte en un proyecto ideal para adentrarse en la programación de Arduino. Para perfeccionar nuestro semáforo, debemos dar instrucciones claras al Arduino sobre sus tareas.

La comunicación entre humanos implica escuchar, hablar, leer, escribir, gesticular o hacer expresiones faciales. La comunicación con microcontroladores (como el que está en tu placa Arduino) implica escribir código.

No podemos simplemente decirle al Arduino que "haga un semáforo" en lenguaje natural. Sin embargo, podemos usar lenguaje natural para escribir un "pseudocódigo" que nos ayude a desarrollar el código real para Arduino.

.. note::
    
    No hay respuestas correctas o incorrectas al escribir pseudocódigo. Cuanto más detallado sea tu pseudocódigo, más fácil será traducirlo en un programa funcional.

Piensa en lo que debe suceder para que tu circuito funcione como un semáforo. En el espacio proporcionado en tu registro, escribe el pseudocódigo que describa cómo funcionará tu semáforo. Usa lenguaje sencillo.

Aquí tienes algunas preguntas orientadoras para tu pseudocódigo:

* ¿Deben estar encendidas dos o más luces al mismo tiempo?
* ¿Cuál es el orden de las luces?
* ¿Qué pasa con las otras luces cuando una está encendida?
* ¿Qué sucede después de que la tercera luz se apaga?
* ¿Cuánto tiempo debe permanecer encendida cada luz?

Aquí tienes un par de ejemplos de pseudocódigo:

.. code-block::

    1) Set all LED pins to output.
    2) Start main loop.
    a) Turn off all lights.
    b) Turn on green light for 10 seconds.
    c) Turn off all lights.
    d) Turn on yellow light for 3 seconds.
    e) Turn off all lights.
    f) Turn on red light for 10 seconds.
    3) Return to the start of the loop.

.. code-block::

    Setup:
        Define all LED pins as output
    Main Loop:
        Turn on green light
        Turn off red and yellow lights
        Wait 10 seconds
        Turn on yellow light
        Turn off red and green lights
        Wait 3 seconds
        Turn on red light
        Turn off green and yellow lights
        Wait 10 seconds

El pseudocódigo no tiene un formato estricto, lo que te permite aclarar tus pensamientos y organizarlos de manera lógica. Este orden lógico se llama algoritmo.
Usas algoritmos todos los días, quizás sin darte cuenta. Piensa en un algoritmo como una receta; en programación, los ingredientes son las palabras clave y los comandos, y los pasos de cocción son el algoritmo.
Un algoritmo es un conjunto de pasos o instrucciones. Cuando un algoritmo se traduce de pseudocódigo a lenguaje de programación de Arduino, le indica a la placa Arduino exactamente qué hacer y cuándo.

.. note::
    
    Usar notas adhesivas o tarjetas puede ser útil al escribir pseudocódigo. Coloca cada paso de tu algoritmo en una nota separada. De esta manera, puedes reorganizar, insertar o eliminar pasos fácilmente.


Transforma el Pseudocódigo en un Sketch para Arduino
--------------------------------------------------------

Es hora de refinar el código que has escrito y agregar los comandos ``digitalWrite()`` y ``delay()`` adicionales según sea necesario. Aquí tienes una guía para estructurar tu código: tu función ``void loop()`` debe encapsular segmentos separados para los LEDs verde, amarillo y rojo, cada uno seguido por un período de retraso único. No todos los retrasos deben ser de la misma duración. Actualiza los comentarios de tu código para que quede claro lo que logra cada línea.

1. Abre el sketch que guardaste antes, ``Lesson6_Blink_LED``. Haz clic en "Guardar como..." en el menú "Archivo" y renómbralo a ``Lesson7_Traffic_Light``. Haz clic en "Guardar".

2. Ahora, según nuestro pseudocódigo, configura los tres pines como salida en el ``void setup()``. Copia el comando ``pinMode()`` dos veces, pégalo a continuación y ajusta los números de los pines para cada uno.

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void setup() {
            // Código de configuración que se ejecuta una vez:
            pinMode(3, OUTPUT); // configurar el pin 3 como salida
            pinMode(4, OUTPUT); // configurar el pin 4 como salida
            pinMode(5, OUTPUT); // configurar el pin 5 como salida
        }

3. En ``void loop()``, primero enciende el LED verde y apaga los otros dos LEDs. Así que, copia los comandos ``digitalWrite()`` dos veces, modifica los números de los pines a 4 y 5, cambia ``HIGH`` a ``LOW`` para los LEDs que quieras apagar y actualiza los comentarios para que se ajusten al escenario actual. El código modificado es el siguiente:

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void loop() {
            // El código principal que se ejecuta repetidamente:
            digitalWrite(3, HIGH);  // Encender el LED en el pin 3
            digitalWrite(4, LOW);   // Apagar el LED en el pin 4
            digitalWrite(5, LOW);   // Apagar el LED en el pin 5
            delay(3000);           // Esperar 3 segundos
        }
4. Quizás quieras que el LED verde permanezca encendido por más tiempo. En nuestro sistema de tráfico real, podría estar encendido alrededor de un minuto, pero aquí lo simularemos con 10 segundos.

    .. code-block:: Arduino
        :emphasize-lines: 6

        void loop() {
            // El código principal que se ejecuta repetidamente:
            digitalWrite(3, HIGH);  // Encender el LED en el pin 3
            digitalWrite(4, LOW);   // Apagar el LED en el pin 4
            digitalWrite(5, LOW);   // Apagar el LED en el pin 5
            delay(10000);           // Esperar 10 segundos
        }

5. Ahora deja que el LED amarillo se encienda y apaga los otros dos LEDs. Nuevamente, copia y pega las 4 líneas de ``void loop()``, configurando el pin 4 en HIGH y los demás en LOW. Cambia el retraso para el LED amarillo a 3 segundos.

    .. code-block:: Arduino
        :emphasize-lines: 7-10

        void loop() {
            // El código principal que se ejecuta repetidamente:
            digitalWrite(3, HIGH);  // Encender el LED en el pin 3
            digitalWrite(4, LOW);   // Apagar el LED en el pin 4
            digitalWrite(5, LOW);   // Apagar el LED en el pin 5
            delay(10000);           // Esperar 10 segundos
            digitalWrite(3, LOW);   // Apagar el LED en el pin 3
            digitalWrite(4, HIGH);  // Encender el LED en el pin 4
            digitalWrite(5, LOW);   // Apagar el LED en el pin 5
            delay(3000);            // Esperar 3 segundos
        }

6. Finalmente, deja que el LED rojo se encienda por 10 segundos, apagando los otros dos LEDs. El código completo es el siguiente:

    .. code-block:: Arduino

        void setup() {
            // Código de configuración que se ejecuta una vez:
            pinMode(3, OUTPUT); // configurar el pin 3 como salida
            pinMode(4, OUTPUT); // configurar el pin 4 como salida
            pinMode(5, OUTPUT); // configurar el pin 5 como salida
        }
        
        void loop() {
            // El código principal que se ejecuta repetidamente:
            digitalWrite(3, HIGH);  // Encender el LED en el pin 3
            digitalWrite(4, LOW);   // Apagar el LED en el pin 4
            digitalWrite(5, LOW);   // Apagar el LED en el pin 5
            delay(10000);           // Esperar 10 segundos
            digitalWrite(3, LOW);   // Apagar el LED en el pin 3
            digitalWrite(4, HIGH);  // Encender el LED en el pin 4
            digitalWrite(5, LOW);   // Apagar el LED en el pin 5
            delay(3000);            // Esperar 3 segundos
            digitalWrite(3, LOW);   // Apagar el LED en el pin 3
            digitalWrite(4, LOW);   // Apagar el LED en el pin 4
            digitalWrite(5, HIGH);  // Encender el LED en el pin 5
            delay(10000);           // Esperar 10 segundos
        }

**Pregunta**

Observa los cruces de calles cerca de tu casa. ¿Cuántos semáforos suele haber? ¿Cómo se coordinan entre ellos?

**Resumen**

¡Felicitaciones por completar la Lección 7! Has logrado traducir pseudocódigo en un sistema de semáforo funcional controlado por Arduino. Aquí tienes un breve resumen de lo que lograste:

* Dominio del Pseudocódigo: Aprendiste a usar pseudocódigo para planificar el funcionamiento de sistemas electrónicos, mejorando tus habilidades de pensamiento lógico y planificación.
* Del Pseudocódigo al Código Real: Experimentaste cómo un enfoque estructurado en pseudocódigo conduce a una programación efectiva y precisa en Arduino.
* Aplicación Práctica: Al ensamblar y programar un sistema de semáforo, demostraste una aplicación práctica de tus conocimientos, mostrando cómo el software controla directamente el hardware.

Esta lección ha mejorado tanto tus habilidades técnicas como tu capacidad de análisis, preparándote para proyectos más complejos en electrónica y programación. ¡Sigue construyendo sobre estas habilidades para desbloquear nuevas posibilidades en la integración tecnológica!
