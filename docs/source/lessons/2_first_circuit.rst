.. note::

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprenez & partagez** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d'un accès anticipé aux annonces de nouveaux produits.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et concours** : Participez à des concours et promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _2_first_circuit:

2. Votre Premier Circuit
============================

Bienvenue dans le monde électrisant de votre premier circuit, où un simple interrupteur peut illuminer votre environnement, et un seul clic peut donner vie à des gadgets. Cette leçon est votre porte d'entrée pour comprendre la force invisible de l'électricité qui alimente les appareils que nous utilisons tous les jours. Curieux de savoir comment fonctionnent vos gadgets préférés ou ce qui fait briller les lumières ? Il est temps de vous lancer dans une exploration pratique de la construction de circuits.

Au début de cette aventure, nous explorerons les origines de l'électricité et suivrons les parcours des électrons à travers les circuits. Cette leçon sert d'introduction pratique aux composants d'un circuit et à leur interaction pour accomplir diverses fonctions. Vous jouerez également le rôle de détective électrique en découvrant comment exploiter et mesurer efficacement cette énergie vivante.

Préparez-vous à des expériences électrisantes ! Voici ce que vous allez accomplir :

* Utiliser une breadboard pour une construction facile de circuits.
* Lire les codes de couleurs des résistances pour gérer le flux électrique.
* Comprendre comment les LEDs contrôlent la direction du courant.
* Apprendre la tension fournie par l'Arduino Uno R3.
* Découvrir comment les électrons circulent dans un circuit.
* Reconnaître différents types de circuits et leurs fonctions.

Prêt à plonger dans votre première expérience de construction de circuits ? Prenons une charge d'énergie et commençons ce voyage lumineux !


Composants Nécessaires
----------------------

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rouge
     - 1 * Résistance de 220Ω
     - Fils de connexion
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Câble USB
     - 1 * Breadboard
     -
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     -
     - 

Breadboard
--------------

1. Trouvez votre breadboard. 

La breadboard que vous allez utiliser est appelée une breadboard sans soudure. Chaque trou de la breadboard contient un connecteur métallique qui agrippe le fil lorsqu'il est inséré. Cela empêche le fil de se déconnecter, assurant ainsi une connexion sécurisée dans votre circuit.

.. image:: img/2_breadboard_half.png
    :width: 500
    :align: center

Vous vous demandez pourquoi cet outil électronique essentiel porte le même nom que la planche de cuisine utilisée pour trancher du pain ? Voici l'histoire ! Avant les années 1970, les composants électroniques étaient assemblés sur de véritables planches en bois, parfois des planches à pain de cuisine réutilisées, en clouant ou collant des composants et en reliant les connexions par des fils.

.. image:: img/2_breadboard_circuit.jpg
    :width: 500
    :align: center

Des années 1960 aux années 1980, les ingénieurs ont expérimenté le fil enroulé pour des circuits plus complexes, une technique semi-permanente nécessitant des outils spécifiques, mais finalement jugée trop encombrante et inadaptée à une utilisation répétée.

.. image:: img/2_breadboard_wire_wrap.jpg
    :width: 500
    :align: center

Puis, au début des années 1970, Ronald J. Portugal a révolutionné le prototypage avec l'invention de la "breadboard sans soudure", rendant l'assemblage des circuits plus rapide, plus facile et sans besoin de soudure. Cet outil innovant a rapidement surpassé le fil enroulé, menant aux breadboards que nous connaissons aujourd'hui, nommées en hommage à leurs prédécesseurs historiques mais conçues pour le créateur moderne.

.. image:: img/2_breadboard_half.png
    :width: 500
    :align: center

Vous êtes curieux de savoir ce qui se cache sous la surface d'une breadboard ? Derrière sa façade en plastique et une couche de mousse collante, recouverte de papier protecteur jaune, se trouvent des dizaines de bandes métalliques, véritable cœur fonctionnel de la breadboard.

.. note::
    Il est préférable de ne pas retirer cette couche protectrice. Nous l'avons fait ici uniquement pour vous montrer ce qui se trouve à l'intérieur.

