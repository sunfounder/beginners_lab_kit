.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones en días festivos.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.


4. La Ley de Ohm: Un Viaje por los Conceptos Esenciales de los Circuitos Eléctricos
=========================================================================================

Todo dispositivo electrónico opera bajo principios que gobiernan los circuitos y las placas de circuitos. Para asegurar que estos dispositivos funcionen correctamente, los ingenieros eléctricos deben comprender profundamente y controlar el flujo de electricidad. Un concepto crucial en este campo es la Ley de Ohm, que establece una relación fundamental entre el voltaje, la corriente y la resistencia en los circuitos eléctricos. Esta lección profundiza en la Ley de Ohm, explorando sus implicaciones y aplicaciones.

Esta lección explora los principios fundamentales que subyacen a cada dispositivo electrónico que utilizamos hoy en día. Comprender estos principios, en particular la Ley de Ohm, es crucial para que los ingenieros eléctricos controlen y predigan el comportamiento de los circuitos de manera efectiva.


La Chispa de la Electricidad
-----------------------------

La historia de la electricidad comienza con experimentos tempranos y descubrimientos profundos. Benjamin Franklin, con su experimento de la cometa, aunque no descubrió la electricidad, despertó curiosidad y fomentó una mayor exploración de las cargas eléctricas y sus poderes.

.. image:: img/2_electronic.webp
    :width: 600
    :align: center

Sus experimentos sentaron las bases para entender que la electricidad implica el movimiento de cargas positivas y negativas, análogo a los fenómenos naturales como los rayos. Inspirado por Franklin, el científico francés Thomas-François Dalibard demostró ejemplos prácticos de cómo las corrientes eléctricas pueden ocurrir de forma natural.

Esta era también fue testigo de la rivalidad y logros conjuntos de Nikola Tesla y Thomas Edison, cuyos esfuerzos ayudaron a moldear nuestra infraestructura eléctrica moderna. El desarrollo de la corriente alterna (AC) por Tesla y la introducción de la bombilla por Edison ejemplifican los rápidos avances en la ingeniería eléctrica.

.. image:: img/2_lamp.webp
    :width: 400
    :align: center

Los avances continuaron con la invención del transistor en 1947, un componente fundamental para todos los dispositivos electrónicos modernos. Este pequeño pero poderoso dispositivo permitió la creación de microchips e interruptores electrónicos, esenciales en el mundo tecnológico actual.

.. image:: img/2_transistor.jpg
    :width: 300
    :align: center
    

Georg Ohm y su Ley
-------------------------

En medio de estos avances tecnológicos, Georg Ohm, un físico alemán, emprendió experimentos que definirían los principios fundamentales de los circuitos eléctricos. En un momento en que la electricidad aún era un campo científico novedoso, Ohm exploró cómo se comportaban las corrientes eléctricas bajo diferentes condiciones, utilizando configuraciones experimentales básicas pero efectivas que involucraban cables, baterías y resistencias caseras.

Los meticulosos experimentos de Ohm revelaron una relación proporcional constante entre el voltaje, la corriente y la resistencia, encapsulada en la fórmula V=IR, ahora celebrada como la Ley de Ohm. Este descubrimiento no solo proporcionó una descripción matemática de la electricidad, sino que también facilitó el diseño y funcionamiento predecible de los dispositivos eléctricos.

.. code-block::

    Voltage = Current x Resistance
    Or
    V = I • R

La perseverancia de Ohm a pesar del escepticismo destacó la importancia de sus hallazgos, que sentaron las bases para futuros avances tecnológicos y marcaron el comienzo de una nueva era en la ingeniería eléctrica.


Comprendiendo la Corriente, el Voltaje y la Resistencia
--------------------------------------------------------------

Para comprender y aplicar completamente la Ley de Ohm, es esencial captar los conceptos básicos de la corriente, el voltaje y la resistencia. Estos componentes son elementos indispensables en cualquier circuito, análogos a los elementos de un río que fluye.

- **Corriente (I)**: El flujo de electrones a través de un conductor, medido en amperios (amperios).
- **Voltaje (V)**: La fuerza eléctrica o presión que impulsa a los electrones a través de un conductor.
- **Resistencia (R)**: Oposición al flujo de electrones, medida en ohmios (Ω), y generalmente representada por la letra griega omega.

.. image:: img/2_resistance.png
    :width: 400
    :align: center

Una analogía con una manguera de jardín ayuda a aclarar estos conceptos:

- **Corriente** es comparable al flujo de agua, indicando la velocidad a la que los electrones se mueven a través de un conductor.
- **Voltaje** es como el control del grifo, regulando la fuerza que impulsa el agua.
- **Resistencia** es similar a los nudos o dobleces en la manguera, que obstruyen el camino del agua y ralentizan el flujo.

Esta explicación nos ayuda a conectar el conocimiento teórico de la Ley de Ohm con el comportamiento de los circuitos reales, sentando las bases para un aprendizaje y aplicación más profundos.


Explorando la Ley de Ohm con Experimentos Prácticos
-------------------------------------------------------

Ahora, apliquemos la Ley de Ohm de manera práctica utilizando un simple circuito con un LED para observar los efectos de cambiar la resistencia y el voltaje.

**Configuración del Experimento**

1. Comenzarás con un circuito básico que incluye un LED y una resistencia de 220 ohmios.
   
   .. image:: img/2_uno_gnd.png
     :width: 600
     :align: center

2. Sustituye la resistencia de 220 ohmios por otras de diferentes valores como se indica a continuación. Registra los cambios en el brillo del LED con cada sustitución para observar cómo la resistencia afecta la corriente y, en consecuencia, la salida de luz.

   .. list-table::
      :widths: 25 100
      :header-rows: 1

      * - Resistencia
        - Observaciones
      * - 100Ω
        - 
      * - 1KΩ
        - 
      * - 10KΩ
        - 
      * - 1MΩ
        - 

  
  Notarás que solo con la resistencia de 100Ω el LED es más brillante que con la resistencia anterior de 220Ω. Con resistencias más altas, el brillo del LED disminuye hasta apagarse por completo en 1MΩ. ¿Por qué ocurre esto?

  Según la Ley de Ohm (I = V/R), a medida que la resistencia aumenta mientras se mantiene constante el voltaje, la corriente que pasa por el LED disminuye, lo que atenúa el LED. Con una resistencia de 1MΩ, la corriente es demasiado pequeña para encender el LED.

3. Después de observar los efectos del cambio de resistencia, mantén la resistencia en 220 ohmios y cambia el suministro de voltaje del circuito de 5V a 3.3V. Registra cualquier cambio en el brillo del LED.

  Notarás que el LED es ligeramente más tenue a 3.3V que a 5V. ¿Por qué sucede esto?

  Usando la Ley de Ohm, sabiendo la resistencia y el nuevo voltaje, la corriente debería ser I = V/R. Con una disminución del voltaje mientras la resistencia se mantiene igual, la corriente disminuye, atenuando el LED.

**Resumen**

Al realizar estos experimentos, has observado directamente cómo la Ley de Ohm es fundamental para comprender y diseñar circuitos eléctricos. Esta aplicación práctica ayuda a consolidar los conceptos teóricos discutidos anteriormente y demuestra las implicaciones del voltaje, la corriente y la resistencia en el mundo real de la ingeniería eléctrica.
