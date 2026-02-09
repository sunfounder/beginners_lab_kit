.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook. Sumérgete más profundamente en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos exclusivos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy mismo!

23. Dado Cibernético
========================

En esta lección, emprenderemos un emocionante viaje a través de dos proyectos que combinan electrónica digital y programación.

.. image:: img/23_dice.jpg
    :align: center
    :width: 500

Primero, exploraremos el funcionamiento de una pantalla de 7 segmentos, aprendiendo cómo controlarla para mostrar números paso a paso. Luego, crearemos un dado electrónico: simplemente presionando un botón, aparecerá un número aleatorio del 1 al 6 en la pantalla de 7 segmentos, ofreciendo una versión digital del dado tradicional.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/23_cycle_dice.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Durante esta lección, aprenderás:

* Los principios de cómo funciona una pantalla de 7 segmentos y cómo hacerla funcionar.
* El uso de declaraciones switch-case para simplificar la lógica del código.
* Cómo utilizar un bucle while para mantener el estado actual hasta que sea necesario un cambio.
* Cómo construir el proyecto Dado Cibernético, integrando electrónica simple con programación interactiva para una aplicación práctica.

El origen de los dados
---------------------------

Los dados son una de las herramientas de juego más antiguas del mundo, con una historia que se remonta a miles de años antes de la era común. Se originaron alrededor del 3000 a.C. en el antiguo Egipto, y solían estar hechos de huesos, marfil u otros materiales naturales. Estos primeros dados a menudo eran de formas irregulares y no siempre completamente simétricos.

.. image:: img/23_dice.png
    :width: 500
    :align: center

También se encontraron dados en la antigua Mesopotamia (actual Irak) alrededor de la misma época. Los adivinos y líderes religiosos antiguos utilizaban dados para tomar decisiones o predecir el futuro, lo que resalta su importancia en ritos religiosos y místicos.

Con el tiempo, la forma y las técnicas de fabricación de los dados se estandarizaron. Para el siglo I a.C., los dados se usaban ampliamente en el Imperio Romano, no solo para juegos de azar, sino también para fines sociales y de entretenimiento.

En Asia, especialmente en la India, el uso de dados se documenta en la antigua epopeya Mahabharata, donde un juego de dados desempeña un papel crucial en la trama.

Durante el Renacimiento, la producción de dados se refinó y los materiales se diversificaron para incluir madera, hueso, marfil e incluso metal. Hoy en día, los dados no solo se utilizan en juegos de entretenimiento y apuestas, sino también en educación, apoyo a la toma de decisiones y en diversos juegos de mesa. Su historia y diversidad reflejan la evolución de la cultura y la tecnología humanas, ofreciendo una ventana fascinante a la exploración del azar y la suerte.



Comprendiendo la pantalla de 7 segmentos
----------------------------------------------

1. Encuentra una pantalla de 7 segmentos.

Una pantalla de 7 segmentos es un componente con forma de "8" que contiene 7 LED. Cada uno de los LED en la pantalla tiene un segmento posicional y un pin de conexión que sobresale del paquete plástico rectangular. Estos pines LED están etiquetados de la "a" a la "g", representando cada LED individual.
Los otros pines LED están conectados formando un pin común. Un octavo LED adicional se utiliza dentro del mismo paquete, lo que permite indicar un punto decimal (DP) cuando dos o más pantallas de 7 segmentos están conectadas para mostrar números mayores de diez.

.. image:: img/23_7_segment.png
    :width: 300
    :align: center

El pin común de la pantalla generalmente indica su tipo. Hay dos tipos de conexiones de pines: una con cátodos conectados y otra con ánodos conectados, lo que indica Cátodo Común (CC) y Ánodo Común (CA). Como su nombre indica, una pantalla CC tiene todos los cátodos de los 7 LED conectados, mientras que una pantalla CA tiene todos los ánodos de los 7 segmentos conectados.

.. note::

    Normalmente, hay una etiqueta en el lateral de la pantalla de 7 segmentos, xxxAx o xxxBx. Generalmente, xxxAx significa cátodo común y xxxBx significa ánodo común. Las pantallas de nuestro kit son de cátodo común.