.. image:: img/2_breadboard_internal0.jpg
    :width: 500
    :align: center

Si vous retiriez (bien que nous vous le déconseillions vivement) ces pièces métalliques à l'aide de pinces, vous découvririez que chaque pièce est un clip métallique avec de petites dents. Chaque bande comporte cinq dents, correspondant aux cinq trous sur la surface de la breadboard pour chaque rangée. Les rails d'alimentation comportent des bandes plus longues avec cinquante dents.

.. image:: img/2_breadboard_internal1.jpg
    :width: 500
    :align: center

Ces petites dents sont parfaites pour agripper les broches des composants électroniques. Lorsqu'un composant est inséré dans la breadboard, le clip s'ouvre légèrement pour saisir fermement la broche métallique. Tout autre composant inséré dans la même rangée de dents sera connecté électriquement.

.. image:: img/2_breadboard_internal2.jpg
    :width: 500
    :align: center

Ce design ingénieux permet un prototypage facile et flexible sans avoir besoin de soudure, rendant les breadboards essentielles pour les amateurs d'électronique et les professionnels.

La plupart des breadboards sont marquées de chiffres, de lettres et de signes plus et moins. Bien que ces étiquettes varient d'une breadboard à l'autre, la fonction reste essentiellement la même. Ces étiquettes vous permettent de trouver plus rapidement les trous correspondants lors de la construction de votre circuit. Les numéros de rangée et les lettres de colonne vous aident à localiser précisément les trous sur la breadboard. Par exemple, le trou "C15" est l'endroit où la colonne C croise la rangée 15.

.. image:: img/2_breadboard_letter_number.jpg
    :width: 500
    :align: center

