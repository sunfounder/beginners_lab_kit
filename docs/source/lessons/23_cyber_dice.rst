.. note::

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprenez & Partagez** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et à des avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions spéciales pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

23. Dés électroniques
=======================

Dans cette leçon, nous nous lançons dans un voyage passionnant à travers deux projets impliquant l'électronique numérique et la programmation.

.. image:: img/23_dice.jpg
    :align: center
    :width: 500

Nous allons tout d'abord découvrir le fonctionnement d'un afficheur à 7 segments et apprendre à le contrôler pour afficher des chiffres, étape par étape. Ensuite, nous allons créer un dé électronique ! En appuyant simplement sur un bouton, un nombre aléatoire entre 1 et 6 apparaîtra sur l'afficheur, offrant une touche digitale aux dés traditionnels.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/23_cycle_dice.mp4" type="video/mp4">
        Votre navigateur ne supporte pas la balise vidéo.
    </video>

Pendant cette leçon, vous apprendrez :

* Les principes de fonctionnement d'un afficheur à 7 segments et comment le faire fonctionner.
* L'utilisation des instructions switch-case pour simplifier la logique du code.
* Comment utiliser une boucle while pour maintenir l'état actuel jusqu'à ce qu'un changement soit nécessaire.
* Comment construire le projet des Dés électroniques, en intégrant de simples composants électroniques avec une programmation interactive pour une application pratique.

L'origine des dés
-----------------------

Les dés font partie des plus anciens outils de jeu au monde, avec une histoire remontant à des milliers d'années avant notre ère. Ils sont apparus vers 3000 avant J.-C. dans l'Égypte ancienne, généralement fabriqués à partir d'os, d'ivoire ou d'autres matériaux naturels. Ces premiers dés étaient souvent irréguliers en forme et parfois pas entièrement symétriques.

.. image:: img/23_dice.png
    :width: 500
    :align: center

Les dés ont également été trouvés dans la Mésopotamie ancienne (actuel Irak) à la même époque. Les devins et les chefs religieux anciens utilisaient les dés pour prendre des décisions ou prédire l'avenir, soulignant leur importance dans les rites religieux et mystiques.

Au fil du temps, la forme et les techniques de fabrication des dés sont devenues standardisées. Au Ier siècle avant J.-C., les dés étaient largement utilisés dans l'Empire romain, non seulement pour le jeu, mais aussi à des fins sociales et de divertissement.

En Asie, notamment en Inde, l'utilisation des dés est documentée dans l'épopée ancienne, le Mahabharata, où un jeu de dés joue un rôle crucial dans l'intrigue.

Pendant la Renaissance, la fabrication des dés s'est perfectionnée, et les matériaux se sont diversifiés pour inclure le bois, l'os, l'ivoire et même le métal. Aujourd'hui, les dés ne sont plus seulement des outils de divertissement et de jeu, mais ils sont également utilisés dans l'éducation, l'aide à la prise de décision et divers jeux de société. Leur histoire et leur diversité reflètent l'évolution de la culture et de la technologie humaines, offrant une fenêtre fascinante sur l'exploration du hasard et de la chance.

Comprendre l'afficheur à 7 segments
-------------------------------------------

1. Trouvez un afficheur à 7 segments. 

Un afficheur à 7 segments est un composant en forme de 8 qui intègre 7 LED. Chacune des LED dans l'afficheur est désignée par un segment positionnel avec l'une de ses broches de connexion émergeant du boîtier plastique rectangulaire. Ces broches LED sont étiquetées de "a" à "g", représentant chaque LED individuelle. Une broche LED supplémentaire permet également d'indiquer un point décimal (DP) lorsqu'au moins deux afficheurs à 7 segments sont connectés pour afficher des nombres supérieurs à dix.

.. image:: img/23_7_segment.png
    :width: 300
    :align: center

La broche commune de l'afficheur détermine généralement son type. Il existe deux types de connexions de broches : une avec des cathodes connectées et une autre avec des anodes connectées, indiquant un afficheur à cathode commune (CC) ou à anode commune (CA). Comme son nom l'indique, un afficheur CC a toutes les cathodes des 7 LED connectées, tandis qu'un afficheur CA a toutes les anodes des 7 segments connectées.

.. note::

    Habituellement, il y a une étiquette sur le côté de l'afficheur à 7 segments, xxxAx ou xxxBx. En général, xxxAx signifie cathode commune et xxxBx signifie anode commune. Les afficheurs dans notre kit sont des cathodes communes.

