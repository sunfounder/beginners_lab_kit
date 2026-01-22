.. note::

    Bonjour, bienvenue dans la communauté Facebook des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 ! Plongez dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et relevez les défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Avant-premières exclusives** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des promotions festives et à des tirages au sort.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !


5. Circuit en série vs. Circuit en parallèle
===============================================

Dans cette leçon, vous allez construire et analyser des circuits en série et en parallèle, tout en apprenant à mesurer et à comprendre comment la tension se comporte dans différentes configurations de circuits. En utilisant un multimètre, vous mesurerez la tension et la résistance des circuits que vous construisez, acquérant ainsi une compréhension pratique des dynamiques des circuits.

Dans cette leçon passionnante, vous allez :

* Relier les schémas électriques aux circuits réels.
* Utiliser un multimètre pour mesurer la résistance et la tension.
* Construire des circuits en série et en parallèle à l'aide d'une plaque d'essai.
* Comparer le comportement de la tension dans les circuits en série et en parallèle.

Ces objectifs vous permettront de combler le fossé entre les connaissances théoriques et l'application pratique, enrichissant ainsi votre compréhension de l'électronique grâce à une expérience pratique.


Circuit en série vs. Circuit en parallèle
---------------------------------------------

Dans nos leçons précédentes, nous avons construit un circuit simple avec un Arduino Uno R3, une résistance et une LED. Le courant dans cette configuration circule en série : du Pin 13 de la carte, à travers la LED, puis à travers la résistance avant de retourner au Pin GND. C'est un exemple simple de circuit en série.

Mais au fur et à mesure que nous avançons dans le monde de l'électronique, nous rencontrons des circuits plus complexes, composés de composants disposés en série ou en parallèle. Pour comprendre ces configurations et leurs implications sur le courant et la tension, il est nécessaire de se familiariser avec les schémas de circuits, aussi appelés schémas électriques.

**Schémas de câblage vs. Schémas électriques**

Nous avons utilisé des schémas de câblage—des représentations picturales qui imitent la disposition physique des composants du circuit. Ces schémas sont intuitifs et utiles pour l'assemblage :

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

Cependant, pour comprendre la fonctionnalité et la logique de conception d'un circuit, les schémas électriques sont indispensables. Ces schémas réduisent les circuits à leur essence, en utilisant des symboles standardisés pour représenter chaque composant. Ils révèlent les relations électriques entre les composants sans l'encombrement des dispositions physiques.

Voici les symboles d'une LED, d'une résistance et d'une batterie que vous trouverez souvent dans les schémas :

.. image:: img/5_led_resistor_symbol.png
  :align: center

Un schéma électrique basé sur notre câblage précédent ressemblerait à ceci, avec l'Arduino Uno R3 entier agissant comme une batterie alimentant le circuit. À partir de ce schéma, vous pouvez clairement indiquer le flux et la direction du courant, simplifiant ainsi la complexité des connexions physiques.

.. image:: img/5_serial_circuit_1led.png
  :align: center

**Configurations en série vs. en parallèle**

Dans un circuit en série, les composants sont alignés en rangée, de sorte que le courant n'a qu'un seul chemin à suivre. Si un composant tombe en panne, tout le circuit est interrompu—comme une guirlande de lumières de Noël où une ampoule grillée éteint toute la chaîne.

.. image:: img/5_serial_circuit_2led.png
  :align: center

Un circuit en parallèle, quant à lui, divise le courant en plusieurs chemins. Chaque composant fonctionne indépendamment, donc si un chemin est interrompu, les autres continuent de fonctionner. Pensez au système électrique de votre maison : si vous éteignez une lumière, la télévision peut toujours fonctionner.

.. image:: img/5_parallel_circuit.png
  :align: center


Exploration des circuits en série
---------------------------------

En nous appuyant sur notre compréhension des différences entre les circuits en série et en parallèle, cette activité se concentre sur la construction d'un circuit en série avec plusieurs LEDs. Rappelez-vous que dans un circuit en série, le courant électrique circule sur un seul trajet. Explorons les caractéristiques uniques des circuits en série à travers cet exercice pratique.

**Composants nécessaires**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 3 * LEDs rouges
     - 3 * Résistances de 220Ω
     - Câbles de connexion
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Câble USB
     - 1 * Plaque d'essai
     - 1 * Multimètre
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter| 
     - 

**Construire le circuit**

1. Modifiez le circuit LED précédent en retirant le câble de connexion entre 1J et le côté positif de la plaque d'essai à droite. Ensuite, prenez une autre LED rouge et insérez sa cathode (la patte la plus courte) dans 1J, et l'anode dans le côté positif de la plaque d'essai, afin de pouvoir connecter une autre LED en série dans le circuit.

