.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook. Sumérgete más en Raspberry Pi, Arduino y ESP32 junto a otros apasionados.

    **¿Por qué unirse?**

    - **Soporte de expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

18. Alarma de luz
========================

.. image:: img/18_light_alarm.png
    :width: 600
    :align: center

Imagina una escena sacada directamente de una película: En un museo tenuemente 
iluminado, un ladrón astuto se acerca sigilosamente a una pintura invaluable. 
Se mueve en silencio, intentando llevar a cabo su robo bajo la cobertura de la noche. 
Sin embargo, en el momento en que toca la pintura, una serie de sofisticados 
sensores se activan, desencadenando alarmas por toda la galería e iluminando 
instantáneamente el área circundante. El ladrón es rápidamente arrestado por 
el personal de seguridad en el lugar, evitando un posible robo de arte en el 
acto. Esto no es una película; es un ejemplo real de cómo la tecnología de 
sensores trabaja en los sistemas de seguridad modernos.

¿Cómo se logra esto? Esto implica colocar una fotorresistencia o un sensor de 
luz más sofisticado cerca del marco de la pintura. Cualquier intento de mover o 
bloquear la pintura altera las condiciones de luz, activando el sistema de alarma.

Ahora, vamos a construir un sistema simulado de alarma de luz utilizando una 
fotorresistencia y un zumbador, ¿de acuerdo?

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="../_static/video/18_light_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

En esta lección, aprenderás:

* Los principios de funcionamiento y características de una fotorresistencia.
* Cómo construir un simple sistema de alarma de luz.


Construyendo el circuito
---------------------------

**Componentes necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Fotorresistencia
     - 1 * Resistor de 10KΩ
     - 1 * Zumbador activo
   * - |list_uno_r3| 
     - |list_photoresistor| 
     - |list_10kohm| 
     - |list_active_buzzer| 
   * - 1 * Cable USB
     - 1 * Protoboard
     - Cables Jumper
     - 1 * Multímetro
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_meter|



**Paso a paso para construir**

1. Comienza con una fotorresistencia.

.. image:: img/17_photoresistor.png
    :width: 100
    :align: center

Una fotorresistencia o célula fotoeléctrica es un resistor variable controlado por la luz. La resistencia de una fotorresistencia disminuye con el aumento de la intensidad de la luz incidente; en otras palabras, exhibe fotoconductividad.

Las fotorresistencias pueden usarse como semiconductores resistivos en circuitos detectores sensibles a la luz y en circuitos de conmutación activados por la luz o la oscuridad. En la oscuridad, la resistencia de una fotorresistencia puede ser tan alta como varios megaohmios (MΩ), mientras que en condiciones de luz puede reducirse a unos pocos cientos de ohmios.

El kit incluye un resistor con una clasificación de 10K a 25°C. Ahora, usa un multímetro para medir la resistencia de la fotorresistencia bajo condiciones normales de luz, iluminada y en oscuridad.

2. Dado que la resistencia nominal de la fotorresistencia es de 10K, configura el multímetro para medir la resistencia en el rango de 20 kiloohmios (20K).

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

3. Inserta la fotorresistencia en el protoboard en las posiciones 10E y 11E. Los pines no tienen dirección, por lo que pueden insertarse libremente.

.. image:: img/17_light_alarm_photoresistor.png
    :width: 500
    :align: center

4. Ahora, toca los dos pines de la fotorresistencia con las puntas de prueba roja y negra del multímetro.

.. image:: img/17_light_alarm_test.png
    :width: 500
    :align: center

5. Lee el valor de la resistencia bajo la luz ambiental actual y regístralo en la tabla a continuación.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Entorno
     - Resistencia (kilohmios)
   * - Luz normal
     - *5.48*
   * - Luz brillante
     - 
   * - Oscuridad
     -

6. Ahora, pídele a un amigo que te ayude a iluminar directamente la fotorresistencia con una linterna u otra fuente de luz. Registra el valor de la resistencia, que podría ser solo unos pocos cientos de ohmios. Por lo tanto, puede que necesites configurar el multímetro en 2K o incluso en 200 ohmios para obtener una lectura más precisa.

.. note::

    Hemos establecido la unidad de resistencia en la tabla en kiloohmios. 1 kiloohmio (kΩ) = 1000 ohmios.

    Si seleccionaste el rango de 200 ohmios y obtuviste una lectura de 164.5 ohmios, conviértelo a 0.16 kiloohmios (redondeado a dos decimales) e introduce el valor convertido en la tabla.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Entorno
     - Resistencia (kilohmios)
   * - Luz normal
     - *≈5.48*
   * - Luz brillante
     - *≈0.16*
   * - Oscuridad
     - 