.. image:: img/23_segment_cathode_1.png
    :align: center
    :width: 600

Para determinar si una pantalla de 7 segmentos es de cátodo común o de ánodo común, puedes utilizar un multímetro. También puedes usar un multímetro para probar si cada segmento de la pantalla funciona correctamente, de la siguiente manera:

1. Configura el multímetro en modo de prueba de diodos. La prueba de diodos es una función del multímetro que se utiliza para verificar la conducción directa de diodos u otros dispositivos semiconductores similares (como los LED). El multímetro pasa una pequeña corriente a través del diodo. Si el diodo está intacto, permitirá que la corriente pase.

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. Inserta la pantalla de 7 segmentos en una placa de pruebas, asegurándote de que el punto decimal esté en la parte inferior derecha y de que se extienda a través del espacio central. Inserta un cable en la misma fila que el pin 1 de la pantalla y tócala con la punta roja del multímetro. Inserta otro cable en la misma fila que cualquier pin marcado con "-" de la pantalla y tócala con la punta negra.

.. image:: img/23_7_segment_test.png
    :align: center
    :width: 500

3. Observa si algún segmento LED se enciende. Si es así, indica que la pantalla es de cátodo común. Si no, intercambia las puntas roja y negra; si un segmento se ilumina después de cambiarlas, indica que la pantalla es de ánodo común.

4. Si un segmento se ilumina, consulta este diagrama para registrar el número de pin del segmento y su posición aproximada en la tabla del manual.

.. image:: img/23_segment_2.png
    :align: center

.. list-table::
    :widths: 20 20 40
    :header-rows: 1

    *   - Pin
        - Segment Number
        - Position
    *   - 1
        - a
        - The top segment
    *   - 2
        -
        -
    *   - 3
        -
        -
    *   - 4
        -
        -
    *   - 5
        -
        -
    *   - 6
        -
        -
    *   - 7
        -
        -
    *   - 8
        -
        -     

5. Repite los pasos anteriores, manteniendo la punta negra en el pin "-" y conectando la punta roja a los demás pines para encontrar los pines de control correspondientes a los segmentos LED de la pantalla.


**Pregunta**

En las pruebas anteriores, se ha determinado que la pantalla del kit es de cátodo común, lo que significa que solo necesitas conectar el pin común a GND y proporcionar un voltaje alto a los demás pines para encender los segmentos correspondientes. Si deseas que la pantalla muestre el número 2, ¿a qué pines deberías proporcionar un voltaje alto? ¿Por qué?

.. image:: img/23_segment_2.png
    :align: center


Construyendo el Circuito
--------------------------------

**Componentes necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Pantalla de 7 segmentos
     - 1 * Resistor de 220Ω
     - 1 * Resistor de 10KΩ
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Botón
     - 1 * Placa de pruebas
     - Cables de puente
     - 1 * Cable USB
   * - |list_button| 
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



**Paso a paso**

Sigue el diagrama de cableado o los siguientes pasos para construir tu circuito.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

1. Inserta la pantalla de 7 segmentos en la placa de pruebas con el punto decimal en la esquina inferior derecha.

.. image:: img/23_segment_segment.png
    :align: center
    :width: 500

2. Inserta un extremo de una resistencia de 220Ω en el terminal negativo (“-”) de la pantalla de 7 segmentos y el otro extremo en el riel negativo de la placa de pruebas. Luego, conecta el riel negativo de la placa de pruebas al pin GND del Arduino Uno R3 con un cable de puente.

.. image:: img/23_segment_resistor_gnd.png
    :align: center
    :width: 500

3. Conecta los pines que controlan los segmentos a, b y c del LED a los pines 2, 3 y 4 del Arduino Uno R3.

.. image:: img/23_segment_abc.png
    :align: center
    :width: 500

4. Conecta los pines que controlan los segmentos d, e, f y g del LED a los pines 5, 6, 7 y 8 del Arduino Uno R3.

.. image:: img/23_segment_defg.png
    :align: center
    :width: 500

