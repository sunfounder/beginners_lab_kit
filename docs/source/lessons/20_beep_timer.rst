.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder para Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.


20. El Temporizador Pomodoro
===========================================

En esta lección, exploraremos la intersección entre la gestión del tiempo y la tecnología creando un Temporizador Pomodoro con un Arduino y un zumbador activo. Aprenderás a utilizar las capacidades de temporización interna del Arduino para construir un temporizador que segmenta el trabajo en intervalos de enfoque de 25 minutos seguidos de descansos de 5 minutos. Este método, conocido como la Técnica Pomodoro, mejora la productividad y la concentración. A lo largo del curso, obtendrás una base sólida en temporización electrónica y experiencia práctica en programación y ensamblaje de circuitos, culminando en la creación de un temporizador Pomodoro funcional. ¡Únete para dominar tu tiempo y aumentar la eficiencia en tus actividades diarias!

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="../_static/video/20_beep_timer.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Al final de esta lección, serás capaz de:

* Comprender la importancia histórica del sonido en la medición del tiempo.
* Identificar los componentes necesarios para construir un circuito de temporizador electrónico.
* Programar un Arduino para controlar un zumbador en la gestión del tiempo utilizando las funciones ``delay()`` y ``millis()``.
* Aplicar la Técnica Pomodoro en un contexto práctico creando un temporizador que alterna entre periodos de trabajo y descanso.


Relojes y Sonido
--------------------

En el mundo antiguo, se usaban campanadas a gran escala para marcar el paso del tiempo y eventos sociales específicos.
Por ejemplo, en las ciudades europeas medievales, las campanas de las iglesias marcaban los horarios de oración y el inicio y fin de las jornadas laborales.
Estas campanadas no solo marcaban el tiempo; también servían como herramientas para el orden social, en torno al cual giraba la vida cotidiana de la comunidad.

**Relojes mecánicos y sonido**

.. image:: img/7_big_ben.png
  :width: 500
  :align: center

Con el desarrollo de los relojes mecánicos, especialmente con el diseño del Big Ben, los relojes comenzaron a equiparse con campanas más complejas y mecanismos de cronometraje.
El sonido del Big Ben se transmite por sus grandes campanas de bronce, mejorando tanto el alcance del sonido como la precisión de los anuncios de tiempo.
En muchas ciudades, el sonido del Big Ben se convirtió en una referencia para que los residentes ajustaran sus actividades diarias, desempeñando un papel crucial en la programación más precisa del tiempo para la navegación,
horarios de trenes y más.

**Cronometraje sonoro en la era electrónica**

.. image:: img/19_timer.jpg
  :width: 500
  :align: center

Con la llegada de la era electrónica, los temporizadores sonoros evolucionaron nuevamente. La introducción de zumbadores electrónicos, especialmente con la ayuda de microcontroladores como Arduino,
permitió que la medición del tiempo se independizara de los grandes dispositivos mecánicos. Estos pequeños dispositivos pueden producir sonidos de diferentes frecuencias y tonos,
que se pueden utilizar para diversas aplicaciones de temporización, desde simples temporizadores de cocina hasta sistemas de control de procesos industriales complejos.
Ejemplos de esto incluyen los sistemas de llamadas de enfermería en hospitales modernos, las campanas de clase en las escuelas y los recordatorios en dispositivos electrónicos personales, todos utilizando zumbadores electrónicos para la gestión del tiempo.


Construcción del Circuito
------------------------------

**Componentes necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Protoboard
     - 1 * Zumbador Activo
     - Cables Jumper
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_active_buzzer| 
     - |list_wire| 
   * - 1 * Cable USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 

**Construcción paso a paso**

Esta lección utiliza el mismo circuito que la Lección 17.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Creación de código - Tick Tick
----------------------------------

En Arduino, ``delay()`` es la función de temporización más simple y comúnmente utilizada.
A menudo la usamos para pausar el programa por un tiempo corto, lo que, combinado con bucles, puede crear un efecto de parpadeo en un LED. Aquí, utilizamos la función ``delay()`` para hacer que el zumbador suene una vez cada segundo.