Les côtés de la breadboard sont généralement distingués par des couleurs rouge et bleue (ou d'autres couleurs), ainsi que par des signes plus et moins, et sont généralement utilisés pour se connecter à l'alimentation, connus sous le nom de bus d'alimentation.
Lors de la construction d'un circuit, il est courant de connecter la borne négative à la colonne bleue (-) et la borne positive à la colonne rouge (+).

.. image:: img/2_breadboard_plus_minus.jpg
    :width: 500
    :align: center



Résistance
---------------------

2. Trouvez une résistance de 220 ohms.

.. image:: img/2_220_resistor.png
    :align: center

Les résistances aident à gérer le flux d'électricité dans un circuit en convertissant l'énergie électrique en chaleur. Chaque résistance a deux fils, un à chaque extrémité, permettant au courant de passer dans les deux directions, ce qui signifie qu'elles peuvent être placées dans n'importe quel sens dans le circuit.

La valeur en ohms d'une résistance indique la quantité de résistance qu'elle ajoute. Une valeur en ohms plus élevée signifie plus de résistance. Par exemple, une résistance de 220 ohms ajoute 220 ohms de résistance, et une résistance de 10 kiloohms ajoute 10 kiloohms.

Pour lire la valeur d'une résistance, il faut vérifier les bandes de couleur. Ce tableau explique la signification de chaque bande de couleur sur une résistance. Le multiplicateur est représenté en notation scientifique, où l'exposant indique le nombre de zéros ajoutés au nombre représenté par les bandes de couleur. Par exemple, une résistance à 4 bandes avec une bande verte en premier correspond au chiffre 5, donc la valeur commence par 5. La deuxième bande est marron, ce qui donne 1 comme deuxième chiffre. La bande multiplicatrice est rouge, soit 2, ce qui signifie qu'on ajoute deux zéros. Cela donne une résistance totale de 5100 ohms, soit 5,1 kilohms (5,1 kΩ).

.. image:: img/2_resistor_card.png

Le tableau ci-dessus représente toutes les résistances incluses dans votre kit. Pour cette leçon, nous utiliserons une résistance de 220 ohms.

.. image:: img/2_all_resistor.png
    :width: 500
    :align: center

3. Pliez les fils de la résistance pour qu'ils soient orientés dans la même direction.

.. image:: img/2_220_resistor_pin.png
    :width: 200
    :align: center

4. Insérez une patte dans le trou supérieur du côté négatif de la breadboard, connectant ainsi la résistance à la source d'alimentation. Insérez l'autre patte de la résistance de 220 ohms dans le trou 1b de la breadboard.

    .. note::
        
        Les résistances sont considérées comme des composants non polarisés, ce qui signifie que leur orientation dans un circuit n'a pas d'importance.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center


LED
-----------------

5. Trouvez la LED rouge.

.. image:: img/2_red_led.png
    :align: center

Les LED, ou diodes électroluminescentes, sont des composants électroniques spécialisés qui émettent de la lumière lorsqu'un courant électrique les traverse dans une direction spécifique.

.. image:: img/2_led_polarity.jpg
    :width: 200
    :align: center

Les couleurs les plus courantes des LED sont le rouge, le jaune, le bleu, le vert et le blanc, la lumière émise correspondant généralement à la couleur de la LED elle-même.

.. image:: img/2_led_color.png
    :width: 600
    :align: center

Ces dispositifs sont dotés de deux broches : une plus longue, appelée anode, et une plus courte, appelée cathode. Pour fonctionner correctement, l'anode doit être connectée à la borne positive de la source d'alimentation, et la cathode doit être connectée à la borne négative ou à la masse. Certaines LED ont un bord plat sur le côté de la cathode pour faciliter leur placement correct.

.. image:: img/2_led_pin.jpg
    :width: 100
    :align: center

6. Insérez la cathode de la LED (la patte courte) dans le trou 1e de la breadboard. Cela connecte la LED à la résistance de 220Ω. N'oubliez pas que les trous 1b et 1e sont connectés sous la breadboard.

.. note::

    Les LED sont des composants polarisés, ce qui signifie que le courant ne peut circuler que dans une seule direction. Si vous constatez que la LED ne s'allume pas, essayez d'inverser les connexions.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

Fil Jumper
----------------------

7. Trouvez un fil jumper.

Votre kit comprend des fils jumpers de différentes couleurs et longueurs, mais ils fonctionnent tous de la même manière. Utilisez des couleurs variées pour identifier facilement les circuits et des fils plus courts pour un montage plus propre. Chaque fil est constitué d'un noyau conducteur et d'une gaine isolante pour éviter les contacts accidentels.

.. image:: img/2_wire_color.jpg
    :width: 500
    :align: center

8. Insérez une extrémité du fil jumper dans le trou 1j de la breadboard. Cela connecte le fil jumper à la LED, car les trous 1f et 1j sont reliés sous la breadboard. Insérez l'autre extrémité du fil jumper dans le trou supérieur du rail positif de la breadboard. Désormais, le fil jumper relie la LED et le fil de masse.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

Arduino Uno R3
------------------

9. Trouvez votre Arduino Uno R3.

.. image:: img/1_uno_board.png
    :width: 400
    :align: center

Dans cette leçon, nous utilisons l'Arduino Uno R3 comme source d'alimentation. Sa broche 5V sert de borne positive et sa broche GND de borne négative, fournissant un courant constant de 5V au circuit.

.. image:: img/1_uno_power_pin.png
    :width: 500
    :align: center

Cependant, connecter directement les bornes de la source d'alimentation sans charge peut provoquer un court-circuit, générant de la chaleur et potentiellement des dommages ou un incendie. Assurez-vous toujours d'inclure une charge, comme une LED ou une résistance, pour éviter les courts-circuits.

.. image:: img/2_short_circuit.png
    :width: 500
    :align: center

10. Connectez un fil du rail positif sur le côté droit de la breadboard à la broche 5V de l'Arduino Uno R3. Il est recommandé d'utiliser un fil rouge ou orange pour représenter la borne positive, ce qui peut être particulièrement utile pour identifier rapidement les connexions dans des projets complexes.

.. image:: img/2_uno_5v.png
    :width: 600
    :align: center

11. Enfin, connectez un fil du rail négatif sur le côté gauche de la breadboard à la broche GND de l'Arduino Uno R3. Un fil noir ou vert est suggéré pour des raisons de cohérence, en utilisant la même couleur pour représenter la borne négative dans tous les circuits.

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

12. Enfin, alimentez l'Arduino Uno R3 en le connectant à un ordinateur ou à une prise de courant à l'aide du câble USB fourni dans le kit, et la LED devrait s'allumer.

    .. image:: img/2_first_circuit.png
        :width: 600
        :align: center

Après avoir connecté votre Arduino Uno R3 et vu la LED s'allumer, vous n'observez pas seulement un simple circuit, mais vous assistez aux principes fondamentaux de l'électricité en action. Explorons ce qui fait fonctionner votre circuit.


Comprendre l'électricité dans les circuits
----------------------------------------------

**Notions essentielles d'électricité**

Le flux des électrons du négatif vers le positif est ce que nous comprenons comme le flux réel des électrons. Initialement, des scientifiques comme Ben Franklin croyaient que le courant était un mouvement de charges positives, c'est pourquoi le courant conventionnel est défini comme allant du positif vers le négatif.

.. image:: img/2_uno_current.png
    :width: 600
    :align: center

Cependant, en réalité, ce sont les électrons, qui portent une charge négative, qui se déplacent de la borne négative vers la borne positive. Aujourd'hui, la plupart des pays utilisent encore le modèle de flux de courant conventionnel. Ainsi, dans les schémas et lors de la conception de composants électroniques, le courant est représenté comme allant de la borne positive vers la borne négative, même si les électrons se déplacent dans la direction opposée.

.. image:: img/2_uno_electron.png
    :width: 600
    :align: center

* **A** Direction du courant conventionnel
* **B** Direction réelle du flux des électrons
* **C** Électrons (non à l'échelle)
* **D** Fil

Il existe deux types de courant généré par une source d'alimentation : le courant alternatif (CA) et le courant continu (CC). Une batterie ou un microcontrôleur comme l'Arduino Uno R3 fournit du CC, où le courant circule dans une seule direction — de la borne positive à la borne négative.

Avec le CA, cependant, le courant change de direction périodiquement. La tension dans le circuit s'inverse lorsque le courant change de direction, le forçant à circuler dans l'autre sens. La plupart des maisons et des bâtiments sont alimentés par des circuits en CA, comme les 120 volts à 60 Hz des prises murales aux États-Unis ou les 220 volts à 50 Hz dans de nombreux pays européens.

**Sécurité dans les circuits**

Lors de la connexion d'une source d'alimentation, il est recommandé de connecter d'abord la borne positive au circuit, suivie de la borne négative. À l'inverse, lors de la déconnexion, il est préférable de retirer d'abord la borne négative pour éviter les courts-circuits. Ce cours utilise une tension et un courant faibles, donc il n'y a aucun risque de choc électrique ou de blessure. Cependant, de bonnes pratiques de sécurité peuvent prévenir les accidents lorsque l'on travaille avec des tensions et des courants plus élevés, comme lors du remplacement de batteries de voiture ou de la réparation de prises électriques.

**Circuits ouverts et fermés**

Lorsque l'électricité circule à travers la LED, la résistance, les fils jumper, et retourne dans le rail négatif de la breadboard, cela forme ce que l'on appelle un circuit fermé. Si vous retirez un fil de la breadboard, la LED s'éteint car le courant a cessé de circuler — le circuit est désormais ouvert.

.. image:: img/2_open_circuit.png
    :width: 600
    :align: center

En maîtrisant ces notions de base, vous serez en mesure de comprendre et de créer des dispositifs électroniques plus complexes qui alimentent notre monde.


**Questions :**

1. Retirez le fil rouge de la breadboard et essayez de le placer dans différents trous de la breadboard. Observez les changements éventuels de la LED. Dessinez les positions des trous qui permettent à la LED de s'allumer.

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center


2. Que se passe-t-il si vous inversez les broches de la LED ? S'allumera-t-elle ? Pourquoi ou pourquoi pas ?