.. image:: img/5_serial_circuit.png

Vous avez maintenant un circuit en série avec deux LEDs. Suivez le parcours du courant à travers le circuit :

* Le courant circule à partir de 5V sur l'Arduino Uno R3, à travers un long câble de connexion jusqu'au terminal positif de la plaque d'essai.
* Ensuite, le courant traverse la première LED, l'allumant grâce au flux de courant.
* Le courant passe ensuite par les clips métalliques de la plaque d'essai pour atteindre la deuxième LED, qui s'allume également.
* Après avoir quitté la deuxième LED, il entre dans la résistance de 220Ω, où il rencontre une résistance, réduisant ainsi l'intensité du courant. Sans cette résistance, le courant dans les LEDs serait trop élevé et pourrait les brûler.
* Le courant retourne ensuite au pin GND de l'Arduino Uno R3, complétant ainsi le circuit.

**Question :**

Dans ce circuit en série, que se passe-t-il si vous retirez une LED ? Pourquoi cela se produit-il ?

.. image:: img/5_serial_circuit_remove.png
    :width: 600
    :align: center


**Mesurer la tension**

1. Réglez le multimètre sur la position 20 volts en courant continu (DC).

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Utilisez le multimètre pour mesurer la tension aux bornes de la résistance.

    .. note::
        
        Mesurer la tension d'un composant dans un circuit signifie vérifier la tension à ses bornes. En essence, la tension représente la différence d'énergie entre deux points. Ainsi, lorsque vous mesurez la tension d'un composant, vous évaluez la différence d'énergie d'un côté à l'autre.

.. image:: img/5_serial_circuit_voltage_resistor.png
    :width: 600
    :align: center

3. Notez la tension mesurée aux bornes de la résistance, unité de mesure : Volts (V).

.. note::

    * La mienne était de 1,13V, vous devez indiquer votre propre mesure.

    * En raison de problèmes de câblage ou d'instabilité de la main, vous pouvez constater des fluctuations de la tension. Essayez de stabiliser votre main, puis observez plusieurs fois pour obtenir une valeur de tension relativement stable.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Tension Résistance
     - Tension LED1
     - Tension LED2
     - Tension Totale 
   * - 2 LEDs
     - *≈1.13 volts*
     - 
     - 
     - 

4. Mesurez maintenant la tension aux bornes de la LED 1 dans le circuit.

.. image:: img/5_serial_circuit_voltage_led1.png
    :width: 600
    :align: center

5. Inscrivez la tension mesurée aux bornes de la LED 1 dans le tableau.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Tension Résistance
     - Tension LED1
     - Tension LED2
     - Tension Totale 
   * - 2 LEDs
     - *≈1.13 volts*
     - *≈1.92 volts*
     - 
     - 

6. Mesurez la tension aux bornes de la LED 2 dans le circuit.

.. image:: img/5_serial_circuit_voltage_led2.png
    :width: 600
    :align: center

7. Notez la tension mesurée aux bornes de la LED 2 dans le tableau.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Tension Résistance
     - Tension LED1
     - Tension LED2
     - Tension Totale 
   * - 2 LEDs
     - *≈1.13 volts*
     - *≈1.92 volts*
     - *≈1.92 volts*
     - 

8. Mesurez maintenant la tension totale du circuit.

.. image:: img/5_serial_circuit_voltage.png
    :width: 600
    :align: center

9. Remplissez la tension mesurée dans la colonne Tension Totale du tableau.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Tension Résistance
     - Tension LED1
     - Tension LED2
     - Tension Totale 
   * - 2 LEDs
     - *≈1.13 volts*
     - *≈1.92 volts*
     - *≈1.92 volts*
     - *≈4.97 volts*


Grâce à nos mesures, vous découvrirez :

.. code-block::

  4.97 volts ≈ 1.13 volts + 1.92 volts + 1.92 volts

  Tension Totale = Tension Résistance + Tension LED 1 + Tension LED 2

Vous pouvez également vérifier si vos résultats de mesure correspondent à cette équation.

.. note::
    
    En raison de l'instabilité des câblages ou des petites différences de fabrication des LEDs et de la résistance, il est possible que la somme des tensions mesurées aux bornes de la résistance et des LEDs ne soit pas exactement égale à la tension totale mesurée. Tant que la différence reste dans une plage raisonnable, cela ne pose pas de problème.


