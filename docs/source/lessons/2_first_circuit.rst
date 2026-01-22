.. note::

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _2_first_circuit:

2. Tu Primer Circuito
=========================

¡Bienvenido al electrizante mundo de tu primer circuito! Aquí, un simple interruptor puede iluminar tu entorno y un solo clic puede dar vida a los dispositivos. Esta lección es tu puerta de entrada para entender la fuerza invisible de la electricidad que alimenta los aparatos que usamos todos los días. ¿Te has preguntado alguna vez cómo funcionan tus gadgets favoritos o qué hace que las luces brillen? Es hora de embarcarte en una exploración práctica de la construcción de circuitos.

Al comenzar esta aventura, exploraremos los orígenes de la electricidad y seguiremos el camino de los electrones a medida que fluyen a través de los circuitos. Esta lección sirve como una introducción práctica a los componentes de un circuito y cómo interactúan para realizar diversas funciones. También jugarás el papel de un detective eléctrico, descubriendo cómo aprovechar y medir efectivamente esta fuerza activa.

¡Prepárate para algunos experimentos electrizantes! Esto es lo que lograrás:

* Usar una protoboard para una construcción fácil de circuitos.
* Leer los códigos de colores de las resistencias para manejar el flujo eléctrico.
* Comprender cómo los LEDs controlan la dirección de la corriente.
* Aprender sobre el voltaje del Arduino Uno R3.
* Descubrir cómo los electrones fluyen a través de un circuito.
* Reconocer los diferentes tipos de circuitos y sus funciones.

¿Estás listo para sumergirte en tu primera experiencia de construcción de circuitos? ¡Vamos a cargarnos de energía y comenzar este viaje iluminador!


Componentes Necesarios
-------------------------

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rojo
     - 1 * Resistencia de 220Ω
     - Cables de conexión
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Cable USB
     - 1 * Protoboard
     - 
     - 




Protoboard
-------------

1. Localiza tu protoboard.

La protoboard que estarás utilizando se llama protoboard sin soldadura. Cada agujero en la protoboard contiene un conector metálico que sujeta el cable cuando se inserta. Esto ayuda a evitar que el cable se salga, garantizando una conexión segura en tu circuito.

.. image:: img/2_breadboard_half.png
    :width: 500
    :align: center

¿Alguna vez te has preguntado por qué esta herramienta esencial de la electrónica comparte un nombre con la tabla de cocina que se usa para cortar pan? ¡Es toda una historia! En los días anteriores a la década de 1970, los circuitos electrónicos se ensamblaban en tablas de madera, a veces tablas de cortar pan reutilizadas, clavando o pegando los componentes y conectándolos con cables.

.. image:: img/2_breadboard_circuit.jpg
    :width: 500
    :align: center

Desde la década de 1960 hasta la de 1980, los ingenieros experimentaron con el método de envolver cables para circuitos más complejos, que era semi-permanente y requería herramientas específicas, pero finalmente se consideró demasiado engorroso y no adecuado para uso repetido.

.. image:: img/2_breadboard_wire_wrap.jpg
    :width: 500
    :align: center

Luego, a principios de la década de 1970, Ronald J. Portugal revolucionó la creación de prototipos con la invención de la "protoboard sin soldadura", haciendo que el montaje de circuitos fuera más rápido, fácil y sin necesidad de soldar. Esta innovadora herramienta superó rápidamente al método de envolver cables, dando lugar a las protoboards que conocemos hoy, nombradas por sus predecesoras históricas pero diseñadas para el creador moderno.

.. image:: img/2_breadboard_half.png
    :width: 500
    :align: center

¿Tienes curiosidad por saber qué se esconde debajo de la superficie de una protoboard? Detrás de su fachada de plástico y una capa de espuma adhesiva, cubierta por un papel protector amarillo, se encuentra el corazón de la funcionalidad de la protoboard: decenas de tiras metálicas.

.. note::
    Es mejor no despegar esta capa protectora. Lo hemos hecho aquí solo para mostrarte qué hay dentro.

