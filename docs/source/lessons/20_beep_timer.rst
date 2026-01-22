.. note::

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprenez & Partagez** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits et à des aperçus exclusifs.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos nouveaux produits.
    - **Promotions et concours festifs** : Participez à des concours et à des promotions spéciales pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

20. Le Timer Pomodoro
===========================================

Dans cette leçon, nous allons explorer l'intersection entre la gestion du temps et la technologie en créant un Timer Pomodoro à l'aide d'un Arduino et d'un buzzer actif. Vous apprendrez à utiliser les capacités internes de temporisation de l'Arduino pour construire un minuteur qui segmente le travail en périodes concentrées de 25 minutes suivies de pauses de 5 minutes. Cette méthode, connue sous le nom de Technique Pomodoro, améliore la productivité et la concentration. Tout au long du cours, vous acquerrez une solide base en temporisation électronique et une expérience pratique en programmation et assemblage de circuits, culminant dans la création d'un Timer Pomodoro fonctionnel. Rejoignez-nous pour maîtriser votre temps et augmenter votre efficacité dans vos activités quotidiennes !

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/20_beep_timer.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

À la fin de cette leçon, vous serez capable de :

* Comprendre l'importance historique du son dans la gestion du temps.
* Identifier les composants nécessaires pour construire un circuit de minuterie électronique.
* Programmer un Arduino pour contrôler un buzzer pour la gestion du temps en utilisant les fonctions ``delay()`` et ``millis()``.
* Appliquer la Technique Pomodoro dans un contexte pratique en créant un minuteur qui alterne entre périodes de travail et de pause.

Horloges et Son
--------------------

Dans l'Antiquité, de grandes cloches étaient utilisées pour marquer le passage du temps et certains événements sociaux spécifiques.
Par exemple, les villes européennes médiévales utilisaient les cloches des églises pour signaler les heures de prière et le début et la fin des journées de travail.
Ces cloches étaient bien plus que de simples indicateurs temporels ; elles servaient d'outils d'organisation sociale, autour desquels la vie quotidienne de la communauté s'articulait.

**Horloges mécaniques et son**

.. image:: img/7_big_ben.png
  :width: 500
  :align: center

Avec le développement des horloges mécaniques, et en particulier avec la conception du Big Ben, les horloges ont commencé à être équipées de cloches plus complexes et de mécanismes de temporisation plus élaborés.
Le son du Big Ben est produit par ses grandes cloches en bronze, ce qui amplifie la portée du son et la précision des annonces temporelles.
Dans de nombreuses villes, le son du Big Ben est devenu une référence pour les habitants, leur permettant d'ajuster leurs activités quotidiennes et jouant un rôle crucial dans la planification plus précise du temps pour la navigation, les horaires de chemin de fer, et plus encore.

**La gestion du temps sonore à l'ère électronique**

.. image:: img/19_timer.jpg
  :width: 500
  :align: center

Avec l'entrée dans l'ère électronique, les minuteurs sonores ont évolué. L'introduction 
des buzzers électroniques, avec l'aide de microcontrôleurs comme l'Arduino, a permis de 
rendre la gestion du temps indépendante des grands dispositifs mécaniques. Ces petits 
appareils peuvent produire des sons à différentes fréquences et hauteurs, ce qui permet 
leur utilisation dans diverses applications de temporisation, allant des minuteurs de 
cuisine simples aux systèmes complexes de contrôle de processus industriels. Parmi les 
exemples, on trouve les systèmes d'appel infirmier dans les hôpitaux modernes, les sonneries 
des écoles et les rappels dans les dispositifs électroniques personnels, tous utilisant des 
buzzers électroniques pour la gestion du temps.

Construction du circuit
---------------------------

**Composants nécessaires**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Plaque d'essai
     - 1 * Buzzer actif
     - Fils de connexion
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_active_buzzer| 
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

Cette leçon utilise le même circuit que celui de la leçon 17.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Création du code - Tic Tic
------------------------------

