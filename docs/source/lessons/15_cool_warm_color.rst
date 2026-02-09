.. note::

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Recevez en avant-première des annonces de nouveaux produits.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et à des promotions spéciales.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

15. Couleurs Chaudes ou Froides
====================================

Les couleurs ne sont pas seulement une partie de notre expérience visuelle, elles influencent également nos émotions et nos sentiments. Dans cette leçon, nous explorerons les impacts psychologiques des couleurs et apprendrons à manipuler une LED RGB pour basculer entre des couleurs chaudes et froides, imitant les effets de températures lumineuses changeantes.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/15_cool_warm_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

**Aperçu**

Le concept des couleurs chaudes et froides se réfère aux effets psychologiques que les couleurs ont sur notre perception. Les rouges, oranges, jaunes et bruns évoquent généralement des sentiments de chaleur et d'excitation, les classant comme des couleurs chaudes. Inversement, les verts, bleus et violets apportent souvent des sentiments de calme et de fraîcheur, les faisant considérer comme des couleurs froides. L'orange et le bleu se trouvent aux extrémités opposées de ce spectre chaud-froid.

.. image:: img/15_mix_color_warm_cool.png
    :width: 400
    :align: center

À la maison ou dans les environnements de détente, les gens préfèrent souvent des éclairages dans des teintes de jaune clair ou de blanc cassé, créant une atmosphère chaleureuse semblable à la lumière du coucher de soleil ou à la lumière des bougies.

.. image:: img/15_mix_color_warm_room.png
    :width: 400
    :align: center

Dans les bibliothèques, les salles de classe, les bureaux et les hôpitaux, des tons de lumière plus froids sont favorisés car ils favorisent la concentration et la fraîcheur, ce qui est propice au travail et à l'apprentissage.

.. image:: img/15_mix_color_cool_room.png
    :width: 400
    :align: center

La chaleur ou la fraîcheur de la lumière est une expérience viscérale qui affecte notre réponse psychologique et notre confort visuel. Les designers et ingénieurs en éclairage choisissent soigneusement les températures de couleur adaptées à la fonction d'un espace et à l'ambiance souhaitée, créant ainsi des environnements à la fois esthétiques et pratiques. En appliquant ces principes de manière scientifique, nous pouvons améliorer la qualité de nos environnements de vie et de travail, favorisant ainsi une atmosphère plus saine et confortable.

Dans cette leçon, nous allons jouer le rôle d'ingénieurs en éclairage pour créer un système capable de basculer entre différentes températures de couleur.

**Objectifs d'apprentissage**

- Comprendre les effets psychologiques des couleurs chaudes et froides.
- Explorer comment les températures lumineuses affectent l'humeur et l'ambiance.
- Apprendre à ajuster les couleurs d'une LED RGB pour simuler différentes températures à l'aide d'Arduino.
- Développer des compétences pratiques en utilisant la fonction ``map()`` pour passer d'une température de couleur à une autre.

Montage du circuit
------------------------

**Composants nécessaires**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Résistances de 220Ω
     - 1 * Potentiomètre
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * Câble USB
     - 1 * Plaque d'essai (breadboard)
     - Fils de connexion
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - 

**Étapes de montage**

Ce circuit est une extension de celui de la leçon 12 en y ajoutant un potentiomètre.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center

1. Retirez le fil reliant la broche GND de l'Arduino Uno R3 à la broche GND de la LED RGB, puis insérez-le dans la borne négative de la plaque d'essai. Connectez ensuite un fil entre la borne négative et la broche GND de la LED RGB.

.. image:: img/15_cool_warm_color_gnd.png
    :width: 500
    :align: center

2. Insérez le potentiomètre dans les trous 25G, 26F et 27G.

.. image:: img/15_cool_warm_color_pot.png
    :width: 500
    :align: center

3. Connectez la broche centrale du potentiomètre à la broche A0 de l'Arduino Uno R3.

.. image:: img/15_cool_warm_color_a0.png
    :width: 500
    :align: center

4. Enfin, connectez la broche gauche du potentiomètre à la broche 5V de l'Arduino Uno R3 et la broche droite à la borne négative de la plaque d'essai.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center