.. image:: img/2_breadboard_internal0.jpg
    :width: 500
    :align: center

Si tiraras (aunque te aconsejamos encarecidamente que no lo hagas) de estas partes metálicas con unos alicates, descubrirías que cada pieza es un clip metálico con pequeños dientes. Cada tira tiene cinco dientes, que corresponden a los cinco agujeros en la superficie de la protoboard en cada fila. Los rieles de alimentación tienen tiras más largas con cincuenta dientes.

.. image:: img/2_breadboard_internal1.jpg
    :width: 500
    :align: center

Estos pequeños dientes son perfectos para sujetar las patas de los componentes electrónicos. Cuando se inserta un componente en la protoboard, el clip se abre ligeramente para sujetar firmemente la pata metálica. Cualquier otro componente insertado en la misma fila de dientes estará conectado eléctricamente.

.. image:: img/2_breadboard_internal2.jpg
    :width: 500
    :align: center

Este ingenioso diseño permite una creación de prototipos fácil y flexible sin la necesidad de soldar, lo que convierte a las protoboards en una herramienta esencial tanto para entusiastas como para profesionales de la electrónica.

La mayoría de las protoboards tienen algunos números, letras y signos de más y menos. Aunque las etiquetas varían de una protoboard a otra, la función es básicamente la misma. Estas etiquetas te permiten encontrar los agujeros correspondientes más rápidamente al construir tu circuito. Los números de fila y las letras de columna te ayudan a ubicar con precisión los agujeros en la protoboard. Por ejemplo, el agujero "C15" es donde la columna C se cruza con la fila 15.

.. image:: img/2_breadboard_letter_number.jpg
    :width: 500
    :align: center


Los laterales de la protoboard suelen estar distinguidos por colores rojo y azul (u otros colores), así como por los signos de más y menos, y generalmente se utilizan para conectar la fuente de alimentación, conocida como el bus de alimentación. Al construir un circuito, es común conectar el terminal negativo a la columna azul (-) y el terminal positivo a la columna roja (+).

.. image:: img/2_breadboard_plus_minus.jpg
    :width: 500
    :align: center



Resistencia
---------------------

2. Localiza una resistencia de 220 ohmios.

.. image:: img/2_220_resistor.png
    :align: center

Las resistencias ayudan a gestionar el flujo de electricidad en un circuito convirtiendo la energía eléctrica en calor. Cada resistencia tiene dos alambres, uno en cada extremo, lo que permite que la electricidad pase en cualquier dirección. Esto significa que se pueden colocar en cualquier sentido dentro del circuito.

El valor en ohmios de una resistencia nos indica la cantidad de resistencia que añade. Un valor más alto de ohmios significa más resistencia. Por ejemplo, una resistencia de 220 ohmios añade 220 ohmios de resistencia, y una resistencia de 10 kiloohmios añade 10 kiloohmios.

Para leer el valor de una resistencia, debes observar las bandas de colores. Este gráfico explica el significado de cada banda de color en una resistencia. El multiplicador está representado en notación científica, donde el exponente indica el número de ceros que se añaden al número representado por las bandas de colores. Por ejemplo, una resistencia de 4 bandas que se muestra en la parte superior del gráfico comienza con una banda verde. El verde representa el número 5, por lo que el valor de la resistencia comienza con 5. La segunda banda es marrón, por lo que el siguiente número es 1. La banda multiplicadora es roja, valorada en 2, lo que significa que añadimos dos ceros. Esto da un valor total de resistencia de 5100 ohmios, o 5.1 kiloohmios (5.1kΩ).

.. image:: img/2_resistor_card.png

El gráfico mostrado aquí representa todas las resistencias incluidas en tu kit. Para esta lección, utilizaremos una resistencia de 220 ohmios.

.. image:: img/2_all_resistor.png
    :width: 500
    :align: center

3. Dobla las patas de la resistencia para que apunten en la misma dirección.