7. En condiciones de oscuridad, la resistencia de la fotorresistencia puede alcanzar varios megaohmios, por lo que necesitamos configurar el multímetro en la posición de 2 megaohmios.

.. image:: img/multimeter_2mΩ.png
    :width: 300
    :align: center

8. Cubre completamente la fotorresistencia con un objeto negro y luego registra la resistencia medida en la tabla.

.. note::
    Hemos configurado la unidad de resistencia en la tabla en kiloohmios. 1 megaohmio (MΩ) = 1000 kiloohmios.

    Si seleccionaste el rango de 2 megaohmios y obtuviste una lectura de 1.954 megaohmios, conviértelo a 1954 kiloohmios, que es el valor que debes introducir.

    Si la lectura es directamente superior a 2MΩ, mostrará "1.", en cuyo caso puedes ingresar directamente 2 megaohmios, o podrías considerar usar un multímetro más preciso para medir el valor exacto.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Entorno
     - Resistencia (kilohmios)
   * - Luz normal
     - *≈5.48*
   * - Luz brillante
     - *≈0.16*
   * - Oscuridad
     - *≈1954*

A partir de las mediciones, hemos confirmado las propiedades fotoconductivas de la fotorresistencia: cuanto más fuerte es la luz, menor es la resistencia; cuanto más tenue es la luz, mayor es la resistencia, llegando a varios megaohmios.

9. Continúa construyendo el circuito. Conecta un pin de la fotorresistencia al terminal negativo del protoboard y el otro pin al pin A0 del Arduino Uno R3.

.. image:: img/17_light_alarm_a0.png
    :width: 500
    :align: center

10. Inserta un resistor de 10K en la misma fila que la conexión de la fotorresistencia al A0.

.. image:: img/17_light_alarm_resistor.png
    :width: 500
    :align: center

En este circuito, el resistor de 10K y la fotorresistencia están conectados en serie, y la corriente que pasa a través de ellos es la misma. El resistor de 10K actúa como protección, y el pin A0 lee el valor después de la conversión de voltaje de la fotorresistencia.

Cuando la luz aumenta, la resistencia de la fotorresistencia disminuye, y su voltaje disminuye, por lo que el valor del pin A0 disminuirá; si la luz es lo suficientemente fuerte, la resistencia de la fotorresistencia se acercará a 0, y el valor del pin A0 será cercano a 0. En ese momento, el resistor de 10K desempeña un papel protector, evitando un cortocircuito al evitar que los 5V y GND se conecten directamente.

Si colocas la fotorresistencia en una situación oscura, el valor del pin A0 aumentará. En una situación lo suficientemente oscura, la resistencia de la fotorresistencia será infinita y su voltaje será cercano a 5V (el resistor de 10K se vuelve insignificante), y el valor del pin A0 será cercano a 1023.

11. Conecta el otro pin del resistor de 10K al pin de 5V en el Arduino Uno R3.

.. image:: img/17_light_alarm_5v.png
    :width: 500
    :align: center

12. A continuación, como en la lección anterior, inserta el zumbador activo en el protoboard, conectando su ánodo al pin 9 del R3 y su cátodo al terminal negativo del protoboard.

.. image:: img/17_light_alarm_buzzer.png
    :width: 500
    :align: center

13. Finalmente, conecta el terminal negativo del protoboard al pin GND en el Arduino Uno R3 con un cable jumper.

.. image:: img/17_light_alarm.png
    :width: 500
    :align: center

Creación del Código
---------------------------
1. Abre el Arduino IDE y comienza un nuevo proyecto seleccionando "Nuevo Sketch" en el menú "Archivo".
2. Guarda tu sketch como ``Lesson18_Light_Alarm`` usando ``Ctrl + S`` o haciendo clic en "Guardar".

3. Antes de la función ``void setup()``, crea constantes para la fotorresistencia y el zumbador, así como un valor de umbral constante que activará la alarma cuando la lectura de la fotorresistencia caiga por debajo de este valor.

.. code-block:: Arduino
    :emphasize-lines: 1,2,3

    const int sensorPin = A0;   // Asigna el pin A0 como constante para la fotorresistencia
    const int buzzerPin = 9;    // Asigna el pin 9 como constante para el zumbador
    const int threshold = 300;  // Establece el valor umbral

    void setup() {
        // coloca tu código de configuración aquí, para que se ejecute una vez:
    }