.. image:: img/23_segment_cathode_1.png
    :align: center
    :width: 600

Pour déterminer si un afficheur à 7 segments est une cathode commune ou une anode commune, vous pouvez utiliser un multimètre. Vous pouvez également utiliser un multimètre pour tester si chaque segment de l'afficheur fonctionne correctement, comme suit :

1. Réglez le multimètre en mode test de diode. Le test de diode est une fonction du multimètre utilisée pour vérifier la conduction directe des diodes ou de dispositifs semi-conducteurs similaires (tels que les LED). Le multimètre fait passer un petit courant à travers la diode. Si la diode est intacte, elle laissera passer le courant.

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. Insérez l'afficheur à 7 segments dans une plaque d'essai, en notant que le point décimal est en bas à droite et assurez-vous qu'il traverse l'espace central. Insérez un fil dans la même rangée que la broche 1 de l'afficheur et touchez-le avec la pointe rouge du multimètre. Insérez un autre fil dans la même rangée que toute broche marquée “-” de l'afficheur et touchez-le avec la pointe noire.

.. image:: img/23_7_segment_test.png
    :align: center
    :width: 500

3. Observez si un segment LED s'allume. Si c'est le cas, cela indique que l'afficheur est à cathode commune. Sinon, inversez les fils rouge et noir ; si un segment s'allume après inversion, cela indique que l'afficheur est à anode commune.

4. Si un segment s'allume, référez-vous à ce schéma pour enregistrer le numéro de la broche du segment et sa position approximative dans le tableau du Manuel.

.. image:: img/23_segment_2.png
    :align: center

.. list-table::
    :widths: 20 20 40
    :header-rows: 1

    *   - Broche
        - Numéro de segment
        - Position
    *   - 1
        - a
        - Segment supérieur
    *   - 2
        - 
        - 
    *   - 3
        - 
        - 
    *   - 4
        - 
        - 
    *   - 5
        - 
        - 
    *   - 6
        - 
        - 
    *   - 7
        - 
        - 
    *   - 8
        - 
        - 

5. Répétez les étapes ci-dessus, en gardant la pointe noire sur la broche “-”, et connectez la pointe rouge aux autres broches pour identifier les broches de commande correspondant aux segments LED de l'afficheur.


**Question**

D'après les tests ci-dessus, on sait que l'afficheur dans le kit est à cathode commune, ce qui signifie que vous devez simplement connecter la broche commune à la masse (GND) et fournir une haute tension aux autres broches pour allumer les segments correspondants. Si vous voulez que l'afficheur affiche le chiffre 2, quelles broches doivent recevoir une haute tension ? Pourquoi ?

.. image:: img/23_segment_2.png
    :align: center



Construction du circuit
--------------------------------

**Composants nécessaires**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Afficheur 7 segments
     - 1 * Résistance 220Ω
     - 1 * Résistance 10KΩ
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Bouton
     - 1 * Plaque d'essai (Breadboard)
     - Fils de connexion
     - 1 * Câble USB
   * - |list_button| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
   * - 1 * Multimètre
     - 
     - 
     - 
   * - |list_meter| 
     - 
     - 
     - 


**Étapes de construction**

Suivez le schéma de câblage ou les étapes ci-dessous pour assembler votre circuit.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

1. Insérez l'afficheur 7 segments dans la plaque d'essai, avec le point décimal dans le coin inférieur droit.

.. image:: img/23_segment_segment.png
    :align: center
    :width: 500

2. Insérez une extrémité d'une résistance de 220Ω dans la broche négative (“-”) de l'afficheur 7 segments, et l'autre extrémité dans le rail négatif de la plaque d'essai. Ensuite, connectez le rail négatif de la plaque d'essai à la broche GND de l'Arduino Uno R3 avec un fil de connexion.

.. image:: img/23_segment_resistor_gnd.png
    :align: center
    :width: 500

3. Connectez les broches contrôlant les segments a, b, c de l'afficheur LED aux broches 2, 3 et 4 de l'Arduino Uno R3.

.. image:: img/23_segment_abc.png
    :align: center
    :width: 500

4. Connectez les broches contrôlant les segments d, e, f, g de l'afficheur LED aux broches 5, 6, 7 et 8 de l'Arduino Uno R3.

