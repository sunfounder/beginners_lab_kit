.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l'univers fascinant du Raspberry Pi, d'Arduino et d'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprenez et partagez** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des concours et à des promotions pendant les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

12. Les Couleurs de l'Arc-en-ciel
=======================================
Imaginez que vous puissiez peindre avec de la lumière, en mélangeant le rouge, le vert et le bleu pour créer toutes les nuances possibles, comme si vous mélangez des couleurs sur une palette, mais avec des faisceaux de lumière.

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

Bienvenue dans cette leçon, où vous allez explorer le monde captivant des LEDs RGB et découvrir comment la combinaison des couleurs primaires peut créer un spectre vibrant de nuances. Ce cours pratique vous guidera à travers les principes de fonctionnement des LEDs RGB et vous introduira aux applications pratiques de la programmation et de la construction de circuits.

Dans cette leçon, vous apprendrez à :

* Comprendre les principes de fonctionnement des LEDs RGB.
* Apprendre à créer et utiliser des fonctions dans votre code pour simplifier les tâches et améliorer la lisibilité.
* Explorer l'impact des différentes combinaisons de couleurs en manipulant la LED RGB.

Construction du Circuit
-----------------------------

**Composants nécessaires**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Résistance de 220Ω
     - Fils de connexion
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Câble USB
     - 1 * Breadboard
     - 1 * Multimètre
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter| 
     - 
     
**Instructions de construction étape par étape**

Suivez le schéma de câblage ou ces étapes pour construire le circuit.

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

1. Commencez avec une LED RGB.

Les LEDs RGB émettent de la lumière en différentes couleurs en intégrant des LEDs rouge, verte et bleue dans un seul boîtier. En variant la tension appliquée aux trois broches, ces LEDs peuvent produire jusqu'à 16 777 216 couleurs différentes.

.. image:: img/12_mix_color_rgb.png
    :width: 400
    :align: center

Selon leur conception, les LEDs RGB peuvent être à anode commune ou cathode commune. Pour ce projet, nous utilisons une LED RGB **à cathode commune**, où les trois LEDs partagent une connexion négative.

* Les LEDs RGB à cathode commune ont une connexion négative partagée.
* Les LEDs RGB à anode commune ont une connexion positive partagée.

.. image:: img/12_rgb_cc_ca.jpg
    :width: 600
    :align: center

Une LED RGB comporte généralement 4 broches ; la plus longue est la masse (GND). En plaçant la LED RGB, assurez-vous que la plus longue broche est la deuxième en partant de la gauche, en configurant les broches comme suit : Rouge, GND, Vert et Bleu de gauche à droite.

.. image:: img/12_mix_color_rgb_1.jpg
    :width: 200
    :align: center

Vous pouvez également utiliser un multimètre en mode test de diode pour identifier la couleur émise par chaque broche.

Réglez le multimètre sur le mode **Continuité** pour mesurer la résistance.

.. image:: img/multimeter_diode_measure.png
    :width: 300
    :align: center

Touchez la broche la plus longue de la LED RGB avec le fil noir du multimètre, puis touchez les autres broches individuellement avec le fil rouge. Vous verrez la LED RGB s'allumer en rouge, vert ou bleu en conséquence.

.. image:: img/12_mix_color_measure_pin.png
    :width: 500
    :align: center

2. Insérez la LED RGB dans la breadboard, avec la broche la plus longue dans le trou 17D, et les trois autres broches dans les trous 18C, 16C et 15C respectivement.

.. image:: img/12_mix_color_bb_1.png
    :width: 500
    :align: center

3. Insérez trois résistances de 220Ω comme indiqué, entre les trous 15E et 15G, 16E et 16G, et 18E et 18G.

.. image:: img/12_mix_color_bb_2.png
    :width: 500
    :align: center

4. Connectez ces résistances aux broches 9, 10 et 11 de l'Arduino Uno R3 à l'aide de fils de connexion comme illustré.

.. image:: img/12_mix_color_bb_3.png
    :width: 500
    :align: center

5. Connectez la broche la plus longue de la LED RGB à la masse (GND) à l'aide d'un fil de connexion.

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

Création du Code - Allumer une LED RGB
-------------------------------------------

1. Ouvrez l'IDE Arduino et démarrez un nouveau projet en sélectionnant « Nouveau Sketch » dans le menu « Fichier ».
2. Sauvegardez votre sketch sous le nom de ``Lesson12_Rainbow_Color`` en utilisant ``Ctrl + S`` ou en cliquant sur « Enregistrer ».

3. La LED dans votre circuit est connectée aux broches numériques de l'Arduino Uno R3. Comme la LED est un dispositif de sortie, vous devrez configurer les broches numériques 9, 10 et 11 comme ``OUTPUT``.

