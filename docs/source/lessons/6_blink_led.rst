.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et relevez vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprenez et partagez** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions spéciales.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !


6. Faire clignoter une LED
===============================

Bienvenue dans cette leçon ! Vous apprendrez à manipuler les broches numériques de l'Arduino Uno R3 pour contrôler une LED de manière programmée, en l'allumant et l'éteignant automatiquement, une compétence essentielle tant dans les applications domestiques qu'industrielles.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="../_static/video/6_blink_led.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Dans cette leçon, vous allez apprendre à :

* Créer et sauvegarder des sketches en utilisant l'IDE Arduino.
* Utiliser les fonctions ``pinMode()`` et ``digitalWrite()`` pour contrôler des éléments de circuit.
* Télécharger des sketches sur l'Arduino Uno R3 et comprendre leurs effets en temps réel.
* Implémenter ``delay()`` dans les sketches pour gérer les comportements du circuit.

À la fin de cette leçon, vous serez capable de construire un circuit qui non seulement allume une LED, mais la fait aussi clignoter à des intervalles que vous définissez, vous offrant ainsi une compréhension de base de l'interaction entre le logiciel et le matériel.

Construction du circuit
----------------------------

**Composants nécessaires**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * LED rouge
     - 1 * Résistance de 220Ω
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

**Étapes de construction**

Prenez le circuit construit dans :ref:`2_first_circuit` et déplacez le fil de la borne 5V vers la broche 3, comme indiqué sur l'image ci-dessous.

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center

Si vous avez démonté le circuit précédent, vous pouvez le reconstruire en suivant ces étapes :

1. Connectez la résistance de 220 ohms à la plaque d'essai. Un fil doit être dans le terminal négatif, et l'autre dans le trou 1B.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Ajoutez une LED rouge à la plaque d'essai. L'anode de la LED (longue patte) doit être dans le trou 1F et la cathode (courte patte) dans le trou 1E. Parfois, il est difficile de distinguer l'anode de la cathode par la longueur des pattes. Rappelez-vous, le côté cathode de la LED a également un bord plat sur la lentille colorée, tandis que l'anode a un bord arrondi.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Utilisez un court câble de connexion pour relier la LED à la source d'alimentation. Une extrémité du câble doit être dans le trou 1J et l'autre dans le terminal positif.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Connectez le terminal positif de la plaque d'essai à la broche 3 de l'Arduino Uno R3.

.. image:: img/6_led_circuit_3.png
    :width: 600
    :align: center

5. Reliez le terminal négatif de la plaque d'essai à l'une des broches de masse ("GND") de l'Arduino Uno R3.

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center


Animer la LED
-----------------------------

Ça y est, il est temps de donner vie à la LED ! Au lieu de se plonger directement dans l'exemple Blink d'Arduino, nous allons partir de zéro et créer un tout nouveau sketch. Allons-y !

**1. Créer et sauvegarder un sketch**

1. Lancez l'IDE Arduino. Allez dans le menu “Fichier” et cliquez sur “Nouveau sketch” pour commencer à neuf. Vous pouvez fermer les autres fenêtres de sketch qui pourraient être ouvertes.

    .. image:: img/6_blink_ide_new.png
        :align: center

2. Organisez la fenêtre de l'IDE Arduino côte à côte avec ce tutoriel en ligne, afin de voir les deux à la fois. Les éléments peuvent sembler petits, mais cela vous évitera de devoir passer d'une fenêtre à l'autre.

    .. image:: img/6_blink_ide_tutorials.png


3. Il est temps de sauvegarder votre sketch. Cliquez sur “Sauvegarder” dans le menu “Fichier” ou appuyez sur ``Ctrl + S``.

    .. image:: img/6_blink_ide_save.png