.. image:: img/23_segment_defg.png
    :align: center
    :width: 500

5. Insérez maintenant un bouton dans la plaque d'essai.

.. image:: img/23_segment_button.png
    :align: center
    :width: 500

6. Connectez la broche inférieure droite du bouton à la broche 9 de l'Arduino R3 avec un fil.

.. image:: img/23_segment_pin9.png
    :align: center
    :width: 500

7. Connectez une résistance de 10KΩ au bouton pour que, lorsque le bouton n'est pas enfoncé, la broche 9 reste à un niveau bas et ne fluctue pas.

.. image:: img/23_segment_10k_resistor.png
    :align: center
    :width: 500

8. Connectez la broche inférieure gauche du bouton au 5V de l'Arduino Uno R3.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - Afficheur 7 segments
        - Arduino UNO R3
    *   - a
        - 2
    *   - b
        - 3 
    *   - c
        - 4
    *   - d
        - 5
    *   - e
        - 6
    *   - f
        - 7
    *   - g
        - 8


Création du code - Affichage des chiffres
-----------------------------------------
1. Ouvrez l'IDE Arduino et démarrez un nouveau projet en sélectionnant “New Sketch” dans le menu “File”.
2. Enregistrez votre croquis sous le nom ``Lesson23_Show_Number`` en utilisant ``Ctrl + S`` ou en cliquant sur “Save”.

3. Définissez les broches connectées à l'afficheur 7 segments et configurez toutes les broches comme des sorties.

.. code-block:: Arduino

    // Définir les broches connectées à l'afficheur 7 segments
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Configurer toutes les broches comme des sorties
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

4. Écrivez maintenant du code pour que l'afficheur 7 segments affiche un chiffre, tel que le chiffre 2. Pour afficher le chiffre 2, réglez les segments F et C à LOW (éteints) et les autres segments à HIGH (allumés).

.. code-block:: Arduino
  :emphasize-lines: 22-29

    // Définir les broches connectées à l'afficheur 7 segments
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Configurer toutes les broches comme des sorties
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {
        // Régler les segments F et C à LOW (éteints) et les autres à HIGH (allumés)
        digitalWrite(pinA, HIGH);
        digitalWrite(pinB, HIGH);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, HIGH);
        digitalWrite(pinE, HIGH);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, HIGH);
    }

5. Vous pouvez maintenant téléverser le code sur l'Arduino Uno R3, et vous verrez le chiffre 2 s'afficher sur l'afficheur 7 segments.

6. Si vous avez besoin d'afficher d'autres chiffres, comme de passer de 1 à 6, utiliser ``digitalWrite()`` pour définir chaque segment rendrait le code très long et la logique moins claire. Ici, nous utilisons une méthode de création de fonction.

7. Créez une fonction avec un paramètre - ``displayDigit()``, qui éteint d'abord tous les segments LED de l'afficheur 7 segments.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Éteindre tous les segments
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);
    }

8. Ensuite, contrôlez différents segments LED pour afficher les chiffres. Nous pourrions utiliser des instructions ``if-else``, mais cela pourrait être encombrant. Ainsi, une instruction ``switch`` offre une manière plus claire et organisée de choisir parmi plusieurs comportements possibles.

En programmation, une instruction ``switch`` est une structure de contrôle utilisée pour exécuter différents segments de code en fonction de la valeur d'une variable.

La syntaxe de base d'une instruction switch est généralement la suivante :

.. code-block:: Arduino

    switch (expression) {
        case value1:
            // code
            break;
        case value2:
            // code
            break;
        default:
            // code
    }

* ``expression`` : Il s'agit d'une expression qui renvoie généralement un entier ou un caractère, sur la base duquel l'instruction switch décide quel ``case`` exécuter.
* ``case`` : Chaque mot-clé ``case`` est suivi d'une valeur qui peut correspondre au résultat de l'``expression``. Si une correspondance est trouvée, le code est exécuté à partir de ce point jusqu'à ce qu'une instruction ``break`` soit rencontrée.
* ``break`` : L'instruction ``break`` est utilisée pour sortir du bloc ``switch``. Sans ``break``, le programme continuerait à exécuter le code du cas suivant, qu'il corresponde ou non, ce qui est connu sous le nom de "fall-through".
* ``default`` : La partie ``default`` est optionnelle et est exécutée si aucun ``case`` ne correspond, de manière similaire au ``else`` dans une structure ``if-else``.

