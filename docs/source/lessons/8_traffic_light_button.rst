.. note::

    Bonjour et bienvenue dans la communauté SunFounder des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprenez et partagez** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

8. Feu de signalisation avec bouton piéton
===========================================

Bienvenue dans la prochaine étape de notre voyage avec Arduino. Dans la leçon précédente, nous avons construit un système de feu de signalisation de base, essentiel à la régulation du trafic, avec des feux rouges, jaunes et verts. Nous allons maintenant ajouter une couche d'interaction reflétant les complexités du monde réel : un bouton pour piétons. Cette fonctionnalité introduit un élément humain à notre croisement électronique, permettant une interaction dynamique entre les piétons et la circulation.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/8_traffic_light_button.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Dans cette leçon, vous apprendrez à :

* Comprendre le fonctionnement des boutons et leur rôle dans les circuits.
* Utiliser ``digitalRead()`` pour détecter les niveaux d'entrée sur une broche.
* Implémenter des instructions ``if`` pour créer des comportements conditionnels dans les systèmes de feu de signalisation.

Au cours de ce projet, nous allons explorer non seulement la configuration technique, mais aussi la logique et la programmation qui permettent à ces systèmes d'être à la fois possibles et efficaces dans la gestion du trafic piétonnier et automobile.

Construire le circuit
-------------------------

**Composants nécessaires**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rouge
     - 1 * LED jaune
     - 1 * LED verte
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_yellow_led| 
     - |list_green_led| 
   * - 1 * Bouton-poussoir
     - 1 * Plaque d'essai
     - 3 * Résistance de 220Ω
     - 1 * Résistance de 10KΩ
   * - |list_button| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Câble USB
     - Câbles de connexion
     - 1 * Multimètre
     - 
   * - |list_usb_cable| 
     - |list_wire| 
     - |list_meter| 
     - 


**Étapes de construction**

Suivez le schéma de câblage ou les étapes ci-dessous pour construire votre circuit.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center  

1. Commencez avec le circuit du feu de signalisation de la leçon précédente.

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

2. Trouvez un bouton-poussoir.

.. image:: img/8_traffic_button.png
    :width: 500
    :align: center

Les boutons sont des composants omniprésents en électronique, agissant comme des interrupteurs pour ouvrir ou fermer des circuits. Voici la structure interne d'un bouton et son symbole courant utilisé dans les schémas de circuits.

.. image:: img/8_traffic_button_symbol.png
    :width: 500
    :align: center

Bien que les boutons aient quatre broches, les broches 1 et 2 sont connectées, tout comme les broches 3 et 4. En appuyant sur le bouton, toutes les broches sont connectées, fermant ainsi le circuit.

3. Insérez le bouton dans la plaque d'essai au niveau de la fente centrale, avec les broches dans les trous 18e, 18f, 20e et 20f.

.. note::

    Si vous avez du mal à insérer le bouton, essayez dans les deux sens. Dans un sens, l'espacement des broches sera légèrement trop étroit pour s'adapter.

.. image:: img/8_traffic_light_button_button.png
    :width: 600
    :align: center

4. Connectez la broche en haut à droite du bouton à la broche numérique 8 de l'Arduino Uno R3 avec un long câble de connexion, en insérant une extrémité dans le trou 18j et l'autre dans la broche 8.

.. image:: img/8_traffic_light_button_pin8.png
    :width: 600
    :align: center

5. Placez une résistance de 10KΩ entre la broche en haut à gauche du bouton et la masse, en connectant une extrémité au trou 18a et l'autre à la borne négative de la plaque d'essai. Cette résistance tire la broche 8 vers la masse, la stabilisant à LOW lorsque le bouton n'est pas pressé.

    .. image:: img/8_traffic_light_button_10k.png
        :width: 600
        :align: center

La broche 8 sert d'entrée pour lire l'état du bouton. Les cartes Arduino lisent les tensions comprises entre 0 et environ 5 volts sur les broches d'entrée, les interprétant comme LOW ou HIGH en fonction d'un seuil de tension. Pour qu'une broche soit lue comme HIGH, elle doit avoir plus de 3 volts. Pour être lue comme LOW, elle doit avoir moins de 1,5 volt.

Sans la résistance de 10KΩ, si la broche 8 était uniquement reliée au bouton, elle flotterait entre 0 et 5V, provoquant des fluctuations aléatoires entre HIGH et LOW.

