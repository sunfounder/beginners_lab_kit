.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook. Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones navideñas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

14. Colores aleatorios
=========================

A veces, la vida necesita un toque de sorpresa. Cuando te sientas indeciso, deja que la aleatoriedad tome las riendas. Esta lección te guiará para que un LED RGB emita colores aleatorios, ideal cuando quieras agregar un toque impredecible a tus proyectos.

Construyendo el circuito
---------------------------

**Componentes necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Resistor de 220Ω
     - Cables de conexión
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Cable USB
     - 1 * Protoboard
     - 
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - 
     - 

Esta lección utiliza el mismo circuito de la Lección 12.

.. image:: img/12_mix_color_bb_4.png
    :width: 600
    :align: center

Creación del código
----------------------

En las lecciones anteriores, controlaste el LED RGB para mostrar los colores que deseabas. Pero a veces no necesitas que muestre un color específico; en su lugar, podrías querer que muestre un color aleatorio, como las luces del escenario. ¿Cómo podemos hacer esto?

**Conociendo las funciones random()**

En el mundo físico, la aleatoriedad abunda, pero en programación, los llamados números "aleatorios" suelen calcularse mediante un algoritmo determinista. Este algoritmo generalmente requiere un punto de partida conocido como "semilla", lo que hace que estos números sean predecibles y, por tanto, se les llame "pseudo-aleatorios". El prefijo "pseudo" indica que estos números parecen aleatorios, pero en realidad siguen un patrón.

Curiosamente, en un Arduino Uno R3, podemos usar mediciones físicas del mundo real como semillas. Durante las mediciones con un multímetro, es posible que notes pequeñas fluctuaciones en los valores de voltaje y corriente del circuito. Estas fluctuaciones pueden aportar imprevisibilidad a nuestros números aleatorios.

Arduino utiliza varias funciones para la aleatoriedad:

* ``randomSeed();``: Inicializa el valor de la semilla del generador de números aleatorios. Esta función garantiza que el punto de partida de la secuencia de números aleatorios varíe en cada ejecución del programa, produciendo secuencias diferentes.

    **Parámetros**
        * ``seed``: Un valor usado para inicializar el generador de números aleatorios. Este valor unsigned long establece el punto de inicio de la secuencia aleatoria.
    **Devuelve**
        Ninguno.

* ``long random(long max);``: Genera un número aleatorio dentro de un rango específico.

    **Parámetros**
        ``max``: El límite superior del número aleatorio (``max`` no está incluido), lo que significa que el número aleatorio estará entre 0 (inclusive) y ``max-1`` (inclusive).
    
    **Devuelve**
        Un número de tipo long entre 0 y max-1.

* ``long random(long min, long max);``: Genera un número aleatorio dentro de un rango específico.

    **Parámetros**
        ``min``: El límite inferior del número aleatorio (inclusive).
        ``max``: El límite superior del número aleatorio (``max`` no incluido), lo que significa que el número aleatorio estará entre min (inclusive) y max-1 (inclusive).
    
    **Devuelve**
        Un número de tipo long entre min y max-1.

**Escribiendo el código**

1. Abre el sketch que guardaste anteriormente, ``Lesson13_PWM_Color_Mixing``.

2. Haz clic en “Guardar como...” en el menú “Archivo” y renómbralo a ``Lesson14_Random_Colors``. Haz clic en "Guardar".

3. Llama a ``randomSeed()`` solo una vez dentro de ``void setup()`` para inicializar la semilla. Evita usar un valor de semilla fijo, ya que esto haría que la misma secuencia de números aleatorios se genere cada vez que se ejecute el programa.

    Usamos ``analogRead(A0)`` para leer el valor de un pin analógico no conectado. Como este pin no está conectado, capta ruido, lo que varía en cada lectura y proporciona una buena semilla para ``randomSeed()``.

.. code-block:: Arduino
    :emphasize-lines: 9

    void setup() {
        // Código de configuración que se ejecuta una vez:
        pinMode(9, OUTPUT);   // Configurar pin azul del LED RGB como salida
        pinMode(10, OUTPUT);  // Configurar pin verde del LED RGB como salida
        pinMode(11, OUTPUT);  // Configurar pin rojo del LED RGB como salida
            
        // Inicializar la semilla aleatoria basada en un pin analógico no conectado
        randomSeed(analogRead(A0));
    }

4. Ahora en ``void loop()``, elimina el código original. Usa la función ``random()`` para generar valores aleatorios almacenados en las variables ``redValue``, ``greenValue`` y ``blueValue``.

.. code-block:: Arduino
    :emphasize-lines: 3-5

    void loop(){
        // Generar valores aleatorios para cada componente de color
        int redValue = random(0, 256);   // Valor aleatorio entre 0 y 255
        int greenValue = random(0, 256); // Valor aleatorio entre 0 y 255
        int blueValue = random(0, 256);  // Valor aleatorio entre 0 y 255
    }

5. Introduce los valores RGB generados en la función ``setColor()``, lo que permitirá que el LED RGB emita el color. También usa una función ``delay()`` para determinar cuánto tiempo se mostrará el color.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        // Generar valores aleatorios para cada componente de color entre 0 y 255
        int redValue = random(0, 256);    // Generar un valor aleatorio para rojo
        int greenValue = random(0, 256);  // Generar un valor aleatorio para verde
        int blueValue = random(0, 256);   // Generar un valor aleatorio para azul

        // Aplicar los valores de color aleatorios al LED RGB
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // Esperar 1 segundo
    }

6. Tu código completo está listo. Puedes subirlo al Arduino Uno R3 y verás que el LED RGB muestra un color aleatorio cada segundo.

.. code-block:: Arduino
    :emphasize-lines: 19,20

    void setup() {
        // Código de configuración que se ejecuta una vez:
        pinMode(9, OUTPUT);   // Configurar pin azul del LED RGB como salida
        pinMode(10, OUTPUT);  // Configurar pin verde del LED RGB como salida
        pinMode(11, OUTPUT);  // Configurar pin rojo del LED RGB como salida
        
        // Inicializar la semilla aleatoria basada en un pin analógico no conectado
        randomSeed(analogRead(A0));
    }

    void loop() {
        // Generar valores aleatorios para cada componente de color entre 0 y 255
        int redValue = random(0, 256);    // Generar un valor aleatorio para rojo
        int greenValue = random(0, 256);  // Generar un valor aleatorio para verde
        int blueValue = random(0, 256);   // Generar un valor aleatorio para azul

        // Aplicar los valores de color aleatorios al LED RGB
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // Esperar 1 segundo
    }

    // Función para configurar el color del LED RGB
    void setColor(int red, int green, int blue) {
        // Escribir valor PWM para rojo, verde y azul en el LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

7. Finalmente, recuerda guardar tu código y organizar tu espacio de trabajo.

**Preguntas**

1. Si cambias el código de ``randomSeed(analogRead(A0))`` a ``randomSeed(0)``, ¿cómo cambiarán los colores del LED RGB y por qué?

2. ¿En qué situaciones se utiliza la aleatoriedad para resolver problemas en la vida diaria, aparte de elegir colores al azar para decoración o seleccionar números de lotería?

**Resumen**

Al final de esta lección, no solo habrás aprendido sobre la aleatoriedad en la programación y cómo manipularla para crear vibrantes y sorprendentes despliegues visuales, sino que también habrás apreciado la simple belleza de la aleatoriedad en la vida diaria. La programación puede ser tan impredecible como la vida misma, y con las herramientas adecuadas, puedes aprovechar esa imprevisibilidad de maneras creativas y funcionales.