.. image:: img/23_flow_swtich.png
    :align: center
    :width: 600

9. Utilisez le ``switch-case`` dans la fonction ``displayDigit()`` pour compléter l'affichage des chiffres sur l'afficheur 7 segments. Par exemple, pour afficher le chiffre 1, seuls les segments B et C doivent être allumés (HIGH) ; pour afficher le chiffre 2, les segments F et C doivent être éteints (LOW), tandis que les autres sont allumés.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Éteindre tous les segments
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Activer les segments nécessaires pour le chiffre désiré
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }


10. Vous pouvez maintenant appeler la fonction ``displayDigit()`` dans la fonction ``void loop()`` pour afficher des nombres spécifiques, par exemple en alternant entre 3 et 6 avec un intervalle d'une seconde.

.. code-block:: Arduino

    void loop() {

        displayDigit(3);  // Affiche le chiffre 3 sur l'afficheur 7 segments
        delay(1000);
        displayDigit(6);  // Affiche le chiffre 6 sur l'afficheur 7 segments
        delay(1000);
    }

11. Voici votre code complet. Vous pouvez maintenant téléverser le code sur l'Arduino Uno R3 et vous verrez l'afficheur 7 segments alterner entre 3 et 6.

.. code-block:: Arduino

    // Définir les broches connectées à l'afficheur 7 segments
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Configurer toutes les broches comme sorties
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {

        displayDigit(3);  // Affiche le chiffre 3 sur l'afficheur 7 segments
        delay(1000);
        displayDigit(6);  // Affiche le chiffre 6 sur l'afficheur 7 segments
        delay(1000);
    }

    void displayDigit(int digit) {
        // Éteindre tous les segments
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Activer les segments nécessaires pour afficher le chiffre (HIGH active les segments pour le cathode commun)
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }

Création du code - Cyber Dice
-------------------------------------
Maintenant que nous savons comment afficher les chiffres de 1 à 6 sur l'afficheur 7 segments, comment pouvons-nous réaliser l'effet d'un Cyber Dice ?

Cela implique d'appuyer sur un bouton pour faire défiler les chiffres de 1 à 6 et de relâcher le bouton pour afficher un nombre fixe. Voyons comment nous pouvons y parvenir avec du code.

1. Ouvrez le croquis que vous avez sauvegardé précédemment, ``Lesson23_Show_Number``.

2. Sélectionnez “Save As...” dans le menu “File” et renommez-le ``Lesson23_Cyber_Dice``. Cliquez sur "Save".

3. Définissez la broche du bouton et configurez-la en tant qu'entrée.

.. code-block:: Arduino
    :emphasize-lines: 10-11,23-24

    // Définir les broches connectées aux segments de l'afficheur 7 segments
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Définir la broche connectée au bouton
    int buttonPin = 9;

    void setup() {
        // Configurer toutes les broches comme sorties
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Configurer la broche du bouton comme entrée
        pinMode(buttonPin, INPUT);
    }

4. Vérifiez si le bouton est pressé au moment où la fonction ``void loop()`` s'exécute. Si le bouton n'est pas pressé, le code à l'intérieur du bloc ``if`` est ignoré.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // Vérifier si le bouton est pressé
        if (digitalRead(buttonPin) == HIGH) {
        }
    }

5. Dans la programmation avec Arduino ou d'autres microcontrôleurs, un problème courant lors de la gestion des entrées de boutons est de s'assurer que chaque pression déclenche une seule action, notamment lors de la génération d'événements ou de commandes (comme la génération d'un nombre aléatoire). Pour résoudre ce problème, nous pouvons utiliser une technique appelée "attente de relâchement".

**attente de relâchement**

L'idée centrale de cette méthode est qu'après avoir appuyé sur un bouton et exécuté une action, le programme entre dans une boucle qui continue de surveiller l'état du bouton jusqu'à ce qu'il soit relâché. Cela permet d'éviter que des actions supplémentaires ne soient déclenchées à cause de rebonds du bouton ou du fait que l'utilisateur maintient le bouton enfoncé.

Nous pouvons implémenter cela avec une boucle ``while`` dans le code.

.. image:: img/while_loop.png
    :width: 400
    :align: center

.. code-block:: Arduino
    :emphasize-lines: 4-6

    void loop() {
        // Vérifiez si le bouton est pressé
        if (digitalRead(buttonPin) == HIGH) {
            // Attendre que le bouton soit relâché avant de continuer
            while (digitalRead(buttonPin) == HIGH) {
            }
        }
    }