La résistance de 10KΩ connectée entre la broche 8 et la masse tire la tension de la broche vers le niveau de la masse, garantissant qu'elle soit lue comme LOW lorsque le bouton n'est pas pressé.

6. Enfin, alimentez le bouton en connectant la borne positive de la plaque d'essai à la broche 5V de l'Arduino Uno R3 à l'aide d'un fil rouge.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center


**Question :**

Votre feu de signalisation est un mélange de circuits en série et en parallèle. Discutez des parties de votre circuit qui sont en série et expliquez pourquoi. Ensuite, expliquez quelles parties sont en parallèle et pourquoi.


Création de Code
--------------------

**Initialisation des Pins**

Jusqu'à présent, vous avez programmé les feux de circulation pour que les LED vertes, jaunes et rouges clignotent séquentiellement. Dans cette leçon, vous allez programmer le bouton piéton afin que, lorsqu'il est pressé, les LED rouges et jaunes s'éteignent tandis que la LED verte clignote, indiquant qu'il est sûr pour les piétons de traverser.

1. Ouvrez le sketch que vous avez sauvegardé précédemment, ``Lesson7_Traffic_Light``. Cliquez sur "Enregistrer sous..." dans le menu "Fichier" et renommez-le en ``Lesson8_Traffic_Light_Button``. Cliquez sur "Enregistrer".

2. Dans la fonction ``void setup()``, ajoutez une autre commande ``pinMode()`` pour déclarer la pin 8 en tant qu'entrée (``INPUT``). Ensuite, ajoutez un commentaire de code pour expliquer cette nouvelle commande.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Configuration initiale exécutée une seule fois :
        pinMode(3, OUTPUT); // Définir la pin 3 comme sortie
        pinMode(4, OUTPUT); // Définir la pin 4 comme sortie
        pinMode(5, OUTPUT); // Définir la pin 5 comme sortie
        pinMode(8, INPUT);  // Déclarer la pin 8 (bouton) comme entrée
    }
    
    void loop() {
        // Code principal, exécuté en boucle :
        digitalWrite(3, HIGH);  // Allumer la LED sur la pin 3
        digitalWrite(4, LOW);   // Éteindre la LED sur la pin 4
        digitalWrite(5, LOW);   // Éteindre la LED sur la pin 5
        delay(10000);           // Attendre 10 secondes
        digitalWrite(3, LOW);   // Éteindre la LED sur la pin 3
        digitalWrite(4, HIGH);  // Allumer la LED sur la pin 4
        digitalWrite(5, LOW);   // Éteindre la LED sur la pin 5
        delay(3000);            // Attendre 3 secondes
        digitalWrite(3, LOW);   // Éteindre la LED sur la pin 3
        digitalWrite(4, LOW);   // Éteindre la LED sur la pin 4
        digitalWrite(5, HIGH);  // Allumer la LED sur la pin 5
        delay(10000);           // Attendre 10 secondes
    }

3. Après avoir codé, vérifiez votre sketch et téléversez le code sur l'Arduino Uno R3.

**Mesure de la Tension sur la Pin 8**

Nous savons déjà comment fonctionne la section des LED de notre circuit grâce à la leçon précédente. Chaque LED, agissant comme une sortie, est contrôlée par différentes pins de l'Arduino Uno R3.

Cependant, le bouton connecté à la pin 8 est différent. C'est un dispositif d'entrée. La pin 8 lira la tension entrante au lieu d'envoyer de la tension.

Utilisons un multimètre pour tester la tension à la pin 8 lorsque le bouton est pressé et relâché. Vous pourriez avoir besoin de l'aide d'un ami pour appuyer sur le bouton pendant la mesure.

1. Réglez le multimètre sur la position 20 volts DC.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Lorsque le bouton n'est pas pressé, mesurez la tension à la pin 8. Touchez le fil de test rouge du multimètre à la pin 8 et le fil noir à la masse (GND).

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

3. Notez la tension mesurée dans le tableau.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - État du Bouton
     - Tension à la Pin 8
     - État
   * - Relâché
     - *0,00 volts*
     - 
   * - Pressé
     - 
     - 

4. Demandez à votre ami de vous aider à appuyer sur le bouton, puis continuez à mesurer la tension à la pin 8.

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

5. Lorsque le bouton est pressé, enregistrez la tension à la pin 8 dans le tableau.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - État du Bouton
     - Tension à la Pin 8
     - État
   * - Relâché
     - *0,00 volts*
     - 
   * - Pressé
     - *≈4,97 volts*
     - 

