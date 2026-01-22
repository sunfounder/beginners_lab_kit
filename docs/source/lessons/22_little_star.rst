.. note::

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et relevez les défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprenez & Partagez** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et à des avant-premières exclusives.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et concours** : Participez à des concours et à des promotions spéciales pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

22. Jouer "Ah! Vous dirai-je, Maman"
===========================================
Dans cette leçon, nous plongeons dans l'intersection fascinante entre la musique et la technologie. Vous apprendrez comment différentes hauteurs musicales sont produites par des changements de fréquence, et comment ce principe peut être appliqué à l'aide d'un microcontrôleur comme Arduino pour contrôler un buzzer. À la fin de cette leçon, vous comprendrez non seulement les bases des fréquences musicales, mais vous serez également capable de programmer un Arduino pour jouer une mélodie simple.

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/22_little_star.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

À la fin de cette leçon, vous serez capable de :

* Comprendre comment les hauteurs musicales correspondent à des fréquences spécifiques.
* Simplifier la programmation en utilisant des tableaux pour stocker et manipuler les notes de musique.
* Écrire et exécuter un programme qui contrôle un buzzer passif pour jouer "Ah! Vous dirai-je, Maman".

Fréquences musicales et production du son
---------------------------------------------
.. image:: img/7_sound.png
  :width: 400
  :align: center

Différents instruments de musique produisent des hauteurs variées en modifiant la fréquence.
Par exemple, sur un piano, le fait de frapper les touches fait vibrer les cordes correspondantes rapidement, produisant des hauteurs spécifiques.
Les scientifiques et les musiciens ont développé diverses méthodes d'accordage et des standards de hauteur en mesurant précisément ces fréquences de vibration.

Lorsque vous contrôlez un Arduino ou un autre microcontrôleur pour envoyer un signal électrique à un buzzer, le diaphragme de ce dernier vibre rapidement en fonction de la fréquence du signal,
produisant ainsi un son. Par exemple, un signal réglé à 440 Hz produira la hauteur musicale standard "A4", qui est un point de référence pour l'accordage musical.
À mesure que la fréquence augmente ou diminue, la hauteur du son produit monte ou descend, permettant ainsi de créer une gamme de hauteurs allant des graves aux aigus dans une composition musicale.

Dans la musique occidentale, une octave inclut 12 hauteurs (demi-tons), de C à B, puis revient à un C plus élevé.

Par exemple, la fréquence du Do central (généralement appelé C4) est d'environ 261,63 Hz. La fréquence d'une note peut être calculée à l'aide de la formule suivante :

.. image:: img/7_music_format.png

où f_0 est la hauteur de référence (généralement A4, fréquence 440Hz), et n est le nombre de demi-tons à partir de la hauteur de référence jusqu'à la hauteur cible (les nombres positifs indiquent une montée, les nombres négatifs une descente).
En utilisant cette formule, nous pouvons calculer la fréquence de n'importe quelle note.

Voici un ensemble de fréquences :

* C (C4) : 262 Hz (en réalité environ 261,63 Hz, arrondi à 262)
* D (D4) : 294 Hz
* E (E4) : 330 Hz
* F (F4) : 349 Hz
* G (G4) : 392 Hz
* A (A4) : 440 Hz
* B (B4) : 494 Hz

Nous allons maintenant explorer les secrets des notes avec Arduino et un buzzer. Faisons jouer au buzzer passif les deux premières lignes de "Ah! Vous dirai-je, Maman" :

.. note::

  La mélodie de "Ah! Vous dirai-je, Maman" repose sur des combinaisons de notes simples,
  et cette mélodie, rendue célèbre par Wolfgang Amadeus Mozart, est très appropriée pour les débutants.

  Voici la partition de base de "Ah! Vous dirai-je, Maman", avec chaque note :

  .. code-block:: 

    C C G G A A G
    F F E E D D C
    G G F F E E D
    G G F F E E D
    C C G G A A G
    F F E E D D C

Construction du circuit
--------------------------

**Composants nécessaires**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Plaque d'essai
     - 1 * Buzzer passif
     - Fils de connexion
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_passive_buzzer| 
     - |list_wire| 
   * - 1 * Câble USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 



**Étapes de construction**

Cette leçon utilise le même circuit que la leçon 21.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center

Création du Code - Tableau
-------------------------------
1. Ouvrez l'IDE Arduino et démarrez un nouveau projet en sélectionnant "New Sketch" dans le menu "Fichier".
2. Enregistrez votre sketch sous le nom ``Lesson22_Array`` en utilisant ``Ctrl + S`` ou en cliquant sur "Enregistrer".

3. Créez maintenant un tableau au tout début du code, stockant les notes de "Ah! Vous dirai-je, Maman" dans ce tableau.

.. code-block:: Arduino

  // Définir les fréquences pour les notes de la gamme de Do majeur (octave à partir du Do central)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // High C

  // Définir un tableau contenant la séquence des notes de la mélodie
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