En Arduino, ``delay()`` est la fonction de temporisation la plus simple et la plus utilisée.
Nous l'utilisons souvent pour suspendre le programme pendant un court laps de temps, ce qui, combiné avec des boucles, peut créer un effet de clignotement de LED. Ici, nous utilisons la fonction ``delay()`` pour faire sonner le buzzer toutes les secondes.

1. Ouvrez l'IDE Arduino et démarrez un nouveau projet en sélectionnant "New Sketch" dans le menu "Fichier".
2. Enregistrez votre sketch sous le nom ``Lesson20_Timer_Tick_Tick`` en utilisant ``Ctrl + S`` ou en cliquant sur "Enregistrer".

3. Écrivez le code suivant :

.. code-block:: Arduino

  const int buzzerPin = 9;   // Assigne la broche 9 à la constante pour le buzzer  
  
  void setup() {
    // Mettre ici le code de configuration, exécuté une seule fois :
    pinMode(buzzerPin, OUTPUT);  // Définir la broche 9 comme sortie
  } 

  void loop() {
    // Mettre ici le code principal, exécuté en boucle :
    digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
    delay(100);                     // Durée du bip : 100 millisecondes
    digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
    delay(1000);                    // Intervalle entre les signaux : 1000 millisecondes
  }

Dans cette configuration, la première fonction ``delay()`` suspend l'Arduino Uno R3 pendant 100 millisecondes, pendant lesquelles le buzzer continue de sonner. La seconde fonction ``delay()`` suspend l'Arduino pendant 1000 millisecondes (1 seconde), pendant lesquelles le buzzer est silencieux.

4. Après avoir téléversé le code sur l'Arduino Uno R3, vous entendrez le buzzer émettre un bip toutes les secondes.

Création du code - ``millis()``
----------------------------------

L'utilisation de ``delay()`` suspend votre code, ce qui peut être peu pratique.

Par exemple, imaginez que vous chauffez une pizza au micro-ondes tout en attendant des emails importants.
Vous mettez la pizza dans le micro-ondes et réglez le minuteur à 10 minutes. L'analogie avec l'utilisation de ``delay()`` serait de rester devant le micro-ondes, regardant le décompte des 10 minutes jusqu'à zéro. Si vous recevez un email important pendant ce temps, vous le manquerez.

Ce que vous feriez normalement, c'est mettre la pizza dans le micro-ondes, puis vérifier vos emails, voire faire autre chose, en revenant périodiquement voir si le minuteur a atteint zéro, indiquant que la pizza est prête.

Arduino dispose également d'un outil de temporisation qui ne suspend pas le programme : la fonction ``millis()``.

``millis()`` est une fonction très importante en programmation Arduino. Elle renvoie le nombre de millisecondes écoulées depuis que la carte Arduino a été mise sous tension ou réinitialisée.

  * ``time = millis()`` : Renvoie le nombre de millisecondes écoulées depuis que la carte Arduino exécute le programme actuel. Ce nombre se réinitialise (retourne à zéro) après environ 50 jours.

  **Paramètres**
    Aucun

  **Renvoie**
    Nombre de millisecondes écoulées depuis le démarrage du programme. Type de données : unsigned long.

Ici, nous faisons de même pour faire sonner le buzzer une fois par seconde.

1. Ouvrez l'IDE Arduino et démarrez un nouveau projet en sélectionnant "New Sketch" dans le menu "Fichier".
2. Enregistrez votre sketch sous le nom ``Lesson20_Timer_Millis`` en utilisant ``Ctrl + S`` ou en cliquant sur "Enregistrer".

3. Tout d'abord, créez une constante appelée ``buzzerPin`` et attribuez-lui la broche 9.

.. code-block:: Arduino
  :emphasize-lines: 1

  const int buzzerPin = 9;   // Assigne la broche 9 à la constante pour le buzzer

  void setup() {
    // Mettez ici votre code de configuration, qui s'exécute une seule fois :
  }

4. Créez deux variables de type long : ``previousMillis`` stockera le temps du dernier bip du buzzer, et ``interval`` définit la fréquence des bips du buzzer, en millisecondes. Ici, il est réglé pour sonner toutes les 1000 millisecondes (ou chaque seconde).