4. Vous pouvez sauvegarder votre sketch à l'emplacement par défaut ou à un autre endroit. Donnez à votre sketch un nom significatif, tel que ``Leçon6_Allumer_LED``, puis cliquez sur “Sauvegarder”.

    * Nommez votre sketch d'après sa fonction pour le retrouver facilement plus tard.
    * Les noms de fichiers de sketchs Arduino ne peuvent pas contenir d'espaces.
    * Lorsque vous enregistrez des modifications importantes, pensez à enregistrer sous une nouvelle version (par ex., V1) pour avoir une sauvegarde.
    
    .. image:: img/6_blink_ide_name.png


5. Votre nouveau sketch se compose de deux parties principales, ``void setup()`` et ``void loop()``, qui sont des fonctions utilisées dans tous les sketches Arduino.

    * ``void setup()`` s'exécute une fois au démarrage du programme pour définir les conditions initiales.
    * ``void loop()`` s'exécute en continu, réalisant les actions répétitives.
    * Placez les commandes pour chaque fonction entre ses accolades ``{}``.
    * Toute ligne commençant par ``//`` est un commentaire. Ce sont des notes pour vous et elles n'affecteront pas l'exécution du code.

    .. code-block:: Arduino

        void setup() {
        // Configuration du code ici, exécuté une fois :

        }

        void loop() {
        // Placez votre code principal ici, qui sera exécuté en boucle :

        }

**2. Choisir la carte et le port**

1. Connectez votre Arduino Uno R3 à l'ordinateur avec un câble USB. Vous verrez la lumière de mise sous tension s'allumer sur l'Arduino.

    .. image:: img/1_connect_uno_pc.jpg
        :width: 600
        :align: center


2. Indiquez à l'IDE que vous utilisez une **Arduino Uno**. Allez dans **Outils** -> **Carte** -> **Cartes Arduino AVR** -> **Arduino Uno**.

    .. image:: img/6_blink_ide_board.png
        :width: 600
        :align: center


3. Ensuite, dans l'IDE Arduino, choisissez le port auquel votre Arduino est connecté.

    .. note::

        * Une fois qu'un port est sélectionné, l'IDE Arduino devrait s'y connecter par défaut chaque fois que l'Arduino est branché via USB.
        * Si une autre carte Arduino est connectée, il vous faudra peut-être choisir un nouveau port.
        * Vérifiez toujours le port en premier en cas de problème de connexion.

    .. image:: img/6_blink_ide_port.png
        :width: 600
        :align: center

**3. Écrire le code**


1. Dans notre projet, nous utilisons la broche numérique 3 sur la carte pour contrôler une LED. Chaque broche peut fonctionner soit en tant que sortie, envoyant 5 volts, soit en tant qu'entrée, lisant la tension entrante. Pour configurer la LED, nous définissons la broche en sortie avec la fonction ``pinMode(pin, mode)``.
    
Voyons la syntaxe de ``pinMode()``.

    * ``pinMode(pin, mode)`` : Définit une broche spécifique en tant qu'``INPUT`` ou ``OUTPUT``.

    **Paramètres**
        - ``pin`` : le numéro de la broche que vous souhaitez configurer.
        - ``mode`` : ``INPUT``, ``OUTPUT`` ou ``INPUT_PULLUP``.

    **Retourne**
        Rien
    
2. Il est maintenant temps d'ajouter notre première ligne de code dans la fonction ``void setup()``.
        
    .. note::

        - Le codage Arduino est sensible à la casse. Assurez-vous d'écrire les fonctions exactement comme elles sont.
        - Remarquez que la commande se termine par un point-virgule. Dans l'IDE Arduino, chaque commande doit se terminer par un point-virgule.
        - Les commentaires dans le code sont utiles pour vous rappeler ce que fait une ligne ou une section du code.

    .. code-block:: Arduino
        :emphasize-lines: 3

        void setup() {
            // Code de configuration ici, exécuté une seule fois :
            pinMode(3,OUTPUT); // définir la broche 3 comme sortie
        }
    
        void loop() {
        // Placez ici votre code principal, exécuté en boucle :

        }