1. Abre el IDE de Arduino y comienza un nuevo proyecto seleccionando “Nuevo Boceto” desde el menú “Archivo”.
2. Guarda tu boceto como ``Lesson20_Timer_Tick_Tick`` usando ``Ctrl + S`` o haciendo clic en “Guardar”.

3. Escribe el código como sigue:

.. code-block:: Arduino

  const int buzzerPin = 9;   // Asigna el pin 9 a la constante para el zumbador  
  
  void setup() {
    // Configura tu código aquí para que se ejecute una vez:
    pinMode(buzzerPin, OUTPUT);  // Establece el pin 9 como salida
  } 

  void loop() {
    // El código principal aquí, para ejecutar repetidamente:
    digitalWrite(buzzerPin, HIGH);  // Encender el zumbador
    delay(100);                     // Duración del pitido: 100 milisegundos
    digitalWrite(buzzerPin, LOW);   // Apagar el zumbador
    delay(1000);                    // Intervalo entre señales: 1000 milisegundos
  }

En esta configuración, la primera función ``delay()`` pausa el Arduino Uno R3 durante 100 milisegundos, durante los cuales el zumbador continúa sonando. La segunda función ``delay()`` pausa el Arduino durante 1000 milisegundos (1 segundo), durante los cuales el zumbador permanece en silencio.

4. Después de cargar el código en el Arduino Uno R3, escucharás que el zumbador emite un pitido una vez por segundo.

Creación de código - ``millis()``
-------------------------------------

Usar ``delay()`` pausa tu código, lo cual puede ser inconveniente.

Por ejemplo, imagina que calientas una pizza en el microondas mientras esperas correos electrónicos importantes.
Colocas la pizza en el microondas y la programas por 10 minutos. La analogía con usar ``delay()`` es sentarse frente al microondas, viendo cómo la cuenta regresiva baja de 10 minutos a cero. Si recibes un correo electrónico importante durante este tiempo, lo perderías.

Lo que normalmente haces es colocar la pizza en el microondas, luego revisas tus correos electrónicos, quizás incluso haces otra cosa, y periódicamente vuelves para ver si el temporizador llegó a cero, indicando que tu pizza está lista.

Arduino también tiene una herramienta de temporización que no pausa el programa, que es ``millis()``.

``millis()`` es una función muy importante en la programación de Arduino. Devuelve el número de milisegundos que han pasado desde que la placa de Arduino fue encendida o reiniciada.

  * ``time = millis()``: Devuelve el número de milisegundos que han pasado desde que la placa Arduino comenzó a ejecutar el programa actual. Este número se desbordará (volverá a cero) después de aproximadamente 50 días.

  **Parámetros**
    Ninguno

  **Devuelve**
    Número de milisegundos que han pasado desde que comenzó el programa. Tipo de dato: unsigned long.

Aquí, de manera similar, hacemos que el zumbador emita un pitido una vez cada segundo.

1. Abre el IDE de Arduino y comienza un nuevo proyecto seleccionando “Nuevo Boceto” desde el menú “Archivo”.
2. Guarda tu boceto como ``Lesson20_Timer_Millis`` usando ``Ctrl + S`` o haciendo clic en “Guardar”.

3. Primero, crea una constante llamada ``buzzerPin`` y asígnale el valor del pin 9.

.. code-block:: Arduino
  :emphasize-lines: 1

  const int buzzerPin = 9;   // Asigna el pin 9 a la constante para el zumbador

  void setup() {
    // Configura tu código aquí para que se ejecute una vez:
  }

4. Crea dos variables de tipo long, ``previousMillis`` almacenará la marca de tiempo de la última vez que sonó el zumbador, y ``interval`` establece con qué frecuencia suena el zumbador, en milisegundos. Aquí, se configura para que suene cada 1000 milisegundos (o cada segundo).