Création du code
----------------------

**Comprendre les couleurs chaudes et froides**

Avant d'ajuster la température de couleur, nous devons comprendre les différences entre les valeurs RGB pour les couleurs chaudes et froides.

La perception de la chaleur dans l'éclairage est quelque peu subjective, mais il est indéniable que les couleurs chaudes doivent tendre vers l'orange-rouge, tandis que les couleurs froides doivent tirer vers le bleu.

1. Ouvrez **Paint** ou tout autre outil de sélection de couleurs, trouvez les couleurs que vous considérez comme les plus chaudes et les plus froides, et notez leurs valeurs RGB dans votre cahier.

.. note::

    Avant de sélectionner une couleur, ajustez les lumens à la position appropriée.

.. list-table::
   :widths: 25 25 50 25
   :header-rows: 1

   * - Type de couleur
     - Rouge
     - Vert
     - Bleu
   * - Couleur chaude
     - 
     - 
     - 
   * - Couleur froide
     - 
     - 
     - 

2. Voici des exemples de tons chauds et froids avec leurs valeurs RGB :

* Rouge (Rouge : 246, Vert : 52, Bleu : 8)

.. image:: img/15_mix_color_tone_warm.png

* Bleu clair (Rouge : 100, Vert : 150, Bleu : 255)

.. image:: img/15_mix_color_tone_cool.png

La principale différence entre les couleurs chaudes et froides réside dans le rapport des intensités des trois couleurs primaires. Ensuite, nous allons stocker ces valeurs RGB dans notre sketch.

3. Ouvrez le sketch que vous avez enregistré précédemment, ``Lesson13_PWM_Color_Mixing``.

4. Cliquez sur « Enregistrer sous... » dans le menu « Fichier », et renommez-le en ``Lesson15_Cool_Warm_Color``. Cliquez sur "Enregistrer".

5. Avant la fonction ``void setup()``, déclarez six variables pour stocker les valeurs RGB de ces deux couleurs. Utilisez les couleurs que vous avez sélectionnées.

.. code-block:: Arduino
    :emphasize-lines: 1-4,6-9

    // Valeurs RGB pour une couleur chaude
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // Valeurs RGB pour une couleur froide
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Configuration initiale à exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB comme sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB comme sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB comme sortie
    }

**Utilisation de la fonction map()**

Pour passer de l’éclairage chaud à l’éclairage froid, il suffit de réduire l’intensité de la lumière rouge, d’augmenter celle de la lumière bleue et d’ajuster finement l’intensité de la lumière verte.

Dans les projets précédents, nous avons appris à faire varier la luminosité de la LED en fonction de la rotation du potentiomètre.

Cependant, dans ce projet, la rotation du potentiomètre modifie l'intensité des broches RGB dans une plage spécifique, ce qui rend la simple division inadéquate pour nos besoins. C'est pourquoi nous avons besoin de la fonction ``map()``.

En programmation Arduino, la fonction ``map()`` est très utile car elle permet de convertir une plage de nombres en une autre.

Voici comment l'utiliser :

* ``map(value, fromLow, fromHigh, toLow, toHigh)`` : Re-map une valeur d'une plage de nombres à une autre. Par exemple, une valeur de ``fromLow`` sera mappée à ``toLow``, une valeur de ``fromHigh`` sera mappée à ``toHigh``, et les valeurs intermédiaires seront mappées en conséquence.

    **Paramètres**
        * ``value`` : le nombre à mapper.
        * ``fromLow`` : la borne inférieure de la plage actuelle de ``value``.
        * ``fromHigh`` : la borne supérieure de la plage actuelle de ``value``.
        * ``toLow`` : la borne inférieure de la plage cible.
        * ``toHigh`` : la borne supérieure de la plage cible.

    **Retourne**
        La valeur remappée. Type de donnée : long.

La fonction ``map()`` ajuste une valeur d'une plage donnée (de fromLow à fromHigh) à une nouvelle plage (de toLow à toHigh). Elle calcule d'abord la position de ``value`` dans sa plage d'origine, puis applique la même proportion pour l'adapter à la nouvelle plage.