6. Les cartes Arduino lisent des tensions comprises entre 0 et environ 5 volts sur les pins d'entrée, les interprétant comme ``LOW`` ou ``HIGH`` en fonction d'une tension de seuil. Pour qu'une pin soit lue comme ``HIGH``, elle doit recevoir plus de 3 volts. Pour être lue comme ``LOW``, elle doit recevoir moins de 1,5 volts.

   En fonction de la tension mesurée, remplissez l'état pour la pin 8.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - État du Bouton
     - Tension à la Pin 8
     - État de la Pin 8
   * - Relâché
     - *0,00 volts*
     - *LOW*
   * - Pressé
     - *≈4,97 volts*
     - *HIGH*


**Instructions Conditionnelles**

Le feu de circulation doit afficher deux comportements différents selon que le bouton est pressé ou non :

* Lorsque le bouton est pressé, le code pour le passage piéton doit s'exécuter, et la LED verte doit clignoter.
* Lorsque le bouton n'est pas pressé, le feu de circulation doit fonctionner normalement, comme vous l'avez programmé.

Pour programmer ces comportements, vous utiliserez une nouvelle fonction de codage appelée instructions conditionnelles.

Les instructions conditionnelles sont parfois appelées instructions ``si-alors``, 
ou plus simplement, une instruction ``if``. Elles vous permettent d'exécuter certaines 
lignes de code lorsqu'une condition ou un scénario spécifique est vérifié.

.. image:: img/if.png
    :width: 300
    :align: center

.. note::

    Vous utilisez souvent des instructions conditionnelles dans la vie quotidienne pour prendre des décisions, par exemple :

    .. code-block:: Arduino

        start;
        if cold;
        then wear a coat;
        end;

Dans l'IDE Arduino, une instruction conditionnelle ressemble à ceci :

    .. code-block:: Arduino

        if (condition) {
            commands to run when the condition is true 
        }

La ``condition`` se trouve entre parenthèses, et utilise des opérateurs de comparaison pour comparer deux ou plusieurs valeurs. Ces valeurs peuvent être des nombres, des variables ou des entrées venant de l'Arduino Uno R3.

Voici une liste des opérateurs de comparaison et comment ils sont utilisés dans la partie conditionnelle d'une instruction if :

.. list-table::
    :widths: 20 20 60
    :header-rows: 1

    *   - Opérateur de Comparaison
        - Signification
        - Exemple
    *   - ==
        - Égal à
        - if (digitalRead(8) == HIGH) {faire quelque chose}
    *   - !=
        - Différent de
        - if (digitalRead(5) != LOW) {faire quelque chose}
    *   - <
        - Inférieur à
        - if (distance < 100) {faire quelque chose}
    *   - >
        - Supérieur à
        - if (count > 5) {faire quelque chose}
    *   - <=
        - Inférieur ou égal à
        - if (number <= minValue) {faire quelque chose}
    *   - >=
        - Supérieur ou égal à
        - if (number >= maxValue) {faire quelque chose}

.. note::

    La comparaison d'égalité utilise deux signes égaux (``==``). Un signe égal seul (``=``) est utilisé pour attribuer une valeur à une variable (comme expliqué dans les sections suivantes), tandis que deux signes égaux sont utilisés pour comparer deux valeurs.

Lorsque vous comparez deux valeurs dans une condition, le résultat peut être ``True`` ou ``False``. Si la condition est ``True``, les commandes entre accolades sont exécutées. Si la condition est ``False``, les commandes sont ignorées.

En programmation, les instructions conditionnelles peuvent être simples ou impliquer des arguments logiques complexes avec plusieurs conditions et scénarios. Vous utiliserez la forme basique des instructions ``if`` dans les prochaines étapes.

**Bouton Non Pressé**

En nous basant sur notre compréhension des instructions conditionnelles, appliquons ce concept pour améliorer notre sketch du feu de circulation. Comme le fait d'appuyer sur un bouton modifie le flux de circulation, nous allons intégrer une condition pour surveiller l'état du bouton.