5. Ahora inserta un botón en la placa de pruebas.

.. image:: img/23_segment_button.png
    :align: center
    :width: 500

6. Conecta el pin inferior derecho del botón al pin 9 del R3 con un cable.

.. image:: img/23_segment_pin9.png
    :align: center
    :width: 500

7. Conecta una resistencia de pull-down de 10K al botón para que cuando el botón no esté presionado, el pin 9 permanezca en nivel bajo y no rebote.

.. image:: img/23_segment_10k_resistor.png
    :align: center
    :width: 500

8. Conecta el pin inferior izquierdo del botón al pin de 5V del Arduino Uno R3.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - Pantalla de 7 segmentos
        - Arduino UNO R3
    *   - a
        - 2
    *   - b
        - 3
    *   - c
        - 4
    *   - d
        - 5
    *   - e
        - 6
    *   - f
        - 7
    *   - g
        - 8


Creación de código - Mostrando números
------------------------------------------
1. Abre el IDE de Arduino y comienza un nuevo proyecto seleccionando "Nuevo boceto" desde el menú "Archivo".
2. Guarda tu boceto como ``Lesson23_Show_Number`` usando ``Ctrl + S`` o haciendo clic en “Guardar”.

3. Define los pines conectados a la pantalla de 7 segmentos y configura todos los pines como salidas.

.. code-block:: Arduino

    // Definir los pines conectados a la pantalla de 7 segmentos
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Configurar todos los pines como salidas
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

4. Ahora escribe el código para que la pantalla de 7 segmentos muestre un número, como el número 2. Para mostrar el número 2, configura los segmentos F y C en LOW (apagado), y los demás segmentos en HIGH (encendido).

.. code-block:: Arduino
  :emphasize-lines: 22-29

    // Definir los pines conectados a la pantalla de 7 segmentos
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Configurar todos los pines como salidas
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {
        // Configurar los segmentos F y C en LOW (apagado), y otros segmentos en HIGH (encendido)
        digitalWrite(pinA, HIGH);
        digitalWrite(pinB, HIGH);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, HIGH);
        digitalWrite(pinE, HIGH);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, HIGH);
    }

5. Ahora puedes cargar el código en el Arduino Uno R3, y verás el número 2 mostrado en la pantalla de 7 segmentos.

6. Si necesitas mostrar otros números, como recorrer del 1 al 6, usar ``digitalWrite()`` para configurar cada segmento haría que el código fuera muy largo y la lógica menos clara. Aquí utilizamos un método de creación de funciones en su lugar.

7. Crea una función con un parámetro: ``displayDigit()``, que primero apaga todos los segmentos LED de la pantalla de 7 segmentos.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Apagar todos los segmentos
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);
    }

8. A continuación, controla diferentes segmentos LED para mostrar números. Aquí podríamos usar sentencias ``if-else``, pero eso podría ser engorroso. Por lo tanto, una declaración ``switch`` proporciona una forma más clara y organizada de elegir entre múltiples comportamientos posibles que varias sentencias ``if-else``.

En programación, una declaración ``switch`` es una estructura de control que se usa para ejecutar diferentes segmentos de código según el valor de una variable.

La sintaxis básica de una declaración ``switch`` es la siguiente:

.. code-block:: Arduino

    switch (expression) {
        case value1:
            // código
            break;
        case value2:
            // código
            break;
        default:
            // código
    }

* ``expression``: Esta es una expresión que generalmente devuelve un entero o carácter, con base en lo cual la declaración ``switch`` decide qué ``case`` ejecutar.
* ``case``: Cada palabra clave ``case`` está seguida por un valor que puede coincidir con el resultado de ``expression``. Si se encuentra una coincidencia, el código se ejecuta desde este punto hasta encontrar una sentencia ``break``.
* ``break``: La sentencia ``break`` se usa para salir del bloque ``switch``. Sin ella, el programa continuaría ejecutando el código del siguiente caso, independientemente de su coincidencia, lo que se conoce como "fall-through".
* ``default``: La parte ``default`` es opcional y se ejecuta si ningún ``case`` coincide, similar a ``else`` en una estructura ``if-else``.