.. image:: img/15_map_pic.png
    :width: 400
    :align: center

Ainsi, cela peut être représenté par la formule suivante :

.. code-block::

    (value-fromLow)/(fromHigh-fromLow) = (y-toLow)/(toHigh-toLow)

En utilisant l'algèbre, vous pouvez réarranger cette équation pour résoudre ``y`` :

.. code-block::

    y = (value-fromLow) * (toHigh-toLow) / (fromHigh-fromLow) + toLow

.. image:: img/15_map_format.png

Par exemple, en utilisant ``y = map(value, 0, 1023, 246, 100);``, si ``value`` est égal à 434, alors ``y = (434-0) * (100 - 246) / (1023-0) + 246``, ce qui équivaut approximativement à 152.


6. Supprimez le code d'origine dans ``void loop()``, puis écrivez un code pour lire la valeur du potentiomètre et la stocker dans la variable ``potValue``.

.. code-block:: Arduino

    void loop() {
        // Code principal à exécuter en boucle :
        int potValue = analogRead(A0);                         // Lire la valeur du potentiomètre
    }

7. Ensuite, utilisez la fonction ``map()`` pour mapper la valeur du potentiomètre de la plage 0~1023 à la plage 255 (``warm_r``) ~ 100 (``cool_r``).

.. code-block:: Arduino

    void loop() {
        // Code principal à exécuter en boucle :
        int potValue = analogRead(A0);                         // Lire la valeur du potentiomètre
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mapper la valeur du potentiomètre à l'intensité rouge
    }

8. Vous pouvez utiliser le moniteur série pour afficher la ``potValue`` et la valeur mappée ``value_r`` pour approfondir votre compréhension de la fonction ``map()``. Activez maintenant le moniteur série dans ``void setup()``.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Configuration initiale à exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB comme sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB comme sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB comme sortie
        Serial.begin(9600);   // Configurer la communication série à 9600 bauds
    }

9. Affichez les variables ``potValue`` et ``value_r`` sur la même ligne, séparées par un "|".

.. code-block:: Arduino
    :emphasize-lines: 23-26

    // Valeurs RGB pour une couleur chaude
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // Valeurs RGB pour une couleur froide
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Configuration initiale à exécuter une seule fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB comme sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB comme sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB comme sortie
        Serial.begin(9600);   // Configurer la communication série à 9600 bauds
    }

    void loop() {
        // Code principal à exécuter en boucle :
        int potValue = analogRead(A0);                         // Lire la valeur du potentiomètre
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mapper la valeur du potentiomètre à l'intensité rouge
        Serial.print(potValue);
        Serial.print(" | ");
        Serial.println(value_r);
        delay(500);  // Attendre 500ms
    }

    // Fonction pour régler la couleur de la LED RGB
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // Appliquer la PWM à la broche rouge
        analogWrite(10, green);  // Appliquer la PWM à la broche verte
        analogWrite(9, blue);    // Appliquer la PWM à la broche bleue
    }

10. Vous pouvez maintenant vérifier et téléverser votre code, ouvrir le moniteur série, et vous verrez deux colonnes de données imprimées.

.. code-block::

    434 | 152
    435 | 152
    434 | 152
    434 | 152
    434 | 152
    434 | 152

À partir des données, il est évident que la position de la valeur 434 dans la plage 0~1023 correspond à la position de 152 dans la plage 246~100.

**Ajuster la température de couleur**

Ici, nous utilisons la fonction ``map()`` pour ajuster l'intensité des trois broches 
de la LED RGB en fonction de la rotation du potentiomètre, passant des teintes les plus 
chaudes aux plus froides. Plus précisément, avec les valeurs de référence fournies, 
lorsque le potentiomètre est tourné, la valeur R de la LED RGB passera progressivement 
de 246 à 100, la valeur G de 8 à 150 (bien que le changement de la valeur G ne soit 
pas très visible), et la valeur B de 8 à 255.