.. code-block:: Arduino
  :emphasize-lines: 3,4

  const int buzzerPin = 9;  // Asigna el pin 9 a la constante para el zumbador

  unsigned long previousMillis = 0;  // Almacena la marca de tiempo de la última vez que sonó el zumbador
  long interval = 1000;              // Intervalo en el que suena (milisegundos)


5. En la función ``void setup()``, configura el pin del zumbador como modo de salida.

.. code-block:: Arduino
  :emphasize-lines: 8

  const int buzzerPin = 9;  // Asigna el pin 9 a la constante para el zumbador

  unsigned long previousMillis = 0;  // Almacena la marca de tiempo de la última vez que sonó el zumbador
  long interval = 1000;              // Intervalo en el que suena (milisegundos)

  void setup() {
    // Configura tu código aquí para que se ejecute una vez:
    pinMode(buzzerPin, OUTPUT);  // Establece el pin 9 como salida
  }

6. En la función ``void loop()`` crea una variable de tipo ``unsigned long`` llamada ``currentMillis`` para almacenar el tiempo actual.

.. code-block:: Arduino
  :emphasize-lines: 3

  void loop() {
    // El código principal aquí, para ejecutar repetidamente:
    unsigned long currentMillis = millis();
  }

7. Cuando el tiempo actual menos el último tiempo actualizado exceda los 1000 ms, se activarán algunas funciones. Además, actualiza el valor de ``previousMillis`` al tiempo actual, para que la próxima activación ocurra en 1 segundo.

.. code-block:: Arduino
  :emphasize-lines: 5,6

  void loop() {
    // El código principal aquí, para ejecutar repetidamente:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Guarda la última vez que sonó el zumbador
    }
  }

8. Agrega las funciones principales que necesitan ejecutarse periódicamente. En este caso, hacer que el zumbador suene.

.. code-block:: Arduino
  :emphasize-lines: 7,8,9

  void loop() {
    // El código principal aquí, para ejecutar repetidamente:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Guarda la última vez que sonó el zumbador
      digitalWrite(buzzerPin, HIGH);   // Emitir sonido
      delay(100);
      digitalWrite(buzzerPin, LOW);    // Silenciar
    }
  }

9. Tu código completo debería verse así. Cárgalo en el Arduino Uno R3 y notarás que el zumbador emite un pitido una vez cada segundo.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Asigna el pin 9 a la constante para el zumbador

  unsigned long previousMillis = 0;  // Almacena la marca de tiempo de la última vez que sonó el zumbador
  long interval = 1000;              // Intervalo en el que suena (milisegundos)

  void setup() {
    // Configura tu código aquí para que se ejecute una vez:
    pinMode(buzzerPin, OUTPUT);  // Establece el pin 9 como salida
  }

  void loop() {
    // El código principal aquí, para ejecutar repetidamente:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Guarda la última vez que sonó el zumbador
      digitalWrite(buzzerPin, HIGH);   // Hacer sonido
      delay(100);
      digitalWrite(buzzerPin, LOW);    // Silencio
    }
  }

**Pregunta**

Si se cambia el ``delay(100);`` a ``delay(1000);``, ¿qué sucederá con el programa? ¿Por qué?


Creación de código - Temporizador Pomodoro
-----------------------------------------------

La Técnica Pomodoro, también conocida como la Técnica del Tomate, es un método de gestión del tiempo desarrollado por Francesco Cirillo a finales de los años 80.
Este método utiliza un temporizador para dividir el trabajo en intervalos de 25 minutos, seguidos de descansos breves.
Cada intervalo de trabajo se llama "pomodoro", en honor al temporizador de cocina en forma de tomate que Cirillo utilizó durante sus años de universidad.

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

Los pasos básicos de la Técnica Pomodoro incluyen:

