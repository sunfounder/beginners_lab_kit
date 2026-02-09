.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. ¡Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas!

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy!

17. Código Morse
========================

El código Morse es como un lenguaje secreto que usa puntos (.) y rayas (-) inventado por Samuel Morse en la década de 1840. Fue creado para enviar mensajes a largas distancias mediante telégrafos. Cada letra del alfabeto y número está representado por una combinación única de estos símbolos. Por ejemplo, el mensaje en código Morse más famoso es "SOS" (··· ––– ···), que es una señal internacional de auxilio. El código Morse fue esencial para la comunicación antes de la invención de los teléfonos y el internet, y era especialmente popular entre los operadores de barcos y aviones. Hoy en día, es divertido aprenderlo como una forma de enviar mensajes secretos a tus amigos.

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="../_static/video/17_morse_code.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

En esta lección aprenderás:

* Cómo funciona un zumbador activo.
* A programar la señal SOS en código Morse, permitiéndote enviar mensajes con un zumbador utilizando este código.


¡La Magia del Código Morse!
--------------------------------

.. image:: img/7_morse.jpeg

¡Imagina inventar una forma de enviar mensajes secretos usando solo puntos y rayas! Eso es lo que hizo Samuel Morse en 1836 con el código Morse. Inicialmente un pintor, Morse se inspiró en un viaje en barco y más tarde, con su amigo Alfred Vail, creó el telégrafo para enviar mensajes a través de cables.

El código Morse utiliza puntos (señales cortas) y rayas (señales largas) para representar letras y números. ¿El primer mensaje en código Morse? "What hath God wrought"—enviado en 1844 desde Washington D.C. a Baltimore, marcando el inicio de la era del telégrafo.

Hoy en día, el código Morse no se usa tanto, pero sigue siendo genial para cosas como la aviación y para los aficionados a la radio. Ahora, vamos a explorar cómo funciona el código Morse con Arduino y un zumbador, ¡y a divertirnos con esta parte de la historia de la comunicación!


Construyendo el Circuito
----------------------------

**Componentes necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Zumbador Activo
     - 1 * Protoboard
     - Cables de conexión
   * - |list_uno_r3| 
     - |list_active_buzzer| 
     - |list_breadboard| 
     - |list_wire| 
   * - 1 * Cable USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 


**Pasos de Construcción**

1. Localiza un zumbador activo, que típicamente tiene una pegatina blanca en la parte delantera y un respaldo sellado negro.

.. image:: img/7_beep_2.png

Los zumbadores, como dispositivos electrónicos de sonido, tienen una rica historia que se remonta al siglo XIX. El precursor de los zumbadores modernos se origina en 1831, cuando Michael Faraday descubrió la inducción electromagnética, formando el principio fundamental detrás del funcionamiento de los zumbadores electromagnéticos. Después de este descubrimiento, muchos científicos e inventores exploraron cómo aplicar las teorías electromagnéticas a dispositivos prácticos. Hoy en día, los zumbadores se clasifican en activos y pasivos:

**Zumbador Activo**

.. image:: img/7_beep_ac.png
    :width: 300
    :align: center

Sellado en la parte posterior, los zumbadores activos contienen un oscilador interno que emite sonido cuando están alimentados, produciendo típicamente un solo tono.

**Zumbador Pasivo**

.. image:: img/7_beep_pa.png
    :width: 300
    :align: center

Abierto en la parte posterior, los zumbadores pasivos requieren una señal de frecuencia externa de un microcontrolador para generar sonido, permitiendo una gama de tonos.

2. El zumbador activo es un dispositivo polar. El lado frontal tiene un signo "+" que indica su terminal positivo (ánodo), que también es el pin más largo. Ahora inserta el zumbador en el protoboard con el ánodo en el agujero 15F y el cátodo en el agujero 18F.

.. image:: img/16_morse_code_buzzer.png
    :width: 500
    :align: center

3. Conecta el cátodo al pin GND en el Arduino Uno R3.

.. image:: img/16_morse_code_gnd.png
    :width: 500
    :align: center

4. Si insertas el ánodo del zumbador en el pin 5V del Arduino Uno R3, escucharás el zumbador activo emitir sonido directamente. Por supuesto, también puedes usar este método para verificar si el zumbador es el correcto. Un zumbador pasivo no producirá sonido cuando se conecte directamente a una fuente de alimentación.

.. image:: img/16_morse_code_5v.png
    :width: 500
    :align: center

5. Ahora, retira el cable insertado en el pin 5V e insértalo en el pin 9 del Arduino Uno R3, para que el zumbador pueda ser controlado con código.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center



Creación del Código
-----------------------
1. Abre el Arduino IDE y comienza un nuevo proyecto seleccionando "Nuevo Sketch" desde el menú "Archivo".
2. Guarda tu sketch como ``Lesson17_Morse_Code`` usando ``Ctrl + S`` o haciendo clic en "Guardar".

3. Primero, crea una constante llamada ``buzzerPin`` y asígnale el valor del pin 9.

.. code-block:: Arduino
    :emphasize-lines: 1

    const int buzzerPin = 9;   // Asigna el pin 9 a la constante para el zumbador

    void setup() {
        // Pon tu código de configuración aquí, para que se ejecute una vez:
    }

4. Inicializa el pin: En la función ``void setup()``, configura el pin del zumbador como salida.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;   // Asigna el pin 9 a la constante para el zumbador

    void setup() {
        // Pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(buzzerPin, OUTPUT);  // Configura el pin 9 como salida
    }