**4. Vérifier le code**

Avant d'activer nos feux de signalisation, nous allons vérifier le code. Cela permet de s'assurer que l'IDE Arduino peut comprendre et compiler vos commandes en langage machine.

1. Pour vérifier votre code, cliquez sur le bouton **cocher** dans le coin supérieur gauche de la fenêtre.

    .. image:: img/6_blink_ide_verify.png
        :width: 600
        :align: center


2. Si votre code est lisible par la machine, un message en bas indiquera que le code a été compilé avec succès. Cette zone montre également l'espace de stockage utilisé par votre programme.

    .. image:: img/6_blink_ide_verify_done.png
        :width: 600
        :align: center


3. Si votre code contient une erreur, vous verrez un message d'erreur orange. L'IDE met souvent en évidence l'endroit où se trouve le problème, généralement près de la ligne en surbrillance. Par exemple, une erreur due à un point-virgule manquant mettra en évidence la ligne juste après l'erreur.

    .. image:: img/6_blink_ide_verify_error.png
        :width: 600
        :align: center


4. Lorsque vous rencontrez des erreurs, il est temps de déboguer — c'est-à-dire de trouver et corriger les erreurs dans votre code. Vérifiez les problèmes courants tels que :

    - Le ``M`` de ``pinMode`` est-il en majuscule ?
    - Avez-vous utilisé toutes les lettres en majuscules pour ``OUTPUT`` ?
    - Avez-vous à la fois une parenthèse ouvrante et fermante dans votre fonction ``pinMode`` ?
    - Avez-vous terminé votre fonction ``pinMode`` par un point-virgule ?
    - L'orthographe est-elle correcte ? Si vous trouvez des erreurs, corrigez-les et vérifiez à nouveau votre code. Continuez à déboguer jusqu'à ce que votre sketch soit sans erreur.

L'IDE Arduino cesse de compiler à la première erreur, vous devrez peut-être vérifier plusieurs fois pour corriger plusieurs erreurs. Vérifier régulièrement votre code est une bonne habitude.

Le débogage est une grande partie de la programmation. Les programmeurs professionnels passent souvent plus de temps à déboguer qu'à écrire du nouveau code. Les erreurs sont normales, donc ne vous découragez pas. Devenir un bon résolveur de problèmes est essentiel pour être un excellent programmeur.

**5. Continuer à écrire le sketch**

1. Vous êtes maintenant prêt à commencer la fonction ``void loop()``. C'est ici que se déroule l'action principale de votre sketch ou programme. Pour allumer la LED connectée à l'Arduino Uno R3, nous devons fournir de la tension au circuit en utilisant ``digitalWrite()``.

    * ``digitalWrite(pin, value)`` : Envoie un signal ``HIGH`` (5V) ou ``LOW`` (0V) à une broche numérique, modifiant l'état de fonctionnement du composant.

    **Paramètres**
        - ``pin`` : le numéro de la broche de l'Arduino.
        - ``value`` : ``HIGH`` ou ``LOW``.
    
    **Retourne**
        Rien

5. Sous le commentaire dans la fonction ``void loop()``, écrivez une commande pour allumer la LED connectée à la broche 3. N'oubliez pas de terminer la commande par un point-virgule. Vérifiez et déboguez votre code si nécessaire.

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Code de configuration ici, exécuté une seule fois :
            pinMode(3, OUTPUT);  // définir la broche 3 comme sortie
        }

        void loop() {
            // Placez ici votre code principal, exécuté en boucle :
            digitalWrite(3, HIGH);
        }

6. Après la commande ``digitalWrite()``, ajoutez un commentaire expliquant ce que fait cette ligne. Par exemple :

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Code de configuration ici, exécuté une seule fois : 
            pinMode(3, OUTPUT);  // définir la broche 3 comme sortie
        }

        void loop() {
            // Placez ici votre code principal, exécuté en boucle :
            digitalWrite(3, HIGH);  // Allumer la LED sur la broche 3
        }

