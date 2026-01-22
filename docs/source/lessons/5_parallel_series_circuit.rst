.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones durante días festivos.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!


5. Circuito en Serie vs. Circuito en Paralelo
================================================

En esta lección, te adentrarás en la construcción y análisis de circuitos en serie y en paralelo, aprendiendo a medir y comprender cómo se comporta el voltaje en diferentes configuraciones de circuitos. Utilizando un multímetro, medirás el voltaje y la resistencia de los circuitos que construyas, obteniendo valiosos conocimientos prácticos sobre la dinámica de los circuitos.

En esta emocionante lección, aprenderás a:

* Relacionar diagramas esquemáticos con circuitos reales.
* Utilizar un multímetro para medir resistencia y voltaje.
* Construir circuitos en serie y en paralelo utilizando una placa de pruebas.
* Comparar el comportamiento del voltaje en circuitos en serie y en paralelo.

Estos objetivos te permitirán cerrar la brecha entre el conocimiento teórico y la aplicación práctica, enriqueciendo tu comprensión de la electrónica a través de experiencias prácticas.


Circuito en Serie vs. Circuito en Paralelo
----------------------------------------------

En nuestras lecciones anteriores, construimos con éxito un circuito simple con un Arduino Uno R3, una resistencia y un LED. La corriente en esta configuración fluye en serie: desde el Pin 13 de la placa, a través del LED, luego a través de la resistencia y de regreso al pin GND. Este es un ejemplo sencillo de un circuito en serie.

Pero a medida que nos adentramos más en el mundo de la electrónica, nos encontramos con circuitos más complejos, que comprenden componentes dispuestos en serie o en paralelo. Para comprender estas disposiciones y sus implicaciones en la corriente y el voltaje, debemos familiarizarnos con los diagramas de circuitos, también conocidos como diagramas esquemáticos.

**Diagramas de Conexión vs. Diagramas Esquemáticos**

Hemos estado utilizando diagramas de conexión, que son representaciones pictóricas que imitan la disposición física de los componentes del circuito. Estos diagramas son intuitivos y útiles para fines de ensamblaje:

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

Sin embargo, para comprender la funcionalidad y la lógica de diseño de un circuito, los diagramas esquemáticos son indispensables. Estos diagramas simplifican los circuitos hasta su esencia, utilizando símbolos estandarizados para representar cada componente. Revelan las relaciones eléctricas entre los componentes sin el desorden de las conexiones físicas.

Aquí están los símbolos de un LED, una resistencia y una batería que encontrarás con frecuencia en los esquemas:

.. image:: img/5_led_resistor_symbol.png
  :align: center

Un diagrama esquemático basado en nuestro cableado anterior se vería así, con todo el Arduino Uno R3 actuando como una batería que alimenta el circuito. A partir de este esquema, puedes visualizar claramente el flujo y la dirección de la corriente, lo que simplifica la complejidad de las conexiones físicas.

.. image:: img/5_serial_circuit_1led.png
  :align: center

**Configuraciones en Serie vs. Configuraciones en Paralelo**

En un circuito en serie, los componentes están alineados en una fila, por lo que la corriente tiene un único camino para seguir. Si un componente falla, se interrumpe todo el circuito, como ocurre con las luces navideñas antiguas, donde una bombilla quemada oscurecía toda la cadena.

.. image:: img/5_serial_circuit_2led.png
  :align: center

En un circuito en paralelo, en cambio, la corriente se divide en varios caminos. Cada componente funciona de manera independiente, por lo que si un camino se interrumpe, los demás continúan funcionando. Piensa en el sistema eléctrico de tu hogar: si apagas una luz, el televisor sigue encendido.

.. image:: img/5_parallel_circuit.png
  :align: center


Adentrándonos en los Circuitos en Serie
-------------------------------------------

Basándonos en nuestra comprensión de las diferencias entre circuitos en serie y en paralelo, esta actividad se centra en la construcción de un circuito en serie con múltiples LEDs. Recuerda que en un circuito en serie, la corriente eléctrica fluye a través de un solo camino. Exploremos las características únicas de los circuitos en serie a través de este ejercicio práctico.

**Componentes Necesarios**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 3 * LEDs rojos
     - 3 * Resistencias de 220Ω
     - Cables de conexión
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Cable USB
     - 1 * Placa de pruebas
     - 1 * Multímetro
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter| 
     - 

**Construcción del Circuito**

1. Ajusta el circuito anterior del LED eliminando el cable de conexión entre 1J y el lado positivo de la placa de pruebas a la derecha. Luego, toma otro LED rojo e inserta su cátodo (la pata más corta) en 1J y el ánodo en el lado positivo de la placa de pruebas, para que puedas conectar en serie otro LED al circuito.