.. code-block:: Arduino
    :emphasize-lines: 3-5


    void setup() {
        // Code à exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB en sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB en sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB en sortie
    }

    void loop() {
        // Code à exécuter en boucle :
    }

4. Maintenant, dans la fonction ``void loop()``, réglez la broche rouge de la LED RGB sur ``HIGH``, et les deux autres broches sur ``LOW``.

.. note::

    Étant donné que nous utilisons les broches PWM 9, 10 et 11, vous avez la possibilité d'utiliser soit ``digitalWrite()``, soit ``analogWrite()`` pour définir un niveau haut ou bas.
    
    Pour cette leçon, comme nous définissons simplement les broches sur haut ou bas, nous utiliserons ``digitalWrite()``.

.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // Code à exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB en sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB en sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB en sortie
    }

    void loop() {
        // Code à exécuter en boucle :
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
    }

5. Enregistrez le code et cliquez sur « Téléverser » pour l'envoyer à votre Arduino Uno R3. Observons ce qui se passe.

6. Vous verrez la LED RGB s'allumer en rouge. Mais si vous voulez également allumer le vert et le bleu ? Comment devriez-vous modifier le code ?

Copiez maintenant les trois commandes ``digitalWrite()`` deux fois de plus. Réglez la broche que vous souhaitez afficher sur ``HIGH`` et les autres sur ``LOW``. Chaque couleur doit briller pendant une seconde.

.. code-block:: Arduino
    :emphasize-lines: 14-21

    void setup() {
        // Code à exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB en sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB en sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB en sortie
    }

    void loop() {
        // Code à exécuter en boucle :
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, HIGH);  // Allumer la broche verte de la LED RGB
        digitalWrite(11, LOW);   // Éteindre la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, LOW);   // Éteindre la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
    }

7. Téléversez à nouveau le code pour voir les effets. Vous verrez que la LED RGB passe en cycle entre le rouge, le vert et le bleu.

**Questions** :

1. Si vous voulez d'autres couleurs, que devriez-vous faire ? Consultez le schéma ci-dessous et remplissez vos idées dans votre manuel.

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

.. list-table::
   :widths: 20 20 20 20
   :header-rows: 1

   * - Couleur
     - Broche rouge
     - Broche verte
     - Broche bleue
   * - Rouge
     - *HIGH*
     - *LOW*
     - *LOW*
   * - Vert
     - *LOW*
     - *HIGH*
     - *LOW*
   * - Bleu
     - *LOW*
     - *LOW*
     - *HIGH*
   * - Jaune
     - 
     - 
     - 
   * - Rose
     - 
     - 
     - 
   * - Cyan
     - 
     - 
     - 
   * - Blanc
     - 
     - 
     - 

Création du Code - Créer des Fonctions
-------------------------------------------

Vous avez peut-être remarqué que pour afficher différentes couleurs séquentiellement sur la LED RGB, vous finissez par écrire de nombreuses lignes de code similaires. Par exemple, pour montrer sept couleurs différentes sur la LED RGB, vous écririez quelque chose comme ceci :

.. code-block:: Arduino

    void setup() {
        // Code à exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB en sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB en sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB en sortie
    }

    void loop() {
        // Code à exécuter en boucle :
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, HIGH);  // Allumer la broche verte de la LED RGB
        digitalWrite(11, LOW);   // Éteindre la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, LOW);   // Éteindre la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, LOW);   // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, HIGH);   // Allumer la broche verte de la LED RGB
        digitalWrite(11, HIGH);   // Allumer la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);   // Allumer la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, HIGH);   // Allumer la broche verte de la LED RGB
        digitalWrite(11, LOW);   // Éteindre la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, HIGH);   // Allumer la broche verte de la LED RGB
        digitalWrite(11, HIGH);   // Allumer la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
    }

Vous avez peut-être remarqué que votre fonction ``void loop()`` est devenue assez longue et que la logique est difficile à suivre. C'est donc le moment idéal pour introduire le concept de fonctions.

Tout au long de votre parcours de programmation, vous avez déjà utilisé des fonctions intégrées à Arduino comme ``pinMode()``, ``digitalWrite()``, et ``delay()``. Maintenant, nous allons plonger dans la création de fonctions personnalisées. Les fonctions personnalisées permettent de simplifier votre code, le rendant plus logique et plus facile à gérer.

Pour créer une fonction, il suffit de l'ajouter à la fin de votre sketch, après l'accolade de la fonction ``void loop()``. Comme ``void setup()`` et ``void loop()``, les fonctions commencent par ``void`` suivi d'un nom que vous choisissez. Les règles de nommage pour les fonctions sont similaires à celles pour les variables ou les constantes. Vous pouvez nommer une fonction comme vous le souhaitez, tant que ce n'est pas un mot-clé de l'IDE Arduino, et vous encadrez ses instructions entre accolades.