1. D'après nos mesures précédentes de la tension de la pin 8, nous savons que lorsque le bouton n'est pas pressé, la pin 8 est à l'état ``LOW``. Ainsi, si la lecture de l'état de la pin 8 renvoie ``LOW``, cela signifie que le bouton n'est pas pressé. Maintenant, au début de la fonction ``void loop()`` dans votre code précédent, entrez l'instruction suivante :

    .. code-block:: Arduino
        :emphasize-lines: 11,13

        void setup() {
            // Code de configuration exécuté une seule fois :
            pinMode(3, OUTPUT); // Définir la pin 3 comme sortie
            pinMode(4, OUTPUT); // Définir la pin 4 comme sortie
            pinMode(5, OUTPUT); // Définir la pin 5 comme sortie
            pinMode(8, INPUT);  // Déclarer la pin 8 (bouton) comme entrée
        }

        void loop() {
            // Code principal, exécuté en boucle :
            if (digitalRead(8) == LOW) {
                
            }

            digitalWrite(3, HIGH);  // Allumer la LED sur la pin 3
            digitalWrite(4, LOW);   // Éteindre la LED sur la pin 4
            digitalWrite(5, LOW);   // Éteindre la LED sur la pin 5

            ...

Tout comme la commande ``digitalWrite()`` est utilisée pour les pins de sortie, la commande ``digitalRead()`` est utilisée pour les pins d'entrée. ``digitalRead(pin)`` est la commande permettant de lire si une pin numérique est à l'état ``HIGH`` ou ``LOW``.

Voici sa syntaxe :

    * ``digitalRead(pin)`` : Lit la valeur d'une pin numérique spécifiée, soit ``HIGH``, soit ``LOW``.

        **Paramètres**
            - ``pin`` : le numéro de la pin Arduino que vous souhaitez lire.
        
        **Retourne**
            ``HIGH`` ou ``LOW``.

2. Ensuite, ajoutez les commandes à exécuter lorsque le bouton n'est pas pressé. Ces commandes sont celles que vous avez déjà créées pour le fonctionnement normal du feu de circulation.

    * Vous pouvez couper et coller ces commandes à l'intérieur des accolades de l'instruction ``if``,
    * Ou bien, vous pouvez simplement déplacer l'accolade fermante de l'instruction ``if`` après le dernier ``delay``.
    * Utilisez la méthode qui vous convient le mieux. Après avoir effectué cette modification, votre fonction ``void loop()`` devrait ressembler à ceci :

.. code-block:: Arduino
    :emphasize-lines: 11,24

    void setup() {
        // Code de configuration exécuté une seule fois :
        pinMode(3, OUTPUT); // Définir la pin 3 comme sortie
        pinMode(4, OUTPUT); // Définir la pin 4 comme sortie
        pinMode(5, OUTPUT); // Définir la pin 5 comme sortie
        pinMode(8, INPUT);  // Déclarer la pin 8 (bouton) comme entrée
    }

    void loop() {
        // Code principal, exécuté en boucle :
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // Allumer la LED sur la pin 3
            digitalWrite(4, LOW);   // Éteindre la LED sur la pin 4
            digitalWrite(5, LOW);   // Éteindre la LED sur la pin 5
            delay(10000);           // Attendre 10 secondes
            digitalWrite(3, LOW);   // Éteindre la LED sur la pin 3
            digitalWrite(4, HIGH);  // Allumer la LED sur la pin 4
            digitalWrite(5, LOW);   // Éteindre la LED sur la pin 5
            delay(3000);            // Attendre 3 secondes
            digitalWrite(3, LOW);   // Éteindre la LED sur la pin 3
            digitalWrite(4, LOW);   // Éteindre la LED sur la pin 4
            digitalWrite(5, HIGH);  // Allumer la LED sur la pin 5
            delay(10000);           // Attendre 10 secondes
        }
    }

Notez comment les commandes à l'intérieur de l'instruction ``if`` sont indentées. Utiliser l'indentation permet de garder votre code ordonné et de clarifier quelles commandes sont exécutées au sein d'une fonction. Même si cela prend quelques secondes supplémentaires, l'indentation, les sauts de ligne et les commentaires dans le code permettent de maintenir la lisibilité, ce qui sera avantageux à long terme.

Une erreur courante de syntaxe est d'oublier le nombre d'accolades requis. Parfois, l'accolade fermante est manquante dans une fonction, ou trop d'accolades fermantes sont ajoutées. Dans votre sketch, chaque accolade ouvrante doit avoir une accolade fermante. Une bonne indentation aide également à résoudre les erreurs liées aux accolades mal appariées.

**Quand le bouton est pressé**

Il est maintenant temps d'écrire le code qui permet aux piétons de traverser la rue lorsque le bouton est pressé.

Cela nécessitera une deuxième instruction conditionnelle. Cette fois-ci, vous devrez comparer la valeur de ``digitalRead()`` pour la pin 8 à ``HIGH`` au lieu de ``LOW``.