.. image:: img/5_serial_circuit.png

Ahora tienes un circuito en serie con dos LEDs. Sigue el recorrido de la corriente a través del circuito:

* La corriente fluye desde 5V en el Arduino Uno R3, a través de un cable largo hacia el terminal positivo de la placa de pruebas.
* Luego, la corriente fluye a través del primer LED, que se enciende debido al flujo de corriente.
* La corriente luego fluye a través de los clips metálicos de la placa de pruebas hacia el segundo LED, que también se enciende.
* Después de pasar por el segundo LED, la corriente entra en la resistencia de 220Ω, donde encuentra resistencia, reduciendo la cantidad de corriente. Sin esta resistencia, la corriente a través de los LEDs sería demasiado alta y podría quemarlos.
* Finalmente, la corriente regresa al pin de tierra del Arduino Uno R3, completando el circuito.

**Pregunta:** 

En este circuito en serie, ¿qué sucede si quitas uno de los LEDs? ¿Por qué ocurre esto?

.. image:: img/5_serial_circuit_remove.png
    :width: 600
    :align: center


**Midiendo el Voltaje**

1. Configura el multímetro en la posición de 20 voltios en corriente continua (DC).

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Utiliza el multímetro para medir el voltaje a través de la resistencia.

    .. note::
        
        Medir el voltaje de un componente en un circuito significa comprobar el voltaje a través de él. En esencia, el voltaje representa la diferencia de energía entre dos puntos. Entonces, cuando mides el voltaje de un componente, estás midiendo la diferencia de energía de un lado al otro.

.. image:: img/5_serial_circuit_voltage_resistor.png
    :width: 600
    :align: center

3. Registra el voltaje a través de la resistencia, la unidad de voltaje es: Voltios (V).


.. note::

    * El mío fue 1.13V, debes completarlo según tu medición.

    * Debido a problemas de cableado y la inestabilidad de tu mano, es posible que el voltaje fluctúe. Debes mantener la mano firme y observar varias veces para obtener un valor de voltaje bastante estable.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Voltaje Resistencia
     - Voltaje LED1
     - Voltaje LED2
     - Voltaje Total 
   * - 2 LEDs
     - *≈1.13 voltios*
     - 
     - 
     - 

4. Ahora, mide el voltaje a través del LED 1 en el circuito.

.. image:: img/5_serial_circuit_voltage_led1.png
    :width: 600
    :align: center

5. Registra el voltaje a través del LED 1 en la tabla.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Voltaje Resistencia
     - Voltaje LED1
     - Voltaje LED2
     - Voltaje Total 
   * - 2 LEDs
     - *≈1.13 voltios*
     - *≈1.92 voltios*
     - 
     - 

6. Mide el voltaje a través del LED 2 en el circuito.

.. image:: img/5_serial_circuit_voltage_led2.png
    :width: 600
    :align: center

7. Registra el voltaje a través del LED 2 en la tabla.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Voltaje Resistencia
     - Voltaje LED1
     - Voltaje LED2
     - Voltaje Total 
   * - 2 LEDs
     - *≈1.13 voltios*
     - *≈1.92 voltios*
     - *≈1.92 voltios*
     - 

8. Ahora mide el voltaje total en el circuito.

.. image:: img/5_serial_circuit_voltage.png
    :width: 600
    :align: center

9. Completa el valor del voltaje medido en la columna de Voltaje Total de la tabla.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Resistor Voltage
     - LED1 Voltage
     - LED2 Voltage
     - Total Voltage 
   * - 2 LEDs
     - *≈1.13 volts*
     - *≈1.92 volts*
     - *≈1.92 volts*
     - *≈4.97 volts*


A través de nuestras mediciones, descubrirás:

.. code-block::

  4.97 volts ≈ 1.13 volts + 1.92 volts + 1.92 volts

  Total Voltage = Resistor Voltage + LED 1 Voltage + LED 2 Voltage

También puedes calcular si los resultados de tus mediciones se ajustan a la ecuación anterior.

.. note::
    
    Debido a la estabilidad del cableado o a pequeñas diferencias de fabricación en los LEDs y la resistencia, es posible que la suma del voltaje de la resistencia y de los dos LEDs no sea exactamente igual al voltaje total que mediste. Esto también es aceptable, siempre que esté dentro de un rango razonable.


Esta es una característica de un circuito en serie, donde el voltaje total a lo largo del circuito es la suma de los voltajes de cada componente.


**Midiendo la Corriente**