.. image:: img/2_220_resistor_pin.png
    :width: 200
    :align: center

4. Inserta una pata en el agujero superior del lado negativo de la protoboard, conectando la resistencia a la fuente de alimentación. Inserta la otra pata de la resistencia de 220 ohmios en el agujero 1b de la protoboard.

    .. note:: 
        Las resistencias se consideran componentes no polarizados, lo que significa que la dirección en que se colocan en un circuito no afecta su funcionamiento.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

LED
-----------------

5. Encuentra el LED rojo.

.. image:: img/2_red_led.png
    :align: center

Los LED, o diodos emisores de luz, son componentes electrónicos especializados que emiten luz cuando una corriente eléctrica fluye a través de ellos en una dirección específica.

.. image:: img/2_led_polarity.jpg
    :width: 200
    :align: center

Los colores más comunes de los LED son rojo, amarillo, azul, verde y blanco, y la luz emitida normalmente coincide con el color del propio LED.

.. image:: img/2_led_color.png
    :width: 600
    :align: center

Estos dispositivos están diseñados con dos patas: una más larga llamada ánodo y otra más corta llamada cátodo. Para que funcionen correctamente, el ánodo debe conectarse al terminal positivo de la fuente de alimentación, y el cátodo debe conectarse al terminal negativo o tierra. Algunos LEDs tienen un borde plano en el lado del cátodo para facilitar su correcta colocación.

.. image:: img/2_led_pin.jpg
    :width: 100
    :align: center

6. Inserta el cátodo del LED (la pata corta) en el agujero 1e de la protoboard. Esto conecta el LED a la resistencia de 220Ω. Recuerda, los agujeros 1b y 1e están conectados por debajo de la protoboard.

.. note::

    Los LEDs son componentes polarizados, lo que significa que la corriente solo puede fluir a través de ellos en una dirección. Si ves que el LED no se enciende, intenta intercambiar las conexiones.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

Cable Jumper
----------------------

7. Encuentra un cable jumper.

Tu kit incluye cables jumper de diferentes colores y longitudes, todos con la misma función. Utiliza colores variados para facilitar la identificación del circuito y cables más cortos para una configuración ordenada. Cada cable consta de un núcleo conductor y una cubierta aislante para evitar contactos no deseados.

.. image:: img/2_wire_color.jpg
    :width: 500
    :align: center

8. Inserta un extremo del cable jumper en el agujero 1j de la protoboard. Esto conecta el cable jumper al LED, ya que los agujeros 1f y 1j están conectados por debajo de la protoboard. Inserta el otro extremo del cable jumper en el agujero superior del riel positivo de la protoboard. Ahora, el cable jumper conecta el LED y el cable de tierra.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

Arduino Uno R3
-----------------

9. Encuentra tu Arduino Uno R3.

.. image:: img/1_uno_board.png
    :width: 400
    :align: center

En esta lección, estamos utilizando el Arduino Uno R3 como fuente de alimentación. Su pin de 5V actúa como el terminal positivo y el pin GND como el terminal negativo, proporcionando un suministro constante de 5V al circuito.

.. image:: img/1_uno_power_pin.png
    :width: 500
    :align: center

Sin embargo, conectar directamente los terminales de la fuente de alimentación sin una carga puede causar un cortocircuito, generando calor y potencialmente causando daños o incluso un incendio. Siempre incluye una carga, como un LED o una resistencia, para evitar cortocircuitos.

.. image:: img/2_short_circuit.png
    :width: 500
    :align: center

10. Conecta un cable desde el riel positivo en el lado derecho de la protoboard hasta el pin de 5V del Arduino Uno R3. Se recomienda usar un cable rojo o naranja para representar el terminal positivo, lo cual puede ser particularmente útil para identificar rápidamente las conexiones en proyectos más complejos.

.. image:: img/2_uno_5v.png
    :width: 600
    :align: center

