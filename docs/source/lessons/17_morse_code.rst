.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez plus profondément dans le monde du Raspberry Pi, d'Arduino et d'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits et aux avant-goûts.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des concours et à des promotions pendant les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

17. Code Morse
========================

Le code Morse est comme un langage secret utilisant des points (.) et des traits (-), inventé par Samuel Morse dans les années 1840. Il a été créé pour envoyer des messages sur de longues distances à l'aide de télégraphes. Chaque lettre de l'alphabet et chaque chiffre sont représentés par une combinaison unique de ces signaux. Par exemple, le message en code Morse le plus célèbre est "SOS" (··· ––– ···), qui est un signal international de détresse. Le code Morse était essentiel pour la communication avant l'invention des téléphones et d'Internet, et il était particulièrement populaire chez les opérateurs de navires et d'avions. Aujourd'hui, c'est amusant à apprendre pour envoyer des messages secrets à vos amis !

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/17_morse_code.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Dans cette leçon, vous apprendrez :

* Comprendre le fonctionnement d'un buzzer actif.
* Apprendre à coder le signal SOS en code Morse, ce qui vous permettra d'envoyer des messages en code Morse à l'aide d'un buzzer.


La magie du code Morse !
----------------------------

.. image:: img/7_morse.jpeg

Imaginez inventer une méthode pour envoyer des messages secrets en utilisant simplement des points et des traits ! C'est ce que Samuel Morse a fait en 1836 avec le code Morse. Initialement peintre, Morse s'est inspiré lors d'un voyage en bateau et plus tard, avec son ami Alfred Vail, a créé le télégraphe pour envoyer des messages à travers des fils.

Le code Morse utilise des points (signaux courts) et des traits (signaux longs) pour représenter des lettres et des chiffres. Le premier message en code Morse ? "What hath God wrought" — envoyé en 1844 de Washington D.C. à Baltimore, lançant l'ère du télégraphe.

Aujourd'hui, le code Morse est moins utilisé, mais il reste cool pour des domaines comme l'aviation et par les amateurs de radio. Maintenant, explorons comment fonctionne le code Morse avec Arduino et un buzzer et amusons-nous avec cette partie de l'histoire de la communication !


Construire le circuit
----------------------

**Composants nécessaires**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Buzzer actif
     - 1 * Plaque d'essai (breadboard)
     - Câbles de connexion
   * - |list_uno_r3| 
     - |list_active_buzzer| 
     - |list_breadboard| 
     - |list_wire| 
   * - 1 * Câble USB
     - 
     - 
     - 
   * - |list_usb_cable| 
     - 
     - 
     - 


**Instructions de montage**

1. Trouvez un buzzer actif qui possède généralement un autocollant blanc à l'avant et un dos noir scellé.

.. image:: img/7_beep_2.png

Les buzzers, en tant que dispositifs sonores électroniques, ont une histoire riche qui remonte au XIXe siècle. Le précurseur des buzzers modernes trouve son origine en 1831, lorsque Michael Faraday découvrit l'induction électromagnétique, formant ainsi le principe fondamental derrière le fonctionnement des buzzers électromagnétiques. Suite à cette découverte révolutionnaire, de nombreux scientifiques et inventeurs ont exploré comment appliquer les théories électromagnétiques à des dispositifs pratiques. Aujourd'hui, les buzzers se divisent en deux catégories : les buzzers actifs et passifs.

**Buzzer actif**

.. image:: img/7_beep_ac.png
    :width: 300
    :align: center

Scellés à l'arrière, les buzzers actifs contiennent un oscillateur interne qui émet un son lorsqu'ils sont alimentés, produisant généralement un bip monotone.

**Buzzer passif**

.. image:: img/7_beep_pa.png
    :width: 300
    :align: center

Ouverts à l'arrière, les buzzers passifs nécessitent un signal de fréquence externe d'un microcontrôleur pour générer du son, ce qui permet de produire une gamme de tonalités.

1. Le buzzer actif est également un dispositif polarisé. Le côté avant porte un signe "+" indiquant sa borne positive (anode), qui est également la broche la plus longue. Insérez maintenant le buzzer dans la plaque d'essai avec l'anode dans le trou 15F et la cathode dans le trou 18F.