Después de haber comprendido las características de voltaje de los circuitos en serie, ahora exploraremos la corriente dentro del circuito utilizando un multímetro.

1. Configura el multímetro en la posición de 20 miliamperios. La corriente no excederá los 20mA, por lo que se elige esta configuración. Si tienes dudas, se recomienda comenzar con la configuración de 200mA.

.. image:: img/multimeter_20a.png
  :width: 300
  :align: center

2. Para medir la corriente, el multímetro debe integrarse en el flujo del circuito. Mantén el ánodo del LED en el agujero 1F y mueve el cátodo (la pata más corta) del agujero 1E al agujero 3E.

.. image:: img/5_serial_circuit_led1_current.png
    :width: 600
    :align: center

3. Mide la corriente a través del LED 1 en el circuito.

.. image:: img/5_serial_circuit_led1_current1.png
    :width: 600
    :align: center

4. Registra la corriente medida en la tabla.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Corriente LED1
     - Corriente LED2
   * - 2 LEDs
     - *≈4.43 miliamperios*
     - 

5. Mueve el cátodo del primer LED de regreso a su posición original y cambia el cátodo del segundo LED (la pata más corta) del agujero 1J al agujero 2J.

.. image:: img/5_serial_circuit_led2_current.png
    :width: 600
    :align: center

6. Mide la corriente a través del LED 2 en el circuito.

.. image:: img/5_serial_circuit_led2_current1.png
    :width: 600
    :align: center

7. Registra la corriente medida en la tabla.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Corriente LED1
     - Corriente LED2
   * - 2 LEDs
     - *≈4.43 miliamperios*
     - *≈4.43 miliamperios*

Nuestras mediciones han ilustrado un principio fundamental de los circuitos en serie: la corriente que fluye a través de cada componente es idéntica. Este flujo constante subraya la interconexión de los componentes en serie, donde la interrupción de la corriente en una parte afecta a todo el circuito.

La exploración del voltaje, la corriente y la resistencia no solo enriquece nuestra comprensión de los circuitos en serie, sino que también sienta las bases para conceptos más complejos de la ingeniería eléctrica. A través de estos experimentos prácticos, cerramos la brecha entre la teoría y la aplicación práctica, haciendo que el proceso de aprendizaje sea tanto atractivo como informativo.

**Pregunta**

Si se añade otro LED a este circuito, resultando en tres LEDs, ¿cómo cambiará la luminosidad de los LEDs? ¿Por qué? ¿Cómo cambian los voltajes a través de los tres LEDs?


Explorando los Circuitos en Paralelo
---------------------------------------

**Componentes Necesarios**

* 1 * Arduino Uno R3
* 3 * LEDs rojos
* 3 * Resistencias de 220Ω
* Varios cables jumper
* 1 * Cable USB
* 1 * Protoboard
* 1 * Multímetro con cables de prueba

**Construyendo el Circuito**

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center
  
1. Conecta una resistencia de 220Ω al protoboard. Un extremo debe estar en el terminal negativo, y el otro extremo en el agujero 1B.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Añade un LED rojo al protoboard. El ánodo del LED (pata larga) debe estar en el agujero 1F. El cátodo (pata corta) debe estar en el agujero 1E.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Usa un cable jumper corto para conectar el LED a la fuente de alimentación. Un extremo del cable jumper debe estar en el agujero 1J. El otro extremo debe estar en el terminal positivo.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center


4. Conecta el cable largo conectado al terminal positivo del protoboard al pin de 5V en el Arduino Uno R3. El LED debería encenderse y permanecer encendido. El pin de 5V proporciona un voltaje constante de 5V en corriente continua (DC) al circuito. Esto es diferente del pin 13, que se puede programar mediante el software Arduino IDE para encenderse y apagarse.

.. image:: img/5_parallel_circuit_5v.png
    :width: 600
    :align: center

5. Conecta el terminal negativo del protoboard a uno de los pines de tierra en el Arduino Uno R3. Los pines de tierra están marcados como "GND".

.. image:: img/5_parallel_circuit_gnd.png
    :width: 600
    :align: center

6. Toma otra resistencia de 220Ω y conecta un extremo al terminal negativo y el otro extremo al agujero 6B.

.. image:: img/5_parallel_circuit_resistor.png
    :width: 600
    :align: center

7. Toma otro LED rojo. El ánodo del LED (pata larga) debe estar en el agujero 6F. El cátodo (pata corta) debe estar en el agujero 6E.

.. image:: img/5_parallel_circuit_led.png
    :width: 600
    :align: center

8. Finalmente, coloca un extremo de un cable jumper corto en el agujero 6J y el otro extremo en el terminal positivo. Esto completa el circuito en paralelo.

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center