.. code-block:: Arduino
    :emphasize-lines: 9-11

    void setup() {
        ...
    }

    void loop() {
        ...
    }

    void lightRed(){
    
    }

1. À la fin de votre sketch, juste après l'accolade de la fonction ``void loop()``, nous allons ajouter sept nouvelles fonctions. Chaque fonction contiendra le code pour afficher une couleur spécifique sur la LED RGB.

.. code-block:: Arduino
    :emphasize-lines: 10-22

    void loop() {
        // placez ici le code qui doit s'exécuter en boucle :
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
        delay(1000);             // Attendre 1 seconde
        ...
    }

    void lightRed(){
    
    }

    void lightGreen(){
    
    }

    ...

    void lightWhite(){
    
    }

2. Ensuite, découpez les extraits de code spécifiques aux couleurs de la fonction ``void loop()`` et collez-les dans leurs fonctions respectives. Il ne restera plus que sept appels à ``delay()`` dans la fonction ``loop()``.

.. code-block:: Arduino

    ...

    void loop() {
        // placez ici le code qui doit s'exécuter en boucle :

        delay(1000);  // Attendre 1 seconde
        delay(1000);  // Attendre 1 seconde
        delay(1000);  // Attendre 1 seconde
        delay(1000);  // Attendre 1 seconde
        delay(1000);  // Attendre 1 seconde
        delay(1000);  // Attendre 1 seconde
        delay(1000);  // Attendre 1 seconde
    }

    void lightRed() {
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
    }
    ...

    void lightWhite() {
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, HIGH);  // Allumer la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
    }

3. Maintenant que les fonctions sont configurées, il est temps de les appeler dans la fonction ``void loop()``. Pour appeler une fonction, écrivez simplement son nom suivi de deux parenthèses et terminez la ligne par un point-virgule.

.. code-block:: Arduino
    :emphasize-lines: 7-22

    void setup() {
        // placez ici le code qui doit s'exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB en sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB en sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB en sortie
    }

    void loop() {
        // placez ici le code qui doit s'exécuter en boucle :
        lightRed();
        delay(1000);  // Attendre 1 seconde
        lightGreen();
        delay(1000);  // Attendre 1 seconde
        lightBlue();
        delay(1000);  // Attendre 1 seconde
        lightYellow();
        delay(1000);  // Attendre 1 seconde
        lightPink();
        delay(1000);  // Attendre 1 seconde
        lightCyan();
        delay(1000);  // Attendre 1 seconde
        lightWhite();
        delay(1000);  // Attendre 1 seconde
    }

    void lightRed() {
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
    }

    void lightGreen() {
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, HIGH);  // Allumer la broche verte de la LED RGB
        digitalWrite(11, LOW);   // Éteindre la broche rouge de la LED RGB
    }
    void lightBlue() {
        digitalWrite(9, HIGH);  // Allumer la broche bleue de la LED RGB
        digitalWrite(10, LOW);  // Éteindre la broche verte de la LED RGB
        digitalWrite(11, LOW);  // Éteindre la broche rouge de la LED RGB
    }
    void lightYellow() {
        digitalWrite(9, LOW);    // Éteindre la broche bleue de la LED RGB
        digitalWrite(10, HIGH);  // Allumer la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
    }
    void lightPink() {
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, LOW);   // Éteindre la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
    }
    void lightCyan() {
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, HIGH);  // Allumer la broche verte de la LED RGB
        digitalWrite(11, LOW);   // Éteindre la broche rouge de la LED RGB
    }
    void lightWhite() {
        digitalWrite(9, HIGH);   // Allumer la broche bleue de la LED RGB
        digitalWrite(10, HIGH);  // Allumer la broche verte de la LED RGB
        digitalWrite(11, HIGH);  // Allumer la broche rouge de la LED RGB
    }

4. Avec toutes les fonctions configurées et appelées dans la boucle, votre code est maintenant complet. Cliquez sur le bouton "Téléverser" pour transférer votre code sur l'Arduino Uno R3. Vous verrez la LED RGB passer en cycle entre rouge, vert, bleu, jaune, rose, cyan et blanc.

.. note::

    La luminosité de la LED RGB peut être assez intense, donc évitez de la regarder directement pendant de longues périodes pour éviter toute fatigue oculaire.

    Vous pourriez également envisager de diffuser la lumière avec un mouchoir ou un matériau dépoli pour adoucir l'intensité lumineuse.

**Résumé**

À travers une série d'exercices de codage, vous écrirez des sketches qui changent dynamiquement la couleur de la LED. En commençant par des commandes basiques pour contrôler chaque couleur, vous allez ensuite restructurer votre code en utilisant des fonctions, rendant votre configuration plus modulaire et facile à maintenir. Cette approche non seulement clarifie le code, mais vous enseigne aussi l'importance des fonctions en programmation.