5. Hacer que un zumbador activo suene es tan simple como encender un LED; solo necesitas usar ``digitalWrite()`` para poner el pin 9 en alto o bajo y ``delay()`` para controlar el tiempo.

.. code-block:: Arduino
    :emphasize-lines: 10-13

    const int buzzerPin = 9;   // Asigna el pin 9 a la constante para el zumbador

    void setup() {
        // Pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(buzzerPin, OUTPUT);  // Configura el pin 9 como salida
    }

    void loop() {
        // Pon tu código principal aquí, para que se ejecute repetidamente:
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(250);                     // Duración del pitido: 250 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(250);                     // Intervalo entre señales: 250 milisegundos
    }

6. Puedes cargar tu código en el Arduino Uno R3, y luego escucharás el sonido de "bip bip".


7. Para hacer que el zumbador emita código Morse, necesitas crear dos funciones después de ``void loop()``, para emitir puntos (señales cortas) y rayas (señales largas).

.. note::

    En el código Morse, existen reglas tradicionales de temporización para los puntos (señales cortas), las rayas (señales largas) y los intervalos entre señales para asegurar que el mensaje sea recibido y comprendido correctamente. Aquí están algunas reglas básicas:

    * Duración de un punto: la unidad de tiempo básica.
    * Duración de una raya: equivale a tres puntos.
    * Intervalo entre puntos: la duración de un punto.
    * Intervalo dentro de un carácter (entre puntos y rayas de una letra o número): la duración de un punto.
    * Intervalo entre caracteres (por ejemplo, entre dos letras): tres puntos.
    * Intervalo entre palabras (por ejemplo, entre dos palabras): siete puntos.

    Por lo tanto, establecemos la duración de un punto en 250ms, una raya en 750ms y el intervalo entre elementos en 250ms.

.. code-block:: Arduino
    :emphasize-lines: 9-14,16-21

    void loop() {
        // Pon tu código principal aquí, para que se ejecute repetidamente:
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(250);                     // Duración del pitido: 250 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(250);                     // Intervalo entre señales: 250 milisegundos
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Duración corta para un punto
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalo entre señales
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Duración más larga para una raya
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalo entre señales
    }

8. Ahora, puedes transmitir código Morse. Por ejemplo, para enviar "SOS" (... --- ...), el código Morse para 'S' consiste en tres puntos, y 'O' en tres rayas, por lo que simplemente llamas a las funciones de punto y raya tres veces respectivamente.

.. code-block:: Arduino
    :emphasize-lines: 2-11

    void loop() {
        dot();
        dot();
        dot();  // S: ...
        dash();
        dash();
        dash();  // O: ---
        dot();
        dot();
        dot();       // S: ...
        delay(750);  // Repite después de un período
    }

9. Aquí está tu código completo. Ahora puedes hacer clic en "Subir" para cargar el código en el Arduino Uno R3, y luego escucharás el código Morse para "SOS" (... --- ...).

.. code-block:: Arduino

    const int buzzerPin = 9;   // Asigna el pin 9 a la constante para el zumbador
    
    void setup() {
        // Configura el pin 9 como salida:
        pinMode(buzzerPin, OUTPUT);  
    }

    void loop() {
        dot();
        dot();
        dot();  // S: ...
        dash();
        dash();
        dash();  // O: ---
        dot();
        dot();
        dot();       // S: ...
        delay(750);  // Repite después de un período
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Duración corta para un punto
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalo entre señales
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Duración más larga para una raya
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalo entre señales
    }


10. Finalmente, recuerda guardar tu código y ordenar tu área de trabajo.


**Resumen**

En esta lección, has explorado los fundamentos del código Morse, una forma única de comunicación desarrollada en la década de 1840 por Samuel Morse. Aprendiste cómo utilizar un zumbador activo para enviar el código Morse para SOS, una señal de socorro reconocida internacionalmente. Esta lección no solo te enseñó cómo configurar y programar un zumbador activo, sino que también te dio una visión de la importancia histórica del código Morse en las telecomunicaciones. Con estas habilidades, ahora puedes enviar mensajes secretos en código Morse a amigos o explorar más aplicaciones en dispositivos modernos.

En esta lección, solo utilizamos los códigos Morse para las letras "S" y "O". Aquí tienes la tabla del código Morse con las 26 letras y los 10 números.

.. list-table::
    :widths: 8 8 8 8 8 8 8 8
    :header-rows: 1

    * - Letter
      - Code
      - Letter
      - Code
      - Letter
      - Code
      - Letter
      - Code
    * - A
      - \.-
      - B
      - \-...
      - C
      - \-.\-.
      - D
      - \-..
    * - E
      - \.
      - F
      - \..-.
      - G
      - \-\-.
      - H
      - \....
    * - I
      - \..
      - J
      - \.\-\-\-
      - K
      - \-.-
      - L
      - \.-..
    * - M
      - \--
      - N
      - \-.
      - O
      - \-\-\-
      - P
      - \.-\-.
    * - Q
      - \-\-.- 
      - R
      - \.-.
      - S
      - \...
      - T
      - \-
    * - U
      - \..-
      - V
      - \...-
      - W
      - \.-\-
      - X
      - \-..-
    * - Y
      - \-.-\-
      - Z
      - \-\-..
      - 1
      - \.\-\-\-\-
      - 2
      - \..\-\-\-
    * - 3
      - \...-\-
      - 4
      - \....-
      - 5
      - \.....
      - 6
      - \-....
    * - 7
      - \-\-...
      - 8
      - \-\-\-..
      - 9
      - \-\-\-\-.
      - 
      - 


**Pregunta**

Usando la tabla de código Morse proporcionada, escribe un código para enviar el mensaje "Hello".