Lorsque le bouton est pressé, le feu de circulation doit arrêter tous les véhicules et signaler qu'il est sûr pour les piétons de traverser. Pour ce faire, vous devez éteindre les LED rouges et jaunes et faire clignoter la LED verte. À l'intérieur des accolades de votre deuxième instruction conditionnelle, ajoutez trois commandes ``digitalWrite()`` :

* Allumez la LED verte connectée à la pin 3.
* Éteignez la LED jaune connectée à la pin 4.
* Éteignez la LED rouge connectée à la pin 5.

Ensuite, faites clignoter la LED verte. N'oubliez pas que la fréquence de clignotement est déterminée par vos instructions ``delay()``.

Votre sketch devrait ressembler à ceci :

.. code-block:: Arduino
    :emphasize-lines: 24-31

    void setup() {
        pinMode(3, OUTPUT);  // déclarer la pin 3 (LED verte) comme sortie
        pinMode(4, OUTPUT);  // déclarer la pin 4 (LED jaune) comme sortie
        pinMode(5, OUTPUT);  // déclarer la pin 5 (LED rouge) comme sortie
        pinMode(8, INPUT);   // déclarer la pin 8 (bouton) comme entrée
    }

    void loop() {
        // Code principal, exécuté en boucle :
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // Allumer la LED sur la pin 3
            digitalWrite(4, LOW);   // Éteindre la LED sur la pin 4
            digitalWrite(5, LOW);   // Éteindre la LED sur la pin 5
            delay(10000);           // Attendre 10 secondes
            digitalWrite(3, LOW);   // Éteindre la LED sur la pin 3
            digitalWrite(4, HIGH);  // Allumer la LED sur la pin 4
            digitalWrite(5, LOW);   // Éteindre la LED sur la pin 5
            delay(3000);            // Attendre 3 secondes
            digitalWrite(3, LOW);   // Éteindre la LED sur la pin 3
            digitalWrite(4, LOW);   // Éteindre la LED sur la pin 4
            digitalWrite(5, HIGH);  // Allumer la LED sur la pin 5
            delay(10000);           // Attendre 10 secondes
        }
        if (digitalRead(8) == HIGH) {  // si le bouton est pressé :
            digitalWrite(3, HIGH);       // Allumer la LED sur la pin 3
            digitalWrite(4, LOW);        // Éteindre la LED sur la pin 4
            digitalWrite(5, LOW);        // Éteindre la LED sur la pin 5
            delay(500);                  // Attendre une demi-seconde
            digitalWrite(3, LOW);        // Éteindre la LED sur la pin 3
            delay(500);                  // Attendre une demi-seconde
        }
    }

Téléversez votre code sur l'Arduino Uno R3. Une fois le sketch transféré, le code s'exécutera.

Observez le comportement de votre feu de circulation. Appuyez sur le bouton et attendez que le feu termine son cycle. La LED verte pour piétons clignote-t-elle ? Lorsque le bouton est relâché, le feu revient-il à son mode de fonctionnement normal ? Si ce n'est pas le cas, ajustez votre sketch et téléversez-le à nouveau sur la carte R3.

Une fois terminé, sauvegardez votre sketch.

**Question**

Pendant les tests, vous pouvez remarquer que la LED verte ne clignote que lorsque le bouton piéton est maintenu enfoncé, mais les piétons ne peuvent pas traverser la route en maintenant le bouton appuyé. Comment pouvez-vous modifier le code pour vous assurer que, une fois le bouton piéton pressé, la LED verte reste allumée suffisamment longtemps pour permettre une traversée sécurisée sans avoir à maintenir le bouton appuyé ? Veuillez écrire la solution en pseudo-code dans votre cahier.

**Résumé**

Dans cette leçon, nous avons intégré un bouton piéton dans un système de feux de circulation, simulant un scénario réel qui équilibre le flux de piétons et de véhicules. Nous avons exploré le fonctionnement d'un bouton dans un circuit électronique et utilisé la fonction ``digitalRead()`` pour surveiller les entrées du bouton. En utilisant des instructions conditionnelles avec des structures ``if``, nous avons programmé les feux pour qu'ils réagissent dynamiquement à l'entrée des piétons, renforçant ainsi notre compréhension des systèmes interactifs. Cette leçon nous a non seulement permis de perfectionner nos compétences en programmation Arduino, mais a également mis en lumière l'application pratique de ces technologies dans la gestion efficace de situations du quotidien.