4. Además, crea una variable para almacenar el valor leído de la fotorresistencia.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int sensorPin = A0;   // Asigna el pin A0 como constante para la fotorresistencia
    const int buzzerPin = 9;    // Asigna el pin 9 como constante para el zumbador
    const int threshold = 300;  // Establece el valor umbral

    int sensorValue = 0;  // Para almacenar la lectura de la fotorresistencia

    void setup() {
        // coloca tu código de configuración aquí, para que se ejecute una vez:
    }

5. En la función ``void setup()``, configura el zumbador como salida e inicia la comunicación serial para monitorear las lecturas de la fotorresistencia.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void setup() {
        // coloca tu código de configuración aquí, para que se ejecute una vez:
        pinMode(buzzerPin, OUTPUT);  // Configura el pin del zumbador como salida
        Serial.begin(9600);          // Inicia la comunicación serial a 9600 baudios
    }

6. En la función ``void loop()``, utiliza la función ``analogRead()`` para leer la fotorresistencia y almacena el valor en la variable ``sensorValue``. Luego imprime este valor en el monitor serial. Recuerda establecer un intervalo de tiempo entre cada lectura.

.. code-block:: Arduino
    :emphasize-lines: 3,4,5

    void loop() {
        // coloca tu código principal aquí, para que se ejecute repetidamente:
        sensorValue = analogRead(sensorPin);  // Lee el valor analógico de la fotorresistencia
        Serial.println(sensorValue);          // Imprime la lectura de la fotorresistencia en el monitor serial
        delay(100); // Espera 0.1 segundos
    }

7. Cuando el entorno cambia de oscuro a brillante, la resistencia de la fotorresistencia disminuye, y también lo hace la lectura en el pin A0. Ahora usa una declaración ``if`` para verificar si el valor de la fotorresistencia está por debajo del ``threshold``; si lo está, activa el zumbador, de lo contrario, apágalo.

.. code-block:: Arduino
    :emphasize-lines: 7-12

    void loop() {
        // coloca tu código principal aquí, para que se ejecute repetidamente:
        sensorValue = analogRead(sensorPin);  // Lee el valor analógico de la fotorresistencia
        Serial.println(sensorValue);          // Imprime la lectura de la fotorresistencia en el monitor serial
        delay(100);                           // Espera 0.1 segundos

        // Verifica si la lectura está por debajo del umbral
        if (sensorValue < threshold) {
            digitalWrite(buzzerPin, HIGH);  // Si está por debajo del umbral, enciende el zumbador
        } else {
            digitalWrite(buzzerPin, LOW);  // Si no está por debajo del umbral, apaga el zumbador
        }
    }

8. Aquí tienes tu código completo. Ahora puedes hacer clic en "Subir" para cargar el código en el Arduino Uno R3.

.. code-block:: Arduino

    const int sensorPin = A0;   // Asigna el pin A0 como constante para la fotorresistencia
    const int buzzerPin = 9;    // Asigna el pin 9 como constante para el zumbador
    const int threshold = 300;  // Establece el valor umbral

    int sensorValue = 0;  // Para almacenar la lectura de la fotorresistencia

    void setup() {
        // coloca tu código de configuración aquí, para que se ejecute una vez:
        pinMode(buzzerPin, OUTPUT);  // Configura el pin del zumbador como salida
        Serial.begin(9600);          // Inicia la comunicación serial a 9600 baudios
    }

    void loop() {
        // coloca tu código principal aquí, para que se ejecute repetidamente:
        sensorValue = analogRead(sensorPin);  // Lee el valor analógico de la fotorresistencia
        Serial.println(sensorValue);          // Imprime la lectura de la fotorresistencia en el monitor serial
        delay(100);                           // Espera 0.1 segundos

        // Verifica si la lectura está por debajo del umbral
        if (sensorValue < threshold) {
            digitalWrite(buzzerPin, HIGH);  // Si está por debajo del umbral, enciende el zumbador
        } else {
            digitalWrite(buzzerPin, LOW);  // Si no está por debajo del umbral, apaga el zumbador
        }
    }

9. Finalmente, recuerda guardar tu código y organizar tu espacio de trabajo.


**Pregunta**

Ladrones astutos podrían elegir robar por la noche, y si una pintura desaparece, 
la fotorresistencia podría no detectar ningún cambio de luz, lo que impediría que 
se active la alarma. ¿Qué se podría hacer para mejorar este fallo?