1. **Definir la tarea**: Decide la tarea que necesitas completar antes de comenzar.
2. **Configurar el temporizador Pomodoro**: Configura un temporizador para 25 minutos de tiempo de trabajo.
3. **Trabajar intensamente**: Concéntrate completamente en la tarea durante esos 25 minutos, evitando cualquier forma de distracción.
4. **Tomar un descanso breve**: Una vez que el tiempo de trabajo haya terminado, toma un descanso de 5 minutos. Durante este tiempo, puedes caminar, estirarte, beber agua, etc., pero evita actividades relacionadas con el trabajo.

Los beneficios de la Técnica Pomodoro incluyen una mayor concentración, reducción de la fatiga, clara delimitación de los tiempos de trabajo y descanso, ayudando a gestionar distracciones, y una mayor motivación y satisfacción por completar tareas. Además, la Técnica Pomodoro no requiere herramientas o tecnología compleja: un temporizador simple es suficiente.

A continuación, programaremos un temporizador que emitirá un sonido cada 25 minutos para señalar el final de un período de trabajo, seguido de un recordatorio para un descanso de 5 minutos:

1. Abre el IDE de Arduino y comienza un nuevo proyecto seleccionando “Nuevo Boceto” desde el menú “Archivo”.
2. Guarda tu boceto como ``Lesson20_Timer_Millis_Pomodoro`` usando ``Ctrl + S`` o haciendo clic en “Guardar”.

3. Define algunas constantes y variables antes de ``void setup()``.

* ``buzzerPin`` identifica a qué pin está conectado el zumbador.
* ``startMillis`` lleva el registro de cuándo empezó el temporizador.
* ``workPeriod`` y ``breakPeriod`` definen cuánto dura cada período.
* ``isWorkPeriod`` es una variable booleana que se usa para rastrear si es hora de trabajar o tomar un descanso.

.. code-block:: Arduino

  const int buzzerPin = 9;          // Asigna el pin 9 a la constante para el zumbador
  unsigned long startMillis;        // Almacena el tiempo cuando empieza el temporizador
  const long workPeriod = 1500000;  // Período de trabajo de 25 minutos
  const long breakPeriod = 300000;  // Período de descanso de 5 minutos
  static bool isWorkPeriod = true;  // Rastrear si es un período de trabajo o descanso


4. Inicializa el pin del zumbador como una salida y comienza el temporizador registrando el tiempo de inicio con ``millis()``.

.. code-block:: Arduino
  :emphasize-lines: 2,3
  
  void setup() {
    pinMode(buzzerPin, OUTPUT); // Inicializa el pin del zumbador como una salida
    startMillis = millis(); // Registra el tiempo de inicio
  }

5. En la función ``void loop()``, crea una variable ``unsigned long`` llamada ``currentMillis`` para almacenar el tiempo actual.

.. code-block:: Arduino
  :emphasize-lines: 2

  void loop() {
    unsigned long currentMillis = millis(); // Actualiza el tiempo actual
  }


6. Usa las declaraciones condicionales ``if else if`` para determinar si es un período de trabajo.

.. code-block:: Arduino
  :emphasize-lines: 4-6

  void loop() {
    unsigned long currentMillis = millis(); // Actualiza el tiempo actual

    if (isWorkPeriod){ 
    } else if (!isWorkPeriod){
    }
  }

7. Si lo es, verifica si el tiempo actual ha excedido el ``workPeriod``. Si es así, reinicia el temporizador, cambia al período de descanso y activa el zumbador para que suene dos veces por una duración prolongada.

.. code-block:: Arduino
  :emphasize-lines: 5-16

  void loop() {
    unsigned long currentMillis = millis();  // Actualiza el tiempo actual

    if (isWorkPeriod) {
      if (currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis;  // Reinicia el temporizador
        isWorkPeriod = false;         // Cambia al período de descanso
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(500);                     // Zumbador encendido por 500 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(200);                     // Zumbador apagado por 200 milisegundos
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(500);                     // Zumbador encendido por 500 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(200);                     // Zumbador apagado por 200 milisegundos
      }
    } else if (!isWorkPeriod) {
    }
  }