Ahora, este circuito tiene dos LEDs en una configuración en paralelo. Hay dos caminos para que fluya la corriente:

* En el primer camino: la corriente entra en el primer LED desde el cable jumper, fluye a través de la resistencia limitadora de corriente y luego hacia el lado negativo del protoboard.
* En el segundo camino: la corriente entra en el segundo LED desde el cable jumper, fluye a través de la resistencia limitadora de corriente y luego hacia el lado negativo del protoboard.
* En el lado negativo, los dos caminos se vuelven a juntar y luego fluyen a través del cable negro de alimentación para llegar al pin de tierra del Arduino Uno R3.


**Pregunta:**

En este circuito en paralelo, ¿qué sucede si se retira uno de los LEDs? ¿Por qué ocurre esto?

.. image:: img/5_parallel_circuit_remove.png
    :width: 600
    :align: center


**Pasos para la medición de voltaje**

1. Ajusta el multímetro en el modo de 20V en corriente continua (DC).

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Recuerda que en un circuito en paralelo, cada rama recibe el voltaje completo de la fuente de alimentación. Así que cada rama en tu configuración debería mostrar alrededor de 5 voltios. Comienza midiendo el voltaje a lo largo del primer camino.

.. image:: img/5_parallel_circuit_voltage1.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Voltaje Camino 1
     - Voltaje Camino 2
   * - 2 LEDs
     - *≈5.00 voltios*
     - 

3. Luego, verifica la caída de voltaje en el segundo camino. Espera que sea cercano a los 5 voltios también.

.. image:: img/5_parallel_circuit_voltage2.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuito
     - Voltaje Camino 1
     - Voltaje Camino 2
   * - 2 LEDs
     - *≈5.00 voltios*
     - *≈5.00 voltios*

Nuestro ejercicio de medición de voltaje en un circuito en paralelo demuestra claramente que cada rama recibe una porción igual del voltaje total de la fuente, aproximadamente 5 voltios en este caso. Esta consistencia a través de diferentes caminos confirma la naturaleza fundamental de los circuitos en paralelo, donde el voltaje se mantiene constante en cada rama, a pesar de posibles variaciones menores debido a diferencias de fabricación en componentes como LEDs y resistencias.


**Pasos para la Medición de Corriente**

En nuestras mediciones anteriores, aprendimos que cada rama en un circuito en paralelo recibe el voltaje completo de la fuente. Pero, ¿qué sucede con la corriente? Vamos a medirla ahora.

1. Ajusta el multímetro en la posición de 200 miliamperios.

.. image:: img/multimeter_200ma.png
    :width: 300
    :align: center

2. Para medir la corriente, el multímetro debe integrarse en el flujo del circuito. Deja un extremo de la resistencia en el terminal negativo del protoboard y mueve el otro extremo al agujero 3B.

.. note::

    Este paso hará que el LED 1 se apague mientras que el LED 2 permanece encendido. Esto demuestra una característica de los circuitos en paralelo: la desconexión de un camino no afecta a los otros.

.. image:: img/5_parallel_circuit_led1_current.png
    :width: 600
    :align: center

3. Coloca los cables rojo y negro del multímetro entre el LED y la resistencia, y verás que el LED 1 vuelve a encenderse.

.. image:: img/5_parallel_circuit_led1_current1.png
    :width: 600
    :align: center

4. Registra la corriente medida en la tabla.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Corriente LED1
     - Corriente LED2
     - Corriente Total
   * - 2 LEDs
     - *≈12.6 miliamperios*
     -
     - 

5. Regresa la primera resistencia a su posición original y deja un extremo de la segunda resistencia en el terminal negativo del protoboard mientras mueves el otro extremo al agujero 9B.

.. image:: img/5_parallel_circuit_led2_current.png
    :width: 600
    :align: center

6. Ahora, mide la corriente a través del LED 2 en el circuito.

.. image:: img/5_parallel_circuit_led2_current1.png
    :width: 600
    :align: center

7. Registra la corriente medida en la tabla.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Corriente LED1
     - Corriente LED2
     - Corriente Total
   * - 2 LEDs
     - *≈12.6 miliamperios*
     - *≈12.6 miliamperios*
     - 

8. Habiendo medido la corriente en ambas ramas, ¿cuál es la corriente total cuando los caminos se juntan? Ahora, mueve el cable jumper del terminal negativo del protoboard al agujero 25C.

.. image:: img/5_parallel_circuit_total_current.png
    :width: 600
    :align: center

9. Mide la corriente total del circuito ahora.

.. image:: img/5_parallel_circuit_total_current1.png
    :width: 600
    :align: center