.. image:: img/16_morse_code_buzzer.png
    :width: 500
    :align: center

2. Connectez la cathode à la broche GND de l'Arduino Uno R3.

.. image:: img/16_morse_code_gnd.png
    :width: 500
    :align: center

3. Si vous insérez l'anode du buzzer dans la broche 5V de l'Arduino Uno R3, vous entendrez le buzzer actif émettre un son directement. Bien sûr, vous pouvez également utiliser cette méthode pour vérifier si le buzzer est correct. Un buzzer passif ne produira pas de son lorsqu'il est directement connecté à une source d'alimentation.

.. image:: img/16_morse_code_5v.png
    :width: 500
    :align: center

4. Maintenant, retirez le fil inséré dans la broche 5V et insérez-le dans la broche 9 de l'Arduino Uno R3, afin que le buzzer puisse être contrôlé par le code.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center

Création du code
---------------------
1. Ouvrez l'IDE Arduino et commencez un nouveau projet en sélectionnant « Nouveau Sketch » dans le menu « Fichier ».
2. Sauvegardez votre sketch sous le nom ``Lesson17_Morse_Code`` en utilisant ``Ctrl + S`` ou en cliquant sur « Sauvegarder ».

3. Tout d'abord, créez une constante appelée ``buzzerPin`` et attribuez-lui la valeur de la broche 9.

.. code-block:: Arduino
    :emphasize-lines: 1

    const int buzzerPin = 9;   // Assigne la broche 9 à la constante pour le buzzer

    void setup() {
        // Configurez ici votre code pour qu'il s'exécute une seule fois :
    }

4. Initialisez la broche : dans la fonction ``void setup()``, définissez la broche du buzzer en mode sortie.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;   // Assigne la broche 9 à la constante pour le buzzer

    void setup() {
        // Configurez ici votre code pour qu'il s'exécute une seule fois :
        pinMode(buzzerPin, OUTPUT);  // Configure la broche 9 en sortie
    }

5. Faire émettre un signal sonore à un buzzer actif est aussi simple que d'allumer une LED ; il suffit d'utiliser ``digitalWrite()`` pour définir la broche 9 sur haut ou bas et ``delay()`` pour contrôler la durée.

.. code-block:: Arduino
    :emphasize-lines: 10-13

    const int buzzerPin = 9;   // Assigne la broche 9 à la constante pour le buzzer

    void setup() {
        // Configurez ici votre code pour qu'il s'exécute une seule fois :
        pinMode(buzzerPin, OUTPUT);  // Configure la broche 9 en sortie
    }

    void loop() {
        // Configurez ici votre code pour qu'il s'exécute de manière répétée :
        digitalWrite(buzzerPin, HIGH);  // Allume le buzzer
        delay(250);                     // Durée du bip : 250 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteint le buzzer
        delay(250);                     // Intervalle entre les signaux : 250 millisecondes
    }

6. Vous pouvez téléverser votre code sur l'Arduino Uno R3, et vous entendrez alors un « bip bip » sonore.

7. Pour faire émettre un code Morse au buzzer, vous devez créer deux fonctions après ``void loop()``, pour émettre des points (signaux courts) et des traits (signaux longs).

.. note::

    En code Morse, il existe des règles de synchronisation traditionnelles pour les points (signaux courts), les traits (signaux longs) et les intervalles entre les signaux afin d'assurer que le message soit reçu et compris correctement. Voici quelques règles de base :

    * Longueur d'un point : l'unité de temps de base.
    * Longueur d'un trait : équivaut à trois points.
    * Intervalle entre les points : longueur d'un point.
    * Intervalle au sein d'un caractère (entre points et traits d'une lettre ou d'un chiffre) : longueur d'un point.
    * Intervalle entre les caractères (par exemple, entre deux lettres) : trois points.
    * Intervalle entre les mots (par exemple, entre deux mots) : sept points.

    Par conséquent, nous définissons la durée d'un point à 250ms, celle d'un trait à 750ms, et l'intervalle entre les éléments à 250ms.