C'est une caractéristique d'un circuit en série, où la tension totale dans le circuit est la somme des tensions à travers chaque composant.

**Mesurer le courant**

Après avoir compris les caractéristiques de la tension dans un circuit en série, explorons maintenant le courant dans le circuit à l'aide d'un multimètre.

1. Réglez le multimètre sur la position 20 milliampères. Le courant ne dépassera pas 20mA, c'est donc le réglage choisi. En cas de doute, il est recommandé de commencer par la position 200mA.

.. image:: img/multimeter_20a.png
  :width: 300
  :align: center

2. Pour mesurer le courant, le multimètre doit être intégré dans le trajet du flux du circuit. Gardez l'anode de la LED dans le trou 1F et déplacez sa cathode (la patte la plus courte) du trou 1E au trou 3E.

.. image:: img/5_serial_circuit_led1_current.png
    :width: 600
    :align: center

3. Mesurez le courant à travers la LED 1 dans le circuit.

.. image:: img/5_serial_circuit_led1_current1.png
    :width: 600
    :align: center

4. Inscrivez le courant mesuré dans le tableau.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - Courant LED1
     - Courant LED2
   * - 2 LEDs
     - *≈4.43 milliamps*
     - 

5. Replacez la cathode de la première LED dans sa position d'origine et déplacez la cathode de la deuxième LED (la patte la plus courte) du trou 1J au trou 2J.

.. image:: img/5_serial_circuit_led2_current.png
    :width: 600
    :align: center

6. Mesurez le courant à travers la deuxième LED dans le circuit.

.. image:: img/5_serial_circuit_led2_current1.png
    :width: 600
    :align: center

7. Notez le courant mesuré dans le tableau.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - Courant LED1
     - Courant LED2
   * - 2 LEDs
     - *≈4.43 milliamps*
     - *≈4.43 milliamps*

Nos mesures ont illustré un principe fondamental des circuits en série : le courant qui traverse chaque composant est identique. Ce flux constant souligne l'interdépendance des composants en série, où l'interruption du courant dans une partie affecte l'ensemble du circuit.

L'exploration de la tension, du courant et de la résistance enrichit non seulement notre compréhension des circuits en série, mais jette également les bases de concepts plus complexes en ingénierie électrique. C'est par ces expériences pratiques que nous comblons le fossé entre la théorie et l'application, rendant le processus d'apprentissage à la fois captivant et informatif.


**Question**

Si une autre LED est ajoutée à ce circuit, ce qui donne trois LEDs, comment la luminosité des LEDs change-t-elle ? Pourquoi ? Comment les tensions à travers les trois LEDs changent-elles ?



Exploration des circuits en parallèle
------------------------------------------

**Composants nécessaires**

* 1 * Arduino Uno R3
* 3 * LEDs rouges
* 3 * Résistances de 220Ω
* Plusieurs fils de connexion
* 1 * Câble USB
* 1 * Plaque d'essai
* 1 * Multimètre avec pointes de test

**Construction du circuit**

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center
  
1. Connectez une résistance de 220Ω à la plaque d'essai. Une extrémité doit être dans le terminal négatif, et l'autre dans le trou 1B.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Ajoutez une LED rouge à la plaque d'essai. L'anode (longue patte) de la LED doit être dans le trou 1F et la cathode (courte patte) dans le trou 1E.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Utilisez un court fil de connexion pour relier la LED à la source d'alimentation. Une extrémité du fil doit être dans le trou 1J et l'autre dans le terminal positif.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Connectez le long fil de connexion, relié au terminal positif de la plaque d'essai, au pin 5V de l'Arduino Uno R3. La LED devrait s'allumer et rester allumée. Le pin 5V fournit un courant constant de 5 volts DC au circuit, contrairement au pin 13, qui peut être programmé via le logiciel Arduino IDE pour s'allumer et s'éteindre.

.. image:: img/5_parallel_circuit_5v.png
    :width: 600
    :align: center

5. Reliez le terminal négatif de la plaque d'essai à l'une des broches de masse ("GND") de l'Arduino Uno R3.

.. image:: img/5_parallel_circuit_gnd.png
    :width: 600
    :align: center

6. Prenez une autre résistance de 220Ω et connectez une extrémité au terminal négatif et l'autre au trou 6B.

.. image:: img/5_parallel_circuit_resistor.png
    :width: 600
    :align: center

7. Prenez une autre LED rouge. L'anode de la LED (longue patte) doit être dans le trou 6F et la cathode (courte patte) dans le trou 6E.

.. image:: img/5_parallel_circuit_led.png
    :width: 600
    :align: center