11. Ensuite, nous n'avons plus besoin de l'impression série temporairement, et l'impression 
série peut affecter l'ensemble du processus du code, alors utilisez ``Ctrl + /`` pour commenter le code concerné.

    .. note::

        La raison pour ne pas supprimer directement est que si vous devez imprimer ultérieurement, vous n'aurez pas besoin de réécrire le code ; il suffit de sélectionner ces lignes et d'appuyer sur ``Ctrl+/`` pour les décommenter.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // code principal à exécuter en boucle :
        int potValue = analogRead(A0);                         // Lire la valeur du potentiomètre
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mapper la valeur du potentiomètre à l'intensité rouge
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Attendre 500ms
    }

12. Continuez à appeler la fonction ``map()``, pour obtenir les valeurs mappées ``value_g`` et ``value_b`` en fonction de la valeur du potentiomètre.

.. code-block:: Arduino
    :emphasize-lines: 9,10

    void loop() {
        // put your main code here, to run repeatedly:
        int potValue = analogRead(A0);                         // Read value from potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Map pot value to red intensity
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Wait for 500ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Map pot value to green intensity
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Map pot value to blue intensity
    }

13. Enfin, appelez la fonction ``setColor()`` pour afficher les valeurs RGB mappées sur la LED RGB.

.. code-block:: Arduino
    :emphasize-lines: 11,12

    void loop() {
        // put your main code here, to run repeatedly:
        int potValue = analogRead(A0);                         // Read value from potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Map pot value to red intensity
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Wait for 500ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Map pot value to green intensity
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Map pot value to blue intensity
        setColor(value_r, value_g, value_b);                   // Set LED color
        delay(500);
    }

14. Votre code complet est le suivant ; vous pouvez cliquer sur le bouton Téléverser pour transférer le code sur l'Arduino Uno R3. Ensuite, vous pourrez tourner le potentiomètre et vous remarquerez que la LED RGB passe progressivement d'une teinte froide à une teinte chaude, ou d'une teinte chaude à une teinte froide.

.. code-block:: Arduino

    // Valeurs RGB pour une couleur chaude
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // Valeurs RGB pour une couleur froide
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);   // Set Blue pin of RGB LED as output
        pinMode(10, OUTPUT);  // Set Green pin of RGB LED as output
        pinMode(11, OUTPUT);  // Set Red pin of RGB LED as output
    }

    void loop() {
        // put your main code here, to run repeatedly:
        int potValue = analogRead(A0);                         // Read value from potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Map pot value to red intensity
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Wait for 500ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Map pot value to green intensity
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Map pot value to blue intensity
        setColor(value_r, value_g, value_b);                   // Set LED color
        delay(500);                                            // Wait for 500ms
    }

    // Function to set the color of the RGB LED
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // Write PWM to red pin
        analogWrite(10, green);  // Write PWM to green pin
        analogWrite(9, blue);    // Write PWM to blue pin
    }

15. Enfin, n'oubliez pas de sauvegarder votre code et de ranger votre espace de travail.

**Conseils**

Pendant l'expérience, vous pourriez remarquer que la transition entre les teintes chaudes et froides n'est pas aussi apparente qu'à l'écran ; par exemple, une lumière censée être chaude peut sembler blanche. C'est normal, car le mélange des couleurs dans une LED RGB n'est pas aussi précis que sur un écran.

Dans ce cas, vous pouvez réduire l'intensité des valeurs G et B dans la couleur chaude pour que la LED RGB affiche une couleur plus appropriée.

**Question**

Notez que les "bornes inférieures" de chaque plage peuvent être plus grandes ou plus petites que les "bornes supérieures", donc la fonction ``map(value, fromLow, fromHigh, toLow, toHigh)`` peut être utilisée pour inverser une plage de nombres, par exemple :

.. code-block::

    y = map(x, 1, 50, 50, 1);

La fonction gère également bien les nombres négatifs, de sorte que cet exemple est également valide et fonctionne bien.

.. code-block::

    y = map(x, 1, 50, 50, -100);

Pour ``y = map(x, 1, 50, 50, -100);``, si ``x`` est égal à 20, quelle devrait être la valeur de ``y`` ? Référez-vous à la formule suivante pour le calculer.

.. image:: img/15_map_format.png