.. image:: img/23_flow_swtich.png
    :align: center
    :width: 600

9. Usa ``switch-case`` en la función ``displayDigit()`` para completar la visualización de números en la pantalla de 7 segmentos. Por ejemplo, para mostrar el 1, solo se necesitan los segmentos B y C en alto; para mostrar el 2, los segmentos F y C deben estar en bajo, mientras que los demás en alto.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Apagar todos los segmentos
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Configurar en HIGH para encender los segmentos necesarios para el número deseado
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }

10. Ahora puedes llamar a ``displayDigit()`` en la función ``void loop()`` para mostrar números específicos, como alternar entre 3 y 6 con un intervalo de un segundo.

.. code-block:: Arduino

    void loop() {

        displayDigit(3);  // Mostrar el número 3 en la pantalla de 7 segmentos
        delay(1000);
        displayDigit(6);  // Mostrar el número 6 en la pantalla de 7 segmentos
        delay(1000);
    }

11. A continuación se muestra tu código completo. Ahora puedes cargar el código en el Arduino Uno R3, y verás que la pantalla de 7 segmentos alterna entre los números 3 y 6.

.. code-block:: Arduino

    // Definir los pines conectados a la pantalla de 7 segmentos
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Configurar todos los pines como salidas
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {

        displayDigit(3);  // Mostrar el número 3 en la pantalla de 7 segmentos
        delay(1000);
        displayDigit(6);  // Mostrar el número 6 en la pantalla de 7 segmentos
        delay(1000);
    }

    void displayDigit(int digit) {
        // Apagar todos los segmentos
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Encender los segmentos necesarios para el número deseado (HIGH enciende los segmentos para cátodo común)
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }

Creación del Código - Cyber Dice
------------------------------------------
Ahora que sabemos cómo mostrar los números del 1 al 6 en la pantalla de 7 segmentos, ¿cómo podemos lograr el efecto de un Cyber Dice?

Esto implica presionar un botón para hacer que la pantalla recorra los números del 1 al 6, y soltar el botón para mostrar un número fijo. Veamos cómo podemos lograr esto con código.

1. Abre el sketch que guardaste anteriormente, ``Lesson23_Show_Number``.

2. Selecciona “Guardar como...” desde el menú “Archivo” y renómbralo como ``Lesson23_Cyber_Dice``. Haz clic en "Guardar".

3. Define el pin del botón y configúralo como entrada.

.. code-block:: Arduino
    :emphasize-lines: 10-11,23-24

    // Definir los pines conectados a los segmentos de la pantalla de 7 segmentos
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Definir el pin conectado al botón
    int buttonPin = 9;

    void setup() {
        // Configurar todos los pines como salidas
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Configurar el pin del botón como entrada
        pinMode(buttonPin, INPUT);
    }

4. Verifica si el botón está presionado en el momento en que se ejecuta la función ``void loop()``. Si el botón no está presionado, el código dentro del bloque ``if`` se omite.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // Verificar si el botón está presionado
        if (digitalRead(buttonPin) == HIGH) {
        }
    }

5. En la programación de Arduino o microcontroladores similares, un problema común al trabajar con entradas de botones es asegurar que cada pulsación genere solo una acción, especialmente al generar eventos o comandos (como generar un número aleatorio). Para abordar esto, podemos utilizar una técnica conocida como "esperar a que se suelte".

**esperar-a-la-liberación**

La idea principal de este método es que, después de presionar un botón y realizar una acción, el programa entra en un bucle que continúa monitoreando el estado del botón hasta que se libera. Esto asegura que no se disparen acciones adicionales debido a rebotes del botón o porque el usuario mantenga presionado el botón.

Podemos implementar esto con un bucle ``while`` en el código.

.. image:: img/while_loop.png
    :width: 400
    :align: center

.. code-block:: Arduino
    :emphasize-lines: 4-6

    void loop() {
        // Verificar si el botón está presionado
        if (digitalRead(buttonPin) == HIGH) {
            // Esperar a que se suelte el botón antes de continuar
            while (digitalRead(buttonPin) == HIGH) {
            }
        }
    }