**6. Téléverser le code**

Une fois que votre code est vérifié et sans erreur, il est temps de le téléverser sur l'Arduino Uno R3 et de voir votre feu de signalisation s'animer.

1. Dans l'IDE, cliquez sur le bouton "Téléverser". L'ordinateur va compiler le code, puis le transférer vers l'Arduino Uno R3. Pendant le transfert, vous devriez voir des lumières clignoter sur la carte, indiquant la communication avec l'ordinateur.

.. image:: img/6_blink_ide_upload.png
    :width: 600
    :align: center

2. Un message "Téléversement terminé" signifie que votre code ne contient pas de problème et que vous avez sélectionné la bonne carte et le bon port.

.. image:: img/6_blink_ide_upload_done.png
    :width: 600
    :align: center


3. Une fois le transfert terminé, le code s'exécutera et vous devriez voir la LED sur la plaque d'essai s'allumer.

**7. Mesurer la tension aux bornes de la LED**

Utilisons un multimètre pour mesurer la tension à la broche 3 et comprendre ce que signifie réellement l'état ``HIGH`` dans le code.

1. Réglez le multimètre sur la position 20 volts en courant continu (DC).

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Commencez par mesurer la tension à la broche 3. Touchez la sonde rouge du multimètre à la broche 3 et la sonde noire à la masse (GND).

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

3. Notez la tension mesurée dans le tableau pour la broche 3 sous la ligne intitulée "HIGH".

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - État
     - Tension broche 3
   * - HIGH
     - *≈4.95 volts*
   * - LOW
     - 


4. Après avoir mesuré, pensez à éteindre le multimètre en le réglant sur la position "OFF".

Nos mesures montrent que la tension sur la broche 3 est proche de 5V. Cela indique que définir une broche à ``HIGH`` dans le code signifie que la tension de sortie à cette broche est proche de 5V.

La tension des broches du R3 est de 5V, donc en les réglant sur ``HIGH``, elle atteint presque 5V. Cependant, certaines cartes fonctionnent à 3.3V, ce qui signifie que leur état ``HIGH`` serait proche de 3.3V.

Faire clignoter la LED
------------------------------
Maintenant que votre LED est allumée, il est temps de la faire clignoter.

1. Ouvrez le sketch que vous avez sauvegardé précédemment, ``Lesson6_Light_up_LED``. Cliquez sur “Enregistrer sous...” dans le menu “Fichier”, et renommez-le en ``Lesson6_Blink_LED``. Cliquez sur "Enregistrer".

2. Dans la fonction ``void loop()`` de votre sketch, copiez les commandes ``digitalWrite()`` et collez-les après les lignes originales. Pour faire clignoter la LED, vous l'avez allumée précédemment ; maintenant, définissez son état sur ``LOW`` pour l'éteindre.

    .. note::
       * Copier et coller peut être un allié précieux pour un programmeur. Reproduisez une section de code propre à un nouvel emplacement et ajustez ses paramètres pour une exécution rapide et efficace.
       * N'oubliez pas de mettre à jour les commentaires pour mieux correspondre à l'action effectuée.
       * Utilisez ``Ctrl+T`` pour formater votre code proprement en un seul clic, le rendant plus lisible et convivial.

    .. code-block:: Arduino
       :emphasize-lines: 8,9

       void setup() {
            // Code de configuration ici, exécuté une seule fois :
            pinMode(3, OUTPUT);  // définir la broche 3 comme sortie
       }

       void loop() {
            // Placez ici votre code principal, exécuté en boucle :
            digitalWrite(3, HIGH);  // Allumer la LED sur la broche 3   
            digitalWrite(3, LOW);  // Éteindre la LED sur la broche 3
       }