6. Maintenant, utilisez la fonction ``random()`` pour générer un nombre aléatoire entre 1 et 6, et utilisez ``displayDigit()`` pour afficher ce nombre sur l'afficheur 7 segments. Vous verrez l'afficheur défiler rapidement à travers différents nombres tant que le bouton est maintenu enfoncé.

.. code-block:: Arduino
    :emphasize-lines: 6-12

    void loop() {
        // Vérifiez si le bouton est pressé
        if (digitalRead(buttonPin) == HIGH) {
            // Attendre que le bouton soit relâché avant de continuer
            while (digitalRead(buttonPin) == HIGH) {
                // Générer un nombre aléatoire entre 1 et 6
                int num = random(1, 7);
                
                // Afficher le nombre aléatoire sur l'afficheur 7 segments
                displayDigit(num);
                // Pause pour permettre une mise à jour visible de l'afficheur
                delay(100);
            }
        }
    }

7. Enfin, ajoutez un délai pour anti-rebond afin d'éviter les entrées rapides multiples.

.. code-block:: Arduino
    :emphasize-lines: 15

    void loop() {
        // Vérifiez si le bouton est pressé
        if (digitalRead(buttonPin) == HIGH) {
            // Attendre que le bouton soit relâché avant de continuer
            while (digitalRead(buttonPin) == HIGH) {
                // Générer un nombre aléatoire entre 1 et 6
                int num = random(1, 7);
                
                // Afficher le nombre aléatoire sur l'afficheur 7 segments
                displayDigit(num);
                // Pause pour permettre une mise à jour visible de l'afficheur
                delay(100);
            }
            // Ajouter un délai pour anti-rebond et éviter les entrées rapides multiples
            delay(500);
        }
    }

8. Votre code complet devrait ressembler à ceci, et vous pouvez maintenant téléverser le code sur l'Arduino Uno R3. Une fois le code téléversé, si vous maintenez le bouton enfoncé, les nombres sur l'afficheur défileront rapidement, et en le relâchant, un nombre sera affiché.

.. code-block:: Arduino

    // Définir les broches connectées aux segments de l'afficheur 7 segments
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Définir la broche connectée au bouton
    int buttonPin = 9;

    void setup() {
        // Configurer toutes les broches comme sorties
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Configurer la broche du bouton comme entrée
        pinMode(buttonPin, INPUT);
    }

    void loop() {
        // Vérifiez si le bouton est pressé
        if (digitalRead(buttonPin) == HIGH) {
            // Attendre que le bouton soit relâché avant de continuer
            while (digitalRead(buttonPin) == HIGH) {
                // Générer un nombre aléatoire entre 1 et 6
                int num = random(1, 7);

                // Afficher le nombre aléatoire sur l'afficheur 7 segments
                displayDigit(num);
                // Pause pour permettre une mise à jour visible de l'afficheur
                delay(100);
            }
            // Ajouter un délai pour anti-rebond et éviter les entrées rapides multiples
            delay(500);
        }
    }

    void displayDigit(int digit) {
        // Éteindre tous les segments
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Allumer les segments nécessaires pour afficher le chiffre (LOW active les segments pour le cathode commun)
        switch (digit) {
            case 1:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            break;
            case 2:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 3:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 4:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 5:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 6:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
        }
    }

9. Enfin, n'oubliez pas de sauvegarder votre code et de ranger votre espace de travail.


**Résumé**

Dans cette leçon, nous avons complété avec succès le projet Cyber Dice, vous permettant de participer à des compétitions amicales avec vos amis pour voir qui peut obtenir le nombre le plus élevé. Tout au long de cette leçon, nous avons exploré le fonctionnement d'un afficheur 7 segments, appris à le contrôler efficacement. Nous avons simplifié notre code à l'aide des instructions switch-case, améliorant ainsi la lisibilité et l'efficacité.

De plus, nous avons mis en place une logique pour contrôler l'affichage des nombres aléatoires sur l'afficheur 7 segments en fonction de l'état d'une pression de bouton, ajoutant ainsi une interaction dynamique à notre projet. Cette expérience pratique vous familiarise non seulement avec des composants électroniques de base et des stratégies de codage, mais illustre également des applications pratiques de ces compétences dans la création de projets interactifs et engageants.

