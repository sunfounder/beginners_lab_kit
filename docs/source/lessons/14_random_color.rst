.. note::

    Bonjour et bienvenue dans la communauté Facebook des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder ! Explorez plus en profondeur Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et à des promotions spéciales.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

14. Couleurs Aléatoires
===========================

Parfois, la vie a besoin d'une touche de surprise. Quand vous ne savez pas quelle couleur choisir, laissez le hasard décider ! Cette leçon vous montrera comment faire briller une LED RGB en couleurs aléatoires, parfait pour ajouter une étincelle imprévisible à vos projets.

Montage du circuit
-------------------------

**Composants nécessaires**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED RGB
     - 3 * Résistances de 220Ω
     - Fils de connexion
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * Câble USB
     - 1 * Plaque d'essai (breadboard)
     - 
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - 
     - 

Cette leçon utilise le même circuit que la leçon 12.

.. image:: img/12_mix_color_bb_4.png
    :width: 600
    :align: center

Création du code
---------------------

Dans les leçons précédentes, vous avez contrôlé la LED RGB pour afficher les couleurs de votre choix. Mais parfois, vous voudrez peut-être qu'elle affiche une couleur aléatoire, comme des lumières de scène. Comment cela peut-il être fait ?

**Comprendre les fonctions random()**

Dans le monde physique, le hasard est omniprésent, mais en programmation, les nombres dits "aléatoires" sont généralement calculés à l'aide d'un algorithme déterministe. Cet algorithme nécessite un point de départ appelé "graine" pour générer ces nombres. Ils sont donc dits "pseudo-aléatoires" car ils semblent aléatoires, mais suivent en réalité un modèle prévisible.

Sur un Arduino Uno R3, nous pouvons utiliser des mesures physiques comme source de hasard. Par exemple, des fluctuations mineures dans la tension et le courant d'un circuit peuvent servir de base à nos nombres pseudo-aléatoires.

Arduino propose plusieurs fonctions pour générer des nombres aléatoires :

* ``randomSeed();`` : Initialise la graine pour le générateur de nombres aléatoires. Cette fonction permet de s'assurer que la séquence de nombres varie à chaque exécution du programme.

    **Paramètres**
        * ``seed`` : Une valeur utilisée pour initialiser le générateur de nombres aléatoires.
    **Retourne**
        Aucun.

* ``long random(long max);`` : Génère un nombre aléatoire dans une plage spécifiée.

    **Paramètres**
        ``max`` : La limite supérieure du nombre aléatoire (excluant ``max``), ce qui signifie que le nombre généré sera compris entre 0 (inclus) et ``max-1`` (inclus).
    
    **Retourne**
        Un nombre de type long compris entre 0 et max-1.

* ``long random(long min, long max);`` : Génère un nombre aléatoire dans une plage spécifiée.

    **Paramètres**
        ``min`` : La limite inférieure du nombre aléatoire (incluse).
        ``max`` : La limite supérieure du nombre aléatoire (excluant ``max``).
    
    **Retourne**
        Un nombre de type long compris entre min et max-1.

**Écrire le code**

1. Ouvrez le sketch que vous avez sauvegardé précédemment, ``Lesson13_PWM_Color_Mixing``.

2. Cliquez sur "Enregistrer sous..." dans le menu "Fichier" et renommez-le en ``Lesson14_Random_Colors``. Cliquez sur "Enregistrer".

3. Appelez ``randomSeed()`` une seule fois dans ``void setup()`` pour initialiser la graine. Nous utilisons ``analogRead(A0)`` pour lire une valeur sur une broche analogique non connectée, qui capte le bruit aléatoire de l'environnement.

.. code-block:: Arduino
    :emphasize-lines: 9

    void setup() {
        // Code à exécuter une fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB en sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB en sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB en sortie
            
        // Initialiser la graine aléatoire avec une broche analogique non connectée
        randomSeed(analogRead(A0));
    }

4. Dans ``void loop()``, remplacez le code original par la fonction ``random()`` pour générer des valeurs aléatoires et les stocker dans les variables ``redValue``, ``greenValue`` et ``blueValue``.

.. code-block:: Arduino
    :emphasize-lines: 3-5

    void loop(){
        // Générer des valeurs aléatoires pour chaque composant de couleur
        int redValue = random(0, 256);   // Valeur aléatoire entre 0 et 255
        int greenValue = random(0, 256); // Valeur aléatoire entre 0 et 255
        int blueValue = random(0, 256);  // Valeur aléatoire entre 0 et 255
    }

5. Transmettez les valeurs RGB générées à la fonction ``setColor()``, et utilisez la fonction ``delay()`` pour déterminer la durée d'affichage de chaque couleur.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        // Générer des valeurs aléatoires pour chaque composant de couleur
        int redValue = random(0, 256);    // Valeur aléatoire pour le rouge
        int greenValue = random(0, 256);  // Valeur aléatoire pour le vert
        int blueValue = random(0, 256);   // Valeur aléatoire pour le bleu

        // Appliquer les valeurs aléatoires à la LED RGB
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // Attendre 1 seconde
    }

6. Votre code est maintenant prêt. Téléchargez-le sur l'Arduino Uno R3 et vous verrez la LED RGB afficher une couleur aléatoire toutes les secondes.

.. code-block:: Arduino
    :emphasize-lines: 19,20

    void setup() {
        // Code à exécuter une fois :
        pinMode(9, OUTPUT);   // Configurer la broche bleue de la LED RGB en sortie
        pinMode(10, OUTPUT);  // Configurer la broche verte de la LED RGB en sortie
        pinMode(11, OUTPUT);  // Configurer la broche rouge de la LED RGB en sortie
        
        // Initialiser la graine aléatoire avec une broche analogique non connectée
        randomSeed(analogRead(A0));
    }

    void loop() {
        // Générer des valeurs aléatoires pour chaque composant de couleur
        int redValue = random(0, 256);    // Valeur aléatoire pour le rouge
        int greenValue = random(0, 256);  // Valeur aléatoire pour le vert
        int blueValue = random(0, 256);   // Valeur aléatoire pour le bleu

        // Appliquer les valeurs aléatoires à la LED RGB
        setColor(redValue, greenValue, blueValue);
        delay(1000);  // Attendre 1 seconde
    }

    // Fonction pour définir la couleur de la LED RGB
    void setColor(int red, int green, int blue) {
        // Écrire la valeur PWM pour le rouge, le vert et le bleu sur la LED RGB
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

7. Enfin, n'oubliez pas de sauvegarder votre code et de ranger votre espace de travail.

**Question**

1. Si vous remplacez ``randomSeed(analogRead(A0))`` par ``randomSeed(0)``, comment les couleurs de la LED RGB vont-elles changer, et pourquoi ?

2. Dans quelles situations le hasard est-il utilisé pour résoudre des problèmes dans la vie quotidienne, en dehors du choix aléatoire de couleurs pour la décoration ou de la sélection des numéros de loterie ?

**Résumé**

À la fin de cette leçon, vous aurez non seulement appris à gérer l'aléatoire en programmation pour créer des affichages visuels dynamiques, mais vous aurez également acquis une nouvelle appréciation de la beauté simple de l'imprévisibilité dans la vie quotidienne. La programmation peut parfois être aussi imprévisible que la vie elle-même, et avec les bons outils, vous pouvez exploiter cette imprévisibilité de manière créative et fonctionnelle.