Un tableau est une structure de données utilisée pour stocker plusieurs éléments du même type en programmation Arduino.
C'est un outil très basique mais puissant, et lorsqu'il est utilisé correctement, il peut considérablement améliorer l'efficacité et les performances du programme.
Les tableaux peuvent stocker des éléments de types tels que les entiers, les nombres à virgule flottante et les caractères.

Similaire à la création de variables et de fonctions, la création d'un tableau implique également de spécifier le type et le nom du tableau - ``int melody[]``.

Les éléments à l'intérieur des ``{}`` sont appelés éléments de tableau, commençant à l'index 0, donc ``melody[0]`` correspond au premier ``c(262)``, et ``melody[13]`` est également ``c(262)``.

4. Imprimez maintenant les éléments aux index 0 et 13 du tableau ``melody[]`` dans le moniteur série.

.. code-block:: Arduino
  :emphasize-lines: 17,18

  // Définir les fréquences pour les notes de la gamme de Do majeur (octave à partir du Do central)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Do aigu

  // Définir un tableau contenant la séquence des notes de la mélodie
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

  void setup() {
    // Mettez ici votre code de configuration, exécuté une seule fois :
    Serial.begin(9600);  // Initialiser la communication série à 9600 baud
    Serial.println(melody[0]);
    Serial.println(melody[13]);
  }
  
  void loop() {
    // Mettez ici votre code principal, exécuté en boucle :
  }

5. Après avoir téléversé le code sur l'Arduino Uno R3, ouvrez le moniteur série et vous verrez deux fois le nombre 262.

.. code-block::

  262
  262

6. Si vous souhaitez imprimer chaque élément du tableau ``melody[]`` un par un, vous devrez d'abord connaître la longueur du tableau. Vous pouvez utiliser la fonction ``sizeof()`` pour calculer le nombre d'éléments dans le tableau.

.. code-block:: Arduino
  :emphasize-lines: 4

  void setup() {
    // Mettez ici votre code de configuration, exécuté une seule fois :
    Serial.begin(9600);  // Initialiser la communication série à 9600 baud
    int notes = sizeof(melody) / sizeof(melody[0]); // Calculer le nombre d'éléments
  }

  
* ``sizeof(melody)`` donne le nombre total d'octets utilisés par tous les éléments du tableau.
* ``sizeof(melody[0])`` donne le nombre d'octets utilisés par un seul élément du tableau.
* Diviser le nombre total d'octets par le nombre d'octets par élément donne le nombre total d'éléments dans le tableau.

7. Ensuite, utilisez une instruction ``for`` pour parcourir les éléments du tableau ``melody[]``, et les imprimer à l'aide de la fonction ``Serial.println()``.

.. code-block:: Arduino

  // Définir les fréquences pour les notes de la gamme de Do majeur (octave à partir du Do central)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Do aigu

  // Définir un tableau contenant la séquence des notes de la mélodie
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };


  void setup() {
    // Mettez ici votre code de configuration, exécuté une seule fois :
    Serial.begin(9600);                              // Initialiser la communication série à 9600 baud
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calculer le nombre d'éléments
    // Boucler à travers chaque note du tableau melody
    for (int i = 0; i < notes; i = i + 1) {
      // Imprimer la fréquence de chaque note dans le moniteur série
      Serial.println(melody[i]);
    }
  }

  void loop() {
    // Mettez ici votre code principal, exécuté en boucle :
  }

8. Après avoir téléversé le code sur l'Arduino Uno R3, ouvrez le moniteur série et vous verrez les éléments du tableau ``melody[]`` imprimés un par un.

.. code-block::

  262
  262
  392
  392
  440
  440
  392
  349
  349
  330
  ...

**Questions**

Vous pouvez également effectuer des opérations sur les éléments du tableau, par exemple en changeant pour ``Serial.println(melody[i] * 1.3);`` Quels types de données obtiendrez-vous et pourquoi ?


Création du Code - Jouer "Ah! Vous dirai-je, Maman"
------------------------------------------------------

Maintenant que nous comprenons bien comment créer des tableaux, accéder aux éléments du tableau et calculer leur longueur ainsi que leurs opérations, appliquons cette connaissance pour programmer un buzzer passif à jouer "Ah! Vous dirai-je, Maman" en utilisant des fréquences et des intervalles stockés.

1. Ouvrez le sketch que vous avez sauvegardé précédemment, ``Lesson22_Array``.

2. Cliquez sur “Enregistrer sous...” dans le menu "Fichier", et renommez-le en ``Lesson22_Little_Star``. Cliquez sur "Enregistrer".

3. Tout d'abord, définissez la broche du buzzer.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Assigne la broche 9 à la constante pour le buzzer


4. Créez maintenant un autre tableau pour stocker la durée des notes.

.. code-block:: Arduino
  :emphasize-lines: 3

  // Configurer la séquence des notes et leurs durées en millisecondes
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