.. code-block:: Arduino
  :emphasize-lines: 3,4

  const int buzzerPin = 9;  // Assigne la broche 9 à la constante pour le buzzer

  unsigned long previousMillis = 0;  // Stocke l'horodatage du dernier bip du buzzer
  long interval = 1000;              // Intervalle de bip (en millisecondes)

5. Dans la fonction ``void setup()``, configurez la broche du buzzer en mode sortie.

.. code-block:: Arduino
  :emphasize-lines: 8

  const int buzzerPin = 9;  // Assigne la broche 9 à la constante pour le buzzer

  unsigned long previousMillis = 0;  // Stocke l'horodatage du dernier bip du buzzer
  long interval = 1000;              // Intervalle de bip (en millisecondes)

  void setup() {
    // Mettez ici votre code de configuration, qui s'exécute une seule fois :
    pinMode(buzzerPin, OUTPUT);  // Définir la broche 9 comme sortie
  }

6. Dans la fonction ``void loop()``, créez une variable de type ``unsigned long`` appelée ``currentMillis`` pour stocker l'heure actuelle.

.. code-block:: Arduino
  :emphasize-lines: 3

  void loop() {
    // Mettez ici votre code principal, qui s'exécute en boucle :
    unsigned long currentMillis = millis();
  }

7. Lorsque le temps écoulé depuis la dernière mise à jour dépasse 1000ms, déclenchez certaines fonctions. Mettez également à jour la valeur de ``previousMillis`` avec l'heure actuelle, pour que le prochain déclenchement se produise dans 1 seconde.

.. code-block:: Arduino
  :emphasize-lines: 5,6

  void loop() {
    // Mettez ici votre code principal, qui s'exécute en boucle :
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Sauvegarder l'heure du dernier bip
    }
  }

8. Ajoutez les fonctions principales à exécuter périodiquement. Dans ce cas, faites sonner le buzzer.

.. code-block:: Arduino
  :emphasize-lines: 7,8,9

  void loop() {
    // Mettez ici votre code principal, qui s'exécute en boucle :
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Sauvegarder l'heure du dernier bip
      digitalWrite(buzzerPin, HIGH);   // Faire sonner le buzzer
      delay(100);
      digitalWrite(buzzerPin, LOW);  // Arrêter le buzzer
    }
  }

9. Votre code complet devrait ressembler à ceci. Téléversez-le sur l'Arduino Uno R3 et vous entendrez le buzzer émettre un bip toutes les secondes.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Assigne la broche 9 à la constante pour le buzzer

  unsigned long previousMillis = 0;  // Stocke l'horodatage du dernier bip du buzzer
  long interval = 1000;              // Intervalle de bip (en millisecondes)

  void setup() {
    // Mettez ici votre code de configuration, qui s'exécute une seule fois :
    pinMode(buzzerPin, OUTPUT);  // Définir la broche 9 comme sortie
  }

  void loop() {
    // Mettez ici votre code principal, qui s'exécute en boucle :
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Sauvegarder l'heure du dernier bip
      digitalWrite(buzzerPin, HIGH);   // Faire sonner le buzzer
      delay(100);
      digitalWrite(buzzerPin, LOW);  // Arrêter le buzzer
    }
  }

**Question**

Si la fonction ``delay(100);`` est remplacée par ``delay(1000);``, que se passera-t-il dans le programme ? Pourquoi ?


Création du code - Timer Pomodoro
-------------------------------------

La Technique Pomodoro, également connue sous le nom de Technique de la tomate, est une méthode de gestion du temps développée par Francesco Cirillo à la fin des années 1980.
Cette méthode utilise un minuteur pour diviser le travail en intervalles de 25 minutes, suivis de courtes pauses.
Chaque intervalle de travail est appelé un "pomodoro", en référence au minuteur de cuisine en forme de tomate que Cirillo utilisait durant ses années universitaires.

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

Les étapes de base de la Technique Pomodoro comprennent :