11. Finalmente, conecta un cable desde el riel negativo en el lado izquierdo de la protoboard hasta el pin GND del Arduino Uno R3. Se sugiere usar un cable negro o verde para mantener la consistencia, utilizando el mismo color para representar el terminal negativo en todos los circuitos.

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

12. Finalmente, alimenta el Arduino Uno R3 conectándolo a una computadora o a una toma de corriente utilizando el cable USB proporcionado en el kit, y el LED debería encenderse.

    .. image:: img/2_first_circuit.png
        :width: 600
        :align: center

Después de conectar tu Arduino Uno R3 y ver que el LED se enciende, no solo estás viendo un circuito simple, sino que estás observando los fundamentos de la electricidad en acción. Vamos a profundizar en lo que hace que tu circuito cobre vida.

Comprendiendo la Electricidad en los Circuitos
-----------------------------------------------------

**Conceptos Básicos de la Electricidad**

El flujo de electrones desde el terminal negativo al positivo es lo que entendemos como el flujo real de electrones. Inicialmente, científicos como Ben Franklin creían que la corriente era un movimiento de cargas positivas, por lo que la corriente convencional se define como fluyendo de positivo a negativo.

.. image:: img/2_uno_current.png
    :width: 600
    :align: center

Sin embargo, en realidad, los electrones, que llevan una carga negativa, se mueven desde el terminal negativo hacia el terminal positivo. La mayoría de los países hoy en día aún utilizan el modelo de flujo de corriente convencional. Por lo tanto, en los diagramas y al diseñar componentes electrónicos, se representa la corriente fluyendo del terminal positivo al negativo, aunque los electrones realmente fluyen en la dirección opuesta.

.. image:: img/2_uno_electron.png
    :width: 600
    :align: center

* **A** Dirección de la corriente tradicional
* **B** Dirección real del flujo de electrones
* **C** Electrones (no a escala)
* **D** Cable

Hay dos tipos de corriente generada por una fuente de alimentación: corriente alterna (CA) y corriente continua (CC). Una batería o un microcontrolador como el Arduino Uno R3 proporciona CC, donde la corriente fluye en una sola dirección, del terminal positivo al terminal negativo.

Con la CA, sin embargo, la corriente cambia de dirección periódicamente. El voltaje en el circuito se invierte a medida que la corriente cambia de dirección, obligándola a fluir en sentido contrario. La mayoría de las casas y edificios están alimentados por circuitos de CA, como los 120 voltios a 60 Hz en los hogares estadounidenses o los 220 voltios a 50 Hz en muchos hogares europeos.

**Seguridad en Circuitos**

Cuando conectes una fuente de alimentación, es prudente conectar primero el extremo positivo al circuito, seguido del negativo. Por el contrario, al desconectar, debes quitar primero el extremo negativo para evitar cortocircuitos. Este curso utiliza voltajes y corrientes bajos, por lo que no hay riesgo de descarga eléctrica o lesiones. Pero unas buenas prácticas de seguridad pueden prevenir daños cuando trabajes con voltajes y corrientes más altos, como al reemplazar baterías de automóviles o reparar enchufes.

**Circuitos Cerrados y Abiertos**

A medida que la electricidad fluye a través del LED, la resistencia, los cables jumper y regresa al riel negativo de la protoboard, forma lo que se conoce como un circuito cerrado. Si quitas un cable de la protoboard, el LED se apagará porque la corriente se ha detenido, el circuito ahora está abierto.

.. image:: img/2_open_circuit.png
    :width: 600
    :align: center

Al dominar estos conceptos básicos, estarás en camino de comprender y crear dispositivos electrónicos más complejos que impulsan nuestro mundo.


**Preguntas:**

1. Retira el cable rojo de la protoboard y experimenta colocándolo en diferentes agujeros de la protoboard. Observa los cambios en el LED. Haz un esquema de las posiciones de los agujeros que permiten que el LED se encienda.

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

2. ¿Qué ocurre si inviertes las patillas del LED? ¿Se encenderá? ¿Por qué sí o por qué no?