.. code-block:: Arduino
    :emphasize-lines: 9-14,16-21

    void loop() {
        // Configurez ici votre code pour qu'il s'exécute de manière répétée :
        digitalWrite(buzzerPin, HIGH);  // Allume le buzzer
        delay(250);                     // Durée du bip : 250 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteint le buzzer
        delay(250);                     // Intervalle entre les signaux : 250 millisecondes
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Courte durée pour un point
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalle entre les signaux
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Durée plus longue pour un trait
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalle entre les signaux
    }

8. Maintenant, vous pouvez transmettre le code Morse. Par exemple, pour envoyer « SOS » (... --- ...), le code Morse pour « S » est constitué de trois points, et « O » de trois traits, vous appelez donc simplement les fonctions dot et dash trois fois respectivement.

.. code-block:: Arduino
    :emphasize-lines: 2-11

    void loop() {
        dot();
        dot();
        dot();  // S : ...
        dash();
        dash();
        dash();  // O : ---
        dot();
        dot();
        dot();       // S : ...
        delay(750);  // Répéter après un intervalle
    }

9. Voici votre code complet. Vous pouvez maintenant cliquer sur "Téléverser" pour charger le code sur l'Arduino Uno R3, après quoi vous entendrez le code Morse pour "SOS" (... --- ...).

.. code-block:: Arduino

    const int buzzerPin = 9;   // Assigne la broche 9 à la constante pour le buzzer
    
    void setup() {
        // Configurez ici votre code pour qu'il s'exécute une seule fois :
        pinMode(buzzerPin, OUTPUT);  // Configure la broche 9 en sortie
    }

    void loop() {
        dot();
        dot();
        dot();  // S: ...
        dash();
        dash();
        dash();  // O: ---
        dot();
        dot();
        dot();       // S: ...
        delay(750);  // Répéter après un intervalle
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Courte durée pour un point
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalle entre les signaux
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Longue durée pour un trait
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervalle entre les signaux
    }


10. Enfin, souvenez-vous de sauvegarder votre code et de ranger votre espace de travail.


**Résumé**

Dans cette leçon, vous avez découvert les bases du code Morse, un moyen de communication unique développé dans les années 1840 par Samuel Morse. Vous avez appris à utiliser un buzzer actif pour envoyer le code Morse pour SOS, un signal de détresse universellement reconnu. Cette leçon vous a non seulement appris à configurer et à coder un buzzer actif, mais vous a également donné un aperçu de l'importance historique du code Morse dans les télécommunications. Avec ces compétences, vous pouvez maintenant envoyer des messages en code Morse à vos amis ou explorer davantage ses applications dans les dispositifs modernes.

Dans cette leçon, nous n'avons utilisé que les codes Morse pour les lettres "S" et "O". Voici le tableau des 26 lettres et des 10 chiffres en code Morse.


.. list-table::
    :widths: 8 8 8 8 8 8 8 8
    :header-rows: 1

    * - Lettre
      - Code
      - Lettre
      - Code
      - Lettre
      - Code
      - Lettre
      - Code
    * - A
      - \.-
      - B
      - \-...
      - C
      - \-.\-.
      - D
      - \-..
    * - E
      - \.
      - F
      - \..-.
      - G
      - \-\-.
      - H
      - \....
    * - I
      - \..
      - J
      - \.\-\-\-
      - K
      - \-.- 
      - L
      - \.-..
    * - M
      - \-- 
      - N
      - \-.
      - O
      - \-\-\-
      - P
      - \.-\-.
    * - Q
      - \-\-.-
      - R
      - \.-.
      - S
      - \...
      - T
      - \-
    * - U
      - \..-
      - V
      - \...-
      - W
      - \.-\-
      - X
      - \-..-
    * - Y
      - \-.-\-
      - Z
      - \-\-..
      - 1
      - \.\-\-\-\-
      - 2
      - \..\-\-\-
    * - 3
      - \...-\-
      - 4
      - \....-
      - 5
      - \.....
      - 6
      - \-....
    * - 7
      - \-\-...
      - 8
      - \-\-\-..
      - 9
      - \-\-\-\-.
      - 
      - 


**Question**

En utilisant le tableau du code Morse fourni, écrivez un code pour envoyer le message "Hello".
