.. note::

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Accede antes que nadie a los anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

19. Sistema de Alarma de Estacionamiento en Reversa
=======================================================

.. image:: img/19_packing.png
    :width: 600
    :align: center

Al retroceder un automóvil, es crucial estar al tanto de los obstáculos detrás del vehículo, especialmente en situaciones con visibilidad limitada. 
Para mejorar la seguridad, muchos vehículos modernos están equipados con sistemas de advertencia de reversa. 

En este proyecto, utilizaremos un Arduino, un sensor ultrasónico y un zumbador activo para simular dicho sistema. 
El sensor ultrasónico ayuda a detectar la distancia a los obstáculos detrás del vehículo, y cuando esta distancia es demasiado corta, el zumbador activo emitirá una alerta para advertir al conductor. 

Este proyecto no solo nos permitirá comprender mejor cómo funcionan los sensores ultrasónicos, sino que también nos enseñará a programar y controlar un Arduino para implementar una función práctica de advertencia de reversa.

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="../_static/video/19_reverse_parking_system.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
  

**Módulo Ultrasónico**


Imagina que estás en una habitación oscura y no puedes ver los objetos a tu alrededor. En esta situación, podrías aplaudir para producir un sonido que se propaga hacia afuera. Cuando este sonido choca con una pared u otro objeto, regresa como un eco. Si escuchas con atención, puedes oír ese eco. Calculando el tiempo que tarda en viajar el sonido y regresar el eco, puedes estimar aproximadamente a qué distancia está la pared u objeto. Los sensores ultrasónicos funcionan de manera similar para "ver" el mundo a su alrededor.

.. image:: img/19_ultrasonic_pic.png
    :width: 400
    :align: center

Los sensores ultrasónicos consisten principalmente en dos partes: un transmisor y un receptor, muy parecidos a tu boca y tus oídos.

1. Emisión de ondas sonoras:

Cuando el sensor ultrasónico se activa, el transmisor emite una serie de ondas sonoras rápidas, similar a cuando aplaudes. Estas ondas tienen una frecuencia tan alta que nuestros oídos no las pueden escuchar.

2. Viaje y regreso del sonido:

Las ondas sonoras se propagan hacia adelante hasta que golpean algo como una pared o una mesa, y luego rebotan.

3. Recepción de las ondas sonoras:

La parte receptora del sensor ultrasónico se encarga de "escuchar" estos ecos, de la misma manera que tus oídos captan las ondas sonoras reflejadas de los objetos.

4. Cálculo de la distancia:

El sensor registra el tiempo que tardan las ondas sonoras en ir y volver. 
Dado que la velocidad del sonido es conocida (aproximadamente 340 metros por segundo en el aire), 
multiplicar este tiempo por la velocidad del sonido te da la distancia total que recorrieron las ondas. 
Como solo necesitamos la distancia de ida hasta el objeto, 
dividimos la distancia total entre 2 para obtener el resultado final.
Esta tecnología hace que los sensores ultrasónicos sean muy útiles en muchas situaciones, 
como ayudar a los robots a evitar obstáculos o asistir a los conductores indicando la distancia a los objetos cuando retroceden.

.. image:: img/19_ultrasonic_ms.png
    :width: 500
    :align: center


**Sincronización Ultrasónica**

El diagrama de sincronización se muestra a continuación. 
Solo necesitas suministrar un pulso corto de 10us en la entrada del trigger para iniciar la medición, 
y luego el módulo emitirá una ráfaga de 8 ciclos de ultrasonido a 40 kHz y activará su eco. 
Puedes calcular la distancia a través del intervalo de tiempo entre el envío de la señal de trigger y la recepción de la señal de eco.

Fórmula: us / 58 = centímetros o us / 148 = pulgadas; o: el rango = tiempo de nivel alto * velocidad (340M/S) / 2; 
se sugiere usar un ciclo de medición superior a 60ms para evitar colisiones de señal entre la señal de trigger y la señal de eco.

.. image:: img/19_ultrasonic_timing.png
    :width: 600
    :align: center


Construcción del Circuito
----------------------------