1. **Définir la tâche** : Décidez de la tâche à accomplir avant de commencer.
2. **Régler le minuteur Pomodoro** : Réglez un minuteur pour 25 minutes de travail.
3. **Travail intense** : Concentrez-vous pleinement sur la tâche pendant ces 25 minutes, en évitant toute distraction.
4. **Faire une courte pause** : Une fois le temps de travail écoulé, prenez une pause de 5 minutes. Pendant cette pause, vous pouvez marcher, vous étirer, boire de l'eau, etc., mais évitez les activités liées au travail.

Les avantages de la Technique Pomodoro incluent une meilleure concentration, une réduction de la fatigue, une distinction claire entre le travail et les pauses, aidant à gérer les distractions, et une motivation accrue grâce à l'accomplissement des tâches. De plus, la Technique Pomodoro ne nécessite pas d'outils ou de technologies complexes — un simple minuteur suffit.

Ensuite, nous allons programmer un minuteur qui émettra un bip toutes les 25 minutes pour signaler la fin d'une période de travail, suivie d'un rappel pour une pause de 5 minutes :

1. Ouvrez l'IDE Arduino et démarrez un nouveau projet en sélectionnant "New Sketch" dans le menu "Fichier".
2. Enregistrez votre sketch sous le nom ``Lesson20_Timer_Millis_Pomodoro`` en utilisant ``Ctrl + S`` ou en cliquant sur "Enregistrer".

3. Définissez quelques constantes et variables avant la fonction ``void setup()``.

* ``buzzerPin`` identifie la broche à laquelle le buzzer est connecté.
* ``startMillis`` enregistre le moment où le minuteur commence.
* ``workPeriod`` et ``breakPeriod`` définissent la durée de chaque période.
* ``isWorkPeriod`` est une variable booléenne utilisée pour savoir s'il s'agit d'une période de travail ou de pause.

.. code-block:: Arduino

  const int buzzerPin = 9;          // Assigne la broche 9 à la constante pour le buzzer
  unsigned long startMillis;        // Stocke l'heure de début du minuteur
  const long workPeriod = 1500000;  // Période de travail de 25 minutes
  const long breakPeriod = 300000;  // Période de pause de 5 minutes
  static bool isWorkPeriod = true;  // Indique s'il s'agit d'une période de travail ou de pause


4. Initialisez la broche du buzzer comme une sortie et démarrez le minuteur en enregistrant l'heure de début avec ``millis()``.

.. code-block:: Arduino
  :emphasize-lines: 2,3
  
  void setup() {
    pinMode(buzzerPin, OUTPUT); // Initialiser la broche du buzzer en tant que sortie
    startMillis = millis(); // Enregistrer l'heure de début
  }

5. Dans la fonction ``void loop()``, créez une variable ``unsigned long`` appelée ``currentMillis`` pour stocker l'heure actuelle.

.. code-block:: Arduino
  :emphasize-lines: 2

  void loop() {
    unsigned long currentMillis = millis(); // Mettre à jour l'heure actuelle
  }

6. Utilisez des instructions conditionnelles ``if else if`` pour déterminer s'il s'agit d'une période de travail.

.. code-block:: Arduino
  :emphasize-lines: 4-6

  void loop() {
    unsigned long currentMillis = millis(); // Mettre à jour l'heure actuelle

    if (isWorkPeriod){ 
    } else if (!isWorkPeriod){
    }
  }

7. Si c'est le cas, vérifiez si l'heure actuelle a dépassé la durée de la ``workPeriod``. Si oui, réinitialisez le minuteur, passez à la période de pause et déclenchez deux bips longs avec le buzzer.

.. code-block:: Arduino
  :emphasize-lines: 5-16

  void loop() {
    unsigned long currentMillis = millis();  // Mettre à jour l'heure actuelle

    if (isWorkPeriod) {
      if (currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis;  // Réinitialiser le minuteur
        isWorkPeriod = false;         // Passer à la période de pause
        digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
        delay(500);                     // Buzzer allumé pendant 500 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
        delay(200);                     // Buzzer éteint pendant 200 millisecondes
        digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
        delay(500);                     // Buzzer allumé pendant 500 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
        delay(200);                     // Buzzer éteint pendant 200 millisecondes
      }
    } else if (!isWorkPeriod) {
    }
  }