8. Enfin, placez une extrémité d'un court fil de connexion dans le trou 6J et l'autre dans le terminal positif. Cela complète le circuit en parallèle.

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center

Maintenant, ce circuit contient deux LEDs dans une configuration parallèle. Il existe deux chemins pour que le courant circule :

* Dans le premier chemin : le courant entre dans la première LED depuis le fil de connexion, traverse la résistance limitant le courant, puis se dirige vers le côté négatif de la plaque d'essai.
* Dans le second chemin : le courant entre dans la deuxième LED depuis le fil de connexion, traverse la résistance limitant le courant, puis se dirige vers le côté négatif de la plaque d'essai.
* Au côté négatif, les deux chemins convergent à nouveau, puis le courant retourne au pin de masse de l'Arduino Uno R3.


**Question :**

Dans ce circuit en parallèle, que se passe-t-il si l'on retire une LED ? Pourquoi cela se produit-il ? 

.. image:: img/5_parallel_circuit_remove.png
    :width: 600
    :align: center


**Étapes de mesure de la tension**

1. Réglez le multimètre sur le mode courant continu 20 volts.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Rappelez-vous, dans un circuit en parallèle, chaque branche reçoit la tension totale de la source d'alimentation. Chaque branche de votre montage devrait donc afficher environ 5 volts. Commencez par mesurer la tension le long du premier chemin.

.. image:: img/5_parallel_circuit_voltage1.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - Tension Chemin 1
     - Tension Chemin 2
   * - 2 LEDs
     - *≈5.00 volts*
     - 

3. Ensuite, vérifiez la chute de tension dans le second chemin. Attendez-vous à ce qu'elle soit également proche de 5 volts.

.. image:: img/5_parallel_circuit_voltage2.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - Path1 Voltage
     - Path2 Voltage
   * - 2 LEDs
     - *≈5.00 volts*
     - *≈5.00 volts*

Notre exercice de mesure de la tension dans un circuit en parallèle démontre clairement que chaque branche reçoit une part égale de la tension totale provenant de la source, soit environ 5 volts dans ce cas. Cette constance entre les différents chemins confirme la nature fondamentale des circuits en parallèle, où la tension reste constante à travers chaque branche, malgré de possibles variations mineures dues à des différences de fabrication dans les composants tels que les LEDs et les résistances.

**Étapes de mesure du courant**

Lors de nos mesures précédentes, nous avons appris que chaque branche dans un circuit en parallèle reçoit la pleine tension de la source. Mais qu'en est-il du courant ? Mesurons-le maintenant.

1. Réglez le multimètre sur la position 200 milliampères.

.. image:: img/multimeter_200ma.png
    :width: 300
    :align: center

2. Pour mesurer le courant, le multimètre doit être intégré dans le chemin du flux du circuit. Laissez une extrémité de la résistance sur le terminal négatif de la plaque d'essai et déplacez l'autre extrémité au trou 3B.

.. note::
    
    Cette étape éteindra la LED 1 tandis que la LED 2 restera allumée. Cela démontre une caractéristique des circuits en parallèle : la déconnexion d'un chemin n'affecte pas les autres.

.. image:: img/5_parallel_circuit_led1_current.png
    :width: 600
    :align: center

3. Placez les sondes rouge et noire du multimètre entre la LED et la résistance, et vous verrez la LED1 s'allumer à nouveau.

.. image:: img/5_parallel_circuit_led1_current1.png
    :width: 600
    :align: center

4. Notez le courant mesuré dans le tableau.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Courant LED1
     - Courant LED2
     - Courant Total
   * - 2 LEDs
     - *≈12.6 milliamps*
     - 
     - 

5. Remettez la première résistance dans sa position d'origine, et gardez une extrémité de la deuxième résistance sur le terminal négatif de la plaque d'essai tout en déplaçant l'autre extrémité au trou 9B.

.. image:: img/5_parallel_circuit_led2_current.png
    :width: 600
    :align: center

6. Mesurez maintenant le courant à travers la LED 2 dans le circuit.

.. image:: img/5_parallel_circuit_led2_current1.png
    :width: 600
    :align: center

7. Notez le courant mesuré dans le tableau.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Courant LED1
     - Courant LED2
     - Courant Total
   * - 2 LEDs
     - *≈12.6 milliamps*
     - *≈12.6 milliamps*
     - 

8. Après avoir mesuré le courant dans les deux chemins, quel est le courant total lorsque les chemins convergent ? Déplacez maintenant le fil de connexion du terminal négatif de la plaque d'essai au trou 25C.