**Componentes Necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Módulo Ultrasónico
     - 1 * Zumbador Activo
     - Cables Jumper
   * - |list_uno_r3| 
     - |list_ultrasonic| 
     - |list_active_buzzer| 
     - |list_wire| 
   * - 1 * Cable USB
     - 1 * Protoboard
     - 1 * Multímetro
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter| 
     - 

**Construcción paso a paso**

Sigue el diagrama de cableado o los pasos a continuación para construir tu circuito.

.. image:: img/19_reversing_aid_bb.png
    :width: 600
    :align: center


Creación de código
----------------------

1. Abre el IDE de Arduino y comienza un nuevo proyecto seleccionando "Nuevo Sketch" en el menú "Archivo".
2. Guarda tu sketch como ``Lesson19_reversin_alarm`` usando ``Ctrl + S`` o haciendo clic en "Guardar".

3. Primero, necesitamos definir los pines en el Arduino que están conectados al sensor ultrasónico y al zumbador. Este paso es crucial ya que establece la base para la interfaz de hardware.

* **TRIGGER_PIN** y **ECHO_PIN** se usan para activar y recibir los ecos del sensor ultrasónico.
* **BUZZER_PIN** es el pin conectado al zumbador.

.. code-block:: Arduino

  #define TRIGGER_PIN  10
  #define ECHO_PIN     9
  #define BUZZER_PIN   2


4. En la función setup(), configuramos el modo para cada pin. El pin Trig debe configurarse como salida (ya que envía la señal), el pin Echo se configura como entrada (ya que recibe la señal) y el pin del zumbador también se configura como salida (ya que debe emitir sonido).

.. code-block:: Arduino

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);
    pinMode(ECHO_PIN, INPUT);
    pinMode(BUZZER_PIN, OUTPUT);
    Serial.begin(9600); // Start serial communication for debugging and distance viewing
  }

5. Escribiendo la función measureDistance():

La función measureDistance() encapsula la lógica necesaria para activar el sensor ultrasónico y leer la distancia basada en el eco recibido:

a. Activación del pulso ultrasónico

  * Establece el TRIGGER_PIN en bajo inicialmente para asegurar un pulso limpio.
  * Un pequeño retraso de 2 microsegundos asegura que la línea esté libre.
  * Envía un pulso alto de 10 microsegundos al TRIGGER_PIN. Este pulso indica al sensor que emita una onda de sonido ultrasónica.
  * Vuelve a establecer el TRIGGER_PIN en bajo para finalizar el pulso.

  .. code-block:: Arduino

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Asegurar que el pin Trig esté bajo antes del pulso
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Enviar un pulso alto
      delayMicroseconds(10);           // Duración del pulso de 10 microsegundos
      digitalWrite(TRIGGER_PIN, LOW);  // Finalizar el pulso alto
    }

.. note::

  En lecciones anteriores, trabajamos con tipos de variables ``int`` y ``float`` o constantes. Ahora, entendamos qué son las variables de tipo long y unsigned long:

  * ``long``: Un entero ``long`` es una versión extendida de un ``int``. Se utiliza para almacenar valores enteros más grandes que superan la capacidad de un ``int`` estándar. Un long típicamente ocupa 32 o 64 bits de memoria, lo que le permite almacenar valores mucho más grandes, tanto positivos como negativos.
  * ``unsigned long``: Un ``unsigned long`` es similar a un ``long`` pero solo puede representar valores no negativos. Usa el bit normalmente reservado para el signo para extender el rango de valores posibles que puede almacenar, pero estrictamente en el espectro positivo.


b. Lectura del eco

  * La función pulseIn() se usa en el ECHO_PIN para medir la duración del pulso entrante. Esta función espera que el pin pase a HIGH, mide cuánto tiempo permanece en HIGH y luego devuelve la duración en microsegundos.
  * Esta duración es el tiempo que tarda el pulso ultrasónico en viajar al objeto y regresar.

  .. code-block:: Arduino
    :emphasize-lines: 7

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Asegurar que el pin Trig esté bajo antes del pulso
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Enviar un pulso alto
      delayMicroseconds(10);           // Duración del pulso de 10 microsegundos
      digitalWrite(TRIGGER_PIN, LOW);  // Finalizar el pulso alto
      long duration = pulseIn(ECHO_PIN, HIGH);  // Medir la duración del nivel alto en el pin Echo
    }