8. Utilisez des instructions conditionnelles ``else if`` pour déterminer s'il s'agit d'une période de pause et vérifiez de la même manière si le temps écoulé a dépassé la durée de la ``breakPeriod``. Si c'est le cas, réinitialisez le minuteur, revenez à la période de travail et faites sonner le buzzer brièvement deux fois.

.. code-block:: Arduino

  } else if (!isWorkPeriod) {
    if (currentMillis - startMillis >= breakPeriod) {
      startMillis = currentMillis;  // Réinitialiser le minuteur
      isWorkPeriod = true;          // Repasser à la période de travail
      digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
      delay(200);                     // Buzzer allumé pendant 200 millisecondes
      digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
      delay(200);                     // Buzzer éteint pendant 200 millisecondes
      digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
      delay(200);                     // Buzzer allumé pendant 200 millisecondes
      digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
      delay(200);                     // Buzzer éteint pendant 200 millisecondes
    }
  }

9. Votre code complet devrait ressembler à ceci, et vous pouvez le téléverser sur l'Arduino Uno R3 pour voir les effets.

.. note::

  Si vous trouvez que 25 minutes de période de travail et 5 minutes de pause sont trop longues lors du débogage, 
  vous pouvez raccourcir ``workPeriod`` à 15000 millisecondes et ``breakPeriod`` à 3000 millisecondes. Vous entendrez alors le buzzer sonner deux fois longuement toutes les 15 secondes, suivi de deux bips courts après 3 secondes.

.. code-block:: Arduino

  const int buzzerPin = 9;          // Assigner la broche 9 à la constante pour le buzzer
  unsigned long startMillis;        // Stocker l'heure de début du minuteur
  const long workPeriod = 1500000;  // Période de travail de 25 minutes
  const long breakPeriod = 300000;  // Période de pause de 5 minutes
  static bool isWorkPeriod = true;  // Suivre s'il s'agit d'une période de travail ou de pause

  void setup() {
    pinMode(buzzerPin, OUTPUT); // Initialiser la broche du buzzer en tant que sortie
    startMillis = millis(); // Enregistrer l'heure de début
  }

  void loop() {
    unsigned long currentMillis = millis(); // Mettre à jour l'heure actuelle

    if (isWorkPeriod){ 
      if(currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis; // Réinitialiser le minuteur
        isWorkPeriod = false; // Passer à la période de pause
        digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
        delay(500);                     // Buzzer allumé pendant 500 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
        delay(200);                     // Buzzer éteint pendant 200 millisecondes
        digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
        delay(500);                     // Buzzer allumé pendant 500 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
        delay(200);                     // Buzzer éteint pendant 200 millisecondes
      }
    } else if (!isWorkPeriod) 
      if(currentMillis - startMillis >= breakPeriod) {
        startMillis = currentMillis; // Réinitialiser le minuteur
        isWorkPeriod = true; // Repasser à la période de travail
        digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
        delay(200);                     // Buzzer allumé pendant 200 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
        delay(200);                     // Buzzer éteint pendant 200 millisecondes
        digitalWrite(buzzerPin, HIGH);  // Allumer le buzzer
        delay(200);                     // Buzzer allumé pendant 200 millisecondes
        digitalWrite(buzzerPin, LOW);   // Éteindre le buzzer
        delay(200);                     // Buzzer éteint pendant 200 millisecondes
      }
    }
  }

10. Enfin, n'oubliez pas d'enregistrer votre code et de ranger votre espace de travail.

**Question**

Pensez à d'autres moments dans votre vie où vous pouvez "entendre" le temps. Listez quelques exemples et notez-les dans votre carnet !

**Résumé**

Dans le cours d'aujourd'hui, nous avons construit avec succès une version électronique du Timer Pomodoro, un outil précieux pour améliorer la productivité grâce à des périodes de travail et de pause structurées. À travers ce projet, les étudiants ont appris l'utilité des buzzers dans la gestion du temps et l'application pratique de la fonction ``millis()`` pour créer du code non bloquant dans Arduino. Cette approche permet le multitâche dans les applications de microcontrôleurs, reflétant des systèmes plus complexes dans les technologies et l'industrie.