.. image:: img/5_parallel_circuit_total_current.png
    :width: 600
    :align: center

9. Mesurez maintenant le courant total du circuit.

.. image:: img/5_parallel_circuit_total_current1.png
    :width: 600
    :align: center

10. Remplissez les résultats mesurés dans le tableau.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuit
     - LED1 Current
     - LED2 Current
     - Total Current
   * - 2 LEDs
     - *≈12.6 milliamps*
     - *≈12.6 milliamps*
     - *≈25.3 milliamps*

Notre exploration des circuits en parallèle a mis en lumière un aspect clé : le courant total est la somme des courants de chaque branche individuelle, conformément aux principes fondamentaux des circuits électriques. Cette activité pratique renforce notre compréhension des circuits en parallèle et met en évidence leur comportement distinct par rapport aux circuits en série, offrant une vision claire de la manière dont les composants en parallèle partagent la charge électrique. À mesure que nous poursuivons notre voyage dans le monde de l'électronique, ces découvertes posent les bases d'investigations plus approfondies dans la conception et le fonctionnement des circuits.

**Question** :

1. Si une autre LED est ajoutée à ce circuit, que se passe-t-il avec la luminosité des LEDs ? Pourquoi ? Notez votre réponse dans votre carnet.

.. image:: img/5_parallel_circuit_3led.png
    :width: 600
    :align: center



Résumé des circuits en série et en parallèle
------------------------------------------------

**Circuits en série**

* **Avantages** : Puisque le courant est le même tout au long du circuit, il est facile de contrôler le courant. Si un composant tombe en panne, le courant s'arrête. Le câblage est plus simple, ce qui réduit le coût de fabrication des grands circuits.
* **Inconvénients** : Si une partie du circuit est endommagée, tout le circuit cesse de fonctionner. Étant donné que le courant est constant, il est impossible d'utiliser des composants nécessitant des courants différents.

**Circuits en parallèle**

* **Avantages** : Si un chemin du circuit est déconnecté, cela n'affecte pas les autres branches du circuit. Un appareil sur une branche peut fonctionner indépendamment des autres appareils. Il est facile d'ajouter de nouvelles branches à tout moment.
* **Inconvénients** : À mesure que de nouveaux appareils sont ajoutés, plus de courant est tiré. Cela peut devenir dangereux car le circuit peut chauffer, ce qui risque de provoquer un incendie. Des fusibles ou des disjoncteurs sont utilisés pour déconnecter le circuit lorsque le courant est trop élevé afin d'éviter une surchauffe. Le câblage est plus complexe, ce qui augmente le coût de fabrication des grands circuits.

**Règles des circuits en série et en parallèle**

Voici les règles pour les circuits en série et en parallèle, que vous pouvez continuer à vérifier à l'aide d'un multimètre :

.. .. list-table::
..    :widths: 10 25 25 25
..    :header-rows: 1

..    * - Circuit
..      - Voltage
..      - Current
..      - Resistance  
..    * - Series
..      - The total voltage of the circuit equals the sum of the voltages used by each component (Total voltage = V1 + V2 + V3 + ...).
..      - The current at any point in the circuit is the same (Total current = I1 = I2 = I3 = ...).
..      - The total resistance of a circuit equals the sum of the resistances of each component (Total resistance = R1 + R2 + R3 + ...).
..    * - Parallel
..      - The voltage used by each load equals the total voltage used by the circuit (Total voltage = V1 = V2 = V3 = ...)
..      - The total current of the circuit equals the sum of the currents used by each component (Total current = I1 + I2 + I3 + ...).
..      - The reciprocal of the total resistance equals the sum of the reciprocals of each component's resistance (1/ Total resistance = 1/R1 + 1/R2 + 1/R3 + ...)   


**Série**

  - La tension totale du circuit est égale à la somme des tensions utilisées par chaque composant (Tension totale = V1 + V2 + V3 + ...).
  - Le courant en tout point du circuit est le même (Courant total = I1 = I2 = I3 = ...).
  - La résistance totale d'un circuit est égale à la somme des résistances de chaque composant (Résistance totale = R1 + R2 + R3 + ...).

**Parallèle**

  - La tension utilisée par chaque charge est égale à la tension totale utilisée par le circuit (Tension totale = V1 = V2 = V3 = ...).
  - Le courant total du circuit est égal à la somme des courants utilisés par chaque composant (Courant total = I1 + I2 + I3 + ...).
  - L'inverse de la résistance totale est égal à la somme des inverses des résistances de chaque composant (1/Résistance totale = 1/R1 + 1/R2 + 1/R3 + ...).