6. Ahora, usa la función ``random()`` para generar un número aleatorio entre 1 y 6, y usa ``displayDigit()`` para mostrar este número en la pantalla de 7 segmentos. Verás que la pantalla cambia rápidamente entre diferentes números mientras se mantiene presionado el botón.

.. code-block:: Arduino
    :emphasize-lines: 6-12

    void loop() {
        // Verificar si el botón está presionado
        if (digitalRead(buttonPin) == HIGH) {
            // Esperar a que se suelte el botón antes de continuar
            while (digitalRead(buttonPin) == HIGH) {
                // Generar un número aleatorio entre 1 y 6
                int num = random(1, 7);
                
                // Mostrar el número aleatorio en la pantalla de 7 segmentos
                displayDigit(num);
                // Esperar un corto período para permitir la actualización visible
                delay(100);
            }
        }
    }

7. Finalmente, agrega un retraso para eliminar el rebote del botón y evitar múltiples entradas rápidas.

.. code-block:: Arduino
    :emphasize-lines: 15

    void loop() {
        // Verificar si el botón está presionado
        if (digitalRead(buttonPin) == HIGH) {
            // Esperar a que se suelte el botón antes de continuar
            while (digitalRead(buttonPin) == HIGH) {
                // Generar un número aleatorio entre 1 y 6
                int num = random(1, 7);
                
                // Mostrar el número aleatorio en la pantalla de 7 segmentos
                displayDigit(num);
                // Esperar un corto período para permitir la actualización visible
                delay(100);
            }
            // Agregar un retraso para eliminar el rebote del botón y evitar múltiples entradas rápidas
            delay(500);
        }
    }

8. Tu código completo debería verse así. Ahora puedes cargar el código en el Arduino Uno R3. Una vez cargado, si mantienes presionado el botón, los números en la pantalla cambiarán rápidamente, y al soltarlo, se mostrará un número.

.. code-block:: Arduino

    // Definir los pines conectados a los segmentos de la pantalla de 7 segmentos
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Definir el pin conectado al botón
    int buttonPin = 9;

    void setup() {
        // Configurar todos los pines como salidas
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Configurar el pin del botón como entrada
        pinMode(buttonPin, INPUT);
    }

    void loop() {
        // Verificar si el botón está presionado
        if (digitalRead(buttonPin) == HIGH) {
            // Esperar a que se suelte el botón antes de continuar
            while (digitalRead(buttonPin) == HIGH) {
                // Generar un número aleatorio entre 1 y 6
                int num = random(1, 7);

                // Mostrar el número aleatorio en la pantalla de 7 segmentos
                displayDigit(num);
                // Esperar un corto período para permitir la actualización visible
                delay(100);
            }
            // Agregar un retraso para eliminar el rebote del botón y evitar múltiples entradas rápidas
            delay(500);
        }
    }

    void displayDigit(int digit) {
        // Apagar todos los segmentos
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Encender los segmentos necesarios para el número deseado (LOW enciende los segmentos para cátodo común)
        switch (digit) {
            case 1:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            break;
            case 2:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 3:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 4:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 5:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 6:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
        }
    }

9. Finalmente, recuerda guardar tu código y organizar tu espacio de trabajo.

**Resumen**

En esta lección, hemos completado con éxito el proyecto Cyber Dice, lo que te permite participar en competiciones amistosas con tus amigos para ver quién obtiene el número más alto. A lo largo de esta lección, exploramos el funcionamiento de una pantalla de 7 segmentos, aprendiendo cómo controlarla de manera efectiva. Simplificamos nuestro código usando declaraciones ``switch-case``, mejorando la legibilidad y eficiencia.

Además, implementamos la lógica para controlar la visualización de números aleatorios en la pantalla de 7 segmentos según el estado de la pulsación de un botón, agregando interacción dinámica a nuestro proyecto. Esta experiencia práctica no solo te familiariza con componentes electrónicos básicos y estrategias de codificación, sino que también ilustra aplicaciones prácticas de estas habilidades para crear proyectos interactivos y entretenidos.