5. Déplacez maintenant une partie du code de ``void setup()`` vers ``void loop()``.

.. code-block:: Arduino
  :emphasize-lines: 8-13

  void setup() {
    // Mettez ici votre code de configuration, exécuté une seule fois :
    Serial.begin(9600);                              // Initialiser la communication série à 9600 baud
  }

  void loop() {
    // Mettez ici votre code principal, exécuté en boucle :
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calculer le nombre d'éléments
    // Boucle à travers chaque note du tableau melody
    for (int i = 0; i < notes; i = i + 1) {
      // Imprimer la fréquence de chaque note dans le moniteur série
      Serial.println(melody[i]);
    }
  }

6. Dans l'instruction ``for``, commentez le code d'impression et utilisez la fonction ``tone()`` pour jouer les notes.

.. code-block:: Arduino
  :emphasize-lines: 9

  void loop() {
    // Mettez ici votre code principal, exécuté en boucle :
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calculer le nombre d'éléments
    // Boucle à travers chaque note du tableau melody
    for (int i = 0; i < notes; i = i + 1) {
      // Imprimer la fréquence de chaque note dans le moniteur série
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Jouer la note
    }
  }

7. Après chaque note jouée, pour rendre la mélodie plus naturelle, ajoutez une courte pause entre deux notes. Ici, nous multiplions la durée des notes par 1,30 pour calculer l'intervalle, afin que la mélodie ne semble pas trop précipitée.

.. code-block:: Arduino
  :emphasize-lines: 10

  void loop() {
    // Mettez ici votre code principal, exécuté en boucle :
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calculer le nombre d'éléments
    // Boucle à travers chaque note du tableau melody
    for (int i = 0; i < notes; i = i + 1) {
      // Imprimer la fréquence de chaque note dans le moniteur série
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Jouer la note
      delay(noteDurations[i] * 1.30);                // Attendre avant de changer la note
    }
  }

8. Utilisez la fonction ``noTone()`` pour arrêter la sortie du son sur la broche actuelle. C'est une étape nécessaire pour s'assurer que chaque note est jouée clairement sans se fondre dans la suivante.

.. code-block:: Arduino
  :emphasize-lines: 11

  void loop() {
    // Mettez ici votre code principal, exécuté en boucle :
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calculer le nombre d'éléments
    // Boucle à travers chaque note du tableau melody
    for (int i = 0; i < notes; i = i + 1) {
      // Imprimer la fréquence de chaque note dans le moniteur série
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Jouer la note
      delay(noteDurations[i] * 1.30);                // Attendre avant de changer la note
      noTone(buzzerPin);                             // Arrêter de jouer la note
    }
  }

9. Voici votre code complet, et une fois que vous aurez téléversé le code sur l'Arduino Uno R3, vous pourrez entendre le buzzer jouer "Ah! Vous dirai-je, Maman".

.. code-block:: Arduino

  int buzzerPin = 9;  // Assigne la broche 9 à la constante pour le buzzer

  // Définir les fréquences des notes de la gamme de Do majeur (octave à partir du Do central)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Do aigu

  // Configurer la séquence des notes et leurs durées en millisecondes
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

  void setup() {
    // Mettez ici votre code de configuration, exécuté une seule fois :
    Serial.begin(9600);                              // Initialiser la communication série à 9600 baud
  }

  void loop() {
    // Mettez ici votre code principal, exécuté en boucle :
    int notes = sizeof(melody) / sizeof(melody[0]);  // Calculer le nombre d'éléments
    // Boucle à travers chaque note du tableau melody
    for (int i = 0; i < notes; i = i + 1) {
      // Imprimer la fréquence de chaque note dans le moniteur série
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Jouer la note
      delay(noteDurations[i] * 1.30);                // Attendre avant de changer la note
      noTone(buzzerPin);                             // Arrêter de jouer la note
    }
  }
  
10. Enfin, n'oubliez pas de sauvegarder votre code et de ranger votre espace de travail.

**Question**

Si vous remplacez le buzzer passif par un buzzer actif dans le circuit, pourrez-vous jouer "Ah! Vous dirai-je, Maman" correctement ? Pourquoi ?

**Résumé**

Maintenant que la leçon est terminée, nous avons appris à utiliser des tableaux pour stocker des données, calculer la longueur d'un tableau, indexer des éléments dans un tableau et effectuer des opérations sur chaque élément. En stockant les fréquences des notes et les intervalles de temps dans des tableaux et en les parcourant avec une boucle for, nous avons réussi à programmer un buzzer passif pour jouer "Ah! Vous dirai-je, Maman".

De plus, nous avons appris à interrompre la lecture d'une note à l'aide de la fonction ``noTone()``.

Cette leçon a renforcé notre compréhension des opérations sur les tableaux et des structures de contrôle en programmation, tout en démontrant comment ces concepts peuvent être appliqués pour créer de la musique avec des composants électroniques, reliant ainsi des connaissances théoriques à des applications pratiques de manière ludique et engageante.