10. Completa los resultados medidos en la tabla.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuito
     - Corriente LED1
     - Corriente LED2
     - Corriente Total
   * - 2 LEDs
     - *≈12.6 miliamperios*
     - *≈12.6 miliamperios*
     - *≈25.3 miliamperios*

Nuestra exploración de los circuitos en paralelo ha revelado un aspecto clave: la corriente total es la suma de las corrientes individuales de cada rama, lo que confirma los principios fundamentales de los circuitos eléctricos. Esta actividad práctica no solo refuerza nuestra comprensión de los circuitos en paralelo, sino que también destaca su comportamiento único en comparación con los circuitos en serie, proporcionando una imagen clara de cómo los componentes en paralelo comparten la carga eléctrica. A medida que continuamos nuestro viaje por el mundo de la electrónica, estos conocimientos sientan las bases para investigaciones más profundas en el diseño y la funcionalidad de los circuitos.

**Pregunta**:

1. Si se añade otro LED a este circuito, ¿qué sucede con la luminosidad de los LEDs? ¿Por qué? Registra tu respuesta en tu cuaderno.

.. image:: img/5_parallel_circuit_3led.png
    :width: 600
    :align: center


Resumen de Circuitos en Serie y Paralelos
-----------------------------------------------------

**Circuitos en Serie**

* **Ventajas**: Dado que la corriente en todo el circuito es la misma, es fácil controlar la corriente. Si un componente falla, la corriente se detendrá. Su cableado es más simple, lo que reduce el costo de construir circuitos grandes.
* **Desventajas**: Si una parte del circuito se daña, todo el circuito dejará de funcionar. Dado que la corriente en el circuito es constante, no se pueden usar componentes que requieran corrientes diferentes.

**Circuitos en Paralelo**

* **Ventajas**: Si cualquier rama del circuito se desconecta, no afecta a las otras ramas. Un dispositivo en una rama puede operar independientemente de otros dispositivos. Se pueden agregar más ramas al circuito en cualquier momento de manera sencilla.
* **Desventajas**: A medida que se agregan más dispositivos al circuito, se extrae más corriente. Esto puede volverse peligroso a medida que el circuito se calienta, lo que podría provocar un incendio. Se utilizan fusibles o disyuntores para desconectar el circuito cuando la corriente es demasiado alta para evitar el sobrecalentamiento. Su cableado es más complejo, lo que aumenta el costo de construir circuitos grandes.

**Reglas de los Circuitos en Serie y Paralelo**

Estas son las reglas para los circuitos en serie y paralelo, que puedes seguir verificando con un multímetro:

.. .. list-table::
..    :widths: 10 25 25 25
..    :header-rows: 1

..    * - Circuito
..      - Voltaje
..      - Corriente
..      - Resistencia  
..    * - Serie
..      - El voltaje total del circuito es igual a la suma de los voltajes utilizados por cada componente (Voltaje total = V1 + V2 + V3 + ...).
..      - La corriente en cualquier punto del circuito es la misma (Corriente total = I1 = I2 = I3 = ...).
..      - La resistencia total de un circuito es igual a la suma de las resistencias de cada componente (Resistencia total = R1 + R2 + R3 + ...).
..    * - Paralelo
..      - El voltaje utilizado por cada carga es igual al voltaje total utilizado por el circuito (Voltaje total = V1 = V2 = V3 = ...)
..      - La corriente total del circuito es igual a la suma de las corrientes utilizadas por cada componente (Corriente total = I1 + I2 + I3 + ...).
..      - El recíproco de la resistencia total es igual a la suma de los recíprocos de las resistencias de cada componente (1/Resistencia total = 1/R1 + 1/R2 + 1/R3 + ...)   


**Serie**

  - El voltaje total del circuito es igual a la suma de los voltajes utilizados por cada componente (Voltaje total = V1 + V2 + V3 + ...).
  - La corriente en cualquier punto del circuito es la misma (Corriente total = I1 = I2 = I3 = ...).
  - La resistencia total de un circuito es igual a la suma de las resistencias de cada componente (Resistencia total = R1 + R2 + R3 + ...).

**Paralelo**

  - El voltaje utilizado por cada carga es igual al voltaje total utilizado por el circuito (Voltaje total = V1 = V2 = V3 = ...)
  - La corriente total del circuito es igual a la suma de las corrientes utilizadas por cada componente (Corriente total = I1 + I2 + I3 + ...).
  - El recíproco de la resistencia total es igual a la suma de los recíprocos de las resistencias de cada componente (1/Resistencia total = 1/R1 + 1/R2 + 1/R3 + ...)   