8. Usa las declaraciones condicionales ``else if`` para determinar si es un período de descanso y verifica de manera similar si el tiempo actual ha excedido el ``breakPeriod``. Si es así, reinicia el temporizador, cambia nuevamente al período de trabajo y activa el zumbador para que suene brevemente dos veces.

.. code-block:: Arduino

  } else if (!isWorkPeriod) {
    if (currentMillis - startMillis >= breakPeriod) {
      startMillis = currentMillis;  // Reinicia el temporizador
      isWorkPeriod = true;          // Cambia al período de trabajo
      digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
      delay(200);                     // Zumbador encendido por 200 milisegundos
      digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
      delay(200);                     // Zumbador apagado por 200 milisegundos
      digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
      delay(200);                     // Zumbador encendido por 200 milisegundos
      digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
      delay(200);                     // Zumbador apagado por 200 milisegundos
    }
  }


9. Tu código completo debería verse así, y puedes cargarlo en el Arduino Uno R3 para ver los efectos.

.. note::

  Si encuentras que esperar 25 minutos para un período de trabajo y 5 minutos para un descanso es demasiado largo durante la depuración, 
  puedes acortar ``workPeriod`` a 15000 milisegundos y ``breakPeriod`` a 3000 milisegundos. Entonces escucharás el zumbador sonar dos veces largo cada 15 segundos, seguido de un zumbido corto dos veces después de 3 segundos.


.. code-block:: Arduino

  const int buzzerPin = 9;          // Asigna el pin 9 a la constante para el zumbador
  unsigned long startMillis;        // Almacena el tiempo cuando comienza el temporizador
  const long workPeriod = 1500000;  // Período de trabajo de 25 minutos
  const long breakPeriod = 300000;  // Período de descanso de 5 minutos
  static bool isWorkPeriod = true;  // Rastrea si es un período de trabajo o descanso

  void setup() {
    pinMode(buzzerPin, OUTPUT); // Inicializa el pin del zumbador como salida
    startMillis = millis(); // Registra el tiempo de inicio
  }

  void loop() {
    unsigned long currentMillis = millis(); // Actualiza el tiempo actual

    if (isWorkPeriod){ 
      if(currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis; // Reinicia el temporizador
        isWorkPeriod = false; // Cambia al período de descanso
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(500);                     // Zumbador encendido por 500 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(200);                     // Zumbador apagado por 200 milisegundos
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(500);                     // Zumbador encendido por 500 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(200);                     // Zumbador apagado por 200 milisegundos
      }
    } else if (!isWorkPeriod) 
      if(currentMillis - startMillis >= breakPeriod) {
        startMillis = currentMillis; // Reinicia el temporizador
        isWorkPeriod = true; // Cambia al período de trabajo
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(200);                     // Zumbador encendido por 200 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(200);                     // Zumbador apagado por 200 milisegundos
        digitalWrite(buzzerPin, HIGH);  // Enciende el zumbador
        delay(200);                     // Zumbador encendido por 200 milisegundos
        digitalWrite(buzzerPin, LOW);   // Apaga el zumbador
        delay(200);                     // Zumbador apagado por 200 milisegundos
      }
    }
  }

10. Finalmente, recuerda guardar tu código y organizar tu área de trabajo.

**Pregunta**

Piensa en otros lugares en tu vida donde puedas "escuchar" el tiempo. ¡Haz una lista de algunos ejemplos y anótalos en tu cuaderno!


**Resumen**

En la clase de hoy, construimos con éxito una versión electrónica del temporizador Pomodoro, una herramienta invaluable para mejorar la productividad mediante períodos de trabajo y descanso estructurados. A través de este proyecto, los estudiantes aprendieron sobre la utilidad de los zumbadores en la gestión del tiempo y la aplicación práctica de la función ``millis()`` para crear un código de temporizador no bloqueante en Arduino. Este enfoque permite la multitarea en aplicaciones de microcontroladores, imitando sistemas más complejos en tecnología e industria.