3. Appuyez sur le bouton "Téléverser" pour transférer le sketch vers l'Arduino Uno R3. Après le transfert, vous remarquerez peut-être que la LED ne clignote pas, ou qu'elle clignote si rapidement que cela en devient imperceptible.

4. Pour observer visuellement le clignotement, vous pouvez utiliser la commande ``delay()`` afin de faire attendre l'Arduino Uno R3 pendant une durée que vous spécifiez, en millisecondes.

    * ``delay(ms)`` : Met le programme en pause pendant le temps spécifié (en millisecondes) passé en paramètre. (Il y a 1000 millisecondes dans une seconde.)

    **Paramètres**
        - ``ms`` : le nombre de millisecondes à attendre. Types de données acceptés : unsigned long.

    **Retourne**
        Rien

5. Maintenant, incluez la commande ``delay(time)`` après chaque commande ON et OFF, en réglant le temps d'attente à 3000 millisecondes (3 secondes). Vous pouvez ajuster cette durée pour que la LED clignote plus rapidement ou plus lentement.

    .. note::

        Pendant ce délai, l'Arduino Uno R3 ne peut exécuter aucune autre tâche ou commande jusqu'à la fin du délai.
        
    .. code-block:: Arduino
       :emphasize-lines: 10,11

       void setup() {
            // Code de configuration ici, exécuté une seule fois :
            pinMode(3, OUTPUT);  // définir la broche 3 comme sortie
       }

       void loop() {
            // Placez ici votre code principal, exécuté en boucle :
            digitalWrite(3, HIGH);  // Allumer la LED sur la broche 3
            delay(3000);  // Attendre 3 secondes   
            digitalWrite(3, LOW);  // Éteindre la LED sur la broche 3
            delay(3000);  // Attendre 3 secondes
       }

6. Téléversez votre sketch sur l'Arduino Uno R3. Une fois terminé, votre LED devrait clignoter toutes les 3 secondes.

7. Vérifiez que tout fonctionne comme prévu, puis sauvegardez votre sketch.

8. Utilisons maintenant un multimètre pour mesurer la tension sur trois broches et comprendre ce que signifie l'état ``LOW`` dans le code. Réglez le multimètre sur la position 20 volts en courant continu.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

9. Commencez par mesurer la tension à la broche 3. Touchez la sonde rouge du multimètre à la broche 3 et la sonde noire à GND.

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

10. Avec les trois LED éteintes, notez la tension mesurée pour la broche 3 dans la ligne "LOW" de votre tableau.

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - État
     - Tension broche 3 
   * - HIGH
     - *≈4.95 volts*
   * - LOW
     - *0.00 volts*

Grâce à nos mesures, nous avons constaté que lorsque les LED sont éteintes, la tension à la broche 3 chute à 0V. Cela montre que dans notre code, définir une broche à "LOW" réduit effectivement la tension de sortie à 0V, éteignant ainsi la LED connectée. Ce principe nous permet de contrôler les états ON et OFF des LED avec un timing précis, imitant le fonctionnement d'un feu de signalisation.

**Question**

Téléversez le code ci-dessus, et vous constaterez que la LED clignote à intervalles de 3 secondes. Si vous voulez qu'elle s'allume et s'éteigne une seule fois, que devriez-vous faire ?


**Résumé**

Félicitations pour avoir complété cette leçon, où vous avez réussi à programmer une LED pour clignoter à l'aide de l'Arduino Uno R3. Cette leçon vous a introduit à l'écriture et au téléversement de sketches Arduino, à la définition des modes de broche, et à la manipulation des sorties pour obtenir des réponses électriques souhaitées. En construisant le circuit et en programmant l'Arduino Uno R3, vous avez acquis des connaissances précieuses sur l'interaction entre les commandes logicielles et les comportements matériels physiques.

Votre capacité à contrôler une LED n'est que le début — imaginez ce que vous pouvez accomplir en développant ces bases !