c. Calculando la distancia

  * Aquí se usa la velocidad del sonido en el aire (aproximadamente 340 m/s). La fórmula para calcular la distancia es (duración * velocidad del sonido) / 2. Dividimos entre 2 porque la onda sonora viaja hasta el objeto y regresa, por lo que solo necesitamos la mitad de la distancia para una medición de ida.
  * En nuestro código, se utiliza 0.034 cm/us (velocidad del sonido en cm/microsegundos) como factor de conversión.

  .. code-block:: Arduino
    :emphasize-lines: 8,9

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Asegurar que el pin Trig esté en bajo antes del pulso
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Enviar un pulso alto
      delayMicroseconds(10);           // Duración del pulso de 10 microsegundos
      digitalWrite(TRIGGER_PIN, LOW);  // Finalizar el pulso alto
      long duration = pulseIn(ECHO_PIN, HIGH);  // Medir la duración del nivel alto en el pin Echo
      long distance = duration * 0.034 / 2;     // Calcular la distancia (en cm)
      return distance;
    }


6. Implementa el Bucle Principal

En la función loop(), se mide la distancia frecuentemente usando la función measureDistance(). 
Se toman decisiones basadas en esta distancia, como si se debe activar el zumbador.

.. code-block:: Arduino

  void loop() {
    long distance = measureDistance(); // Medir distancia
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance > 0 && distance <= 50) {
      digitalWrite(BUZZER_PIN, HIGH);  // Activar el zumbador si está cerca
      delay(100);                      // El zumbador suena durante 100 milisegundos
      digitalWrite(BUZZER_PIN, LOW);   // Apagar el zumbador
    } else {
      digitalWrite(BUZZER_PIN, LOW);   // Mantener el zumbador apagado
    }

    delay(100);  // Retardo entre mediciones para evitar sobrecarga del sensor
  }


7. Aquí tienes tu código completo. Ahora puedes hacer clic en "Subir" para cargar el código en el Arduino Uno R3.

.. code-block:: Arduino

  #define TRIGGER_PIN  10
  #define ECHO_PIN     9
  #define BUZZER_PIN   2

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Configurar el pin Trig como salida
    pinMode(ECHO_PIN, INPUT);      // Configurar el pin Echo como entrada
    pinMode(BUZZER_PIN, OUTPUT);   // Configurar el pin del zumbador como salida
    Serial.begin(9600);            // Iniciar comunicación serial para depuración
  }

  void loop() {
    long distance = measureDistance(); // Llamar a la función para medir la distancia
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance > 0 && distance <= 50) { // Si la distancia está dentro de los 50 cm
      digitalWrite(BUZZER_PIN, HIGH);     // Encender el zumbador
      delay(100);                         // El zumbador suena durante 100 milisegundos
      digitalWrite(BUZZER_PIN, LOW);      // Apagar el zumbador
    } else {
      digitalWrite(BUZZER_PIN, LOW);      // Mantener el zumbador apagado
    }

    delay(100);  // Retardo entre mediciones
  }

  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Asegurar que el pin Trig esté en bajo antes del pulso
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH); // Enviar un pulso alto
    delayMicroseconds(10);           // Duración del pulso de 10 microsegundos
    digitalWrite(TRIGGER_PIN, LOW);  // Finalizar el pulso alto

    long duration = pulseIn(ECHO_PIN, HIGH);  // Medir la duración del nivel alto en el pin Echo
    long distance = duration * 0.034 / 2;     // Calcular la distancia (en cm)
    return distance;
  }

8. Finalmente, recuerda guardar tu código y organizar tu área de trabajo.


**Pregunta**

Si deseas que la distancia detectada por este dispositivo sea más precisa con decimales, ¿cómo deberías modificar el código?

