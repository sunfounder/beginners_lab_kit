.. note::

    Bonjour et bienvenue dans la communauté Facebook des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et tirages au sort** : Participez à des promotions spéciales et des concours lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

24. Lumière clignotante avec le 74HC595
===========================================

Dans cette leçon, nous allons plonger dans le monde du circuit intégré de registre à décalage 74HC595. Ce composant puissant permet de contrôler de nombreuses LED avec seulement quelques broches, ce qui le rend parfait pour mettre en œuvre des effets de lumière clignotante. À la fin de cette leçon, vous comprendrez parfaitement comment fonctionne le 74HC595, comment l'utiliser pour décaler des données binaires et comment l'appliquer dans une expérience pratique de contrôle des LED.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/24_flowing_light.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Dans cette leçon, vous apprendrez à :

* Comprendre le fonctionnement du circuit intégré 74HC595 et les fonctions de ses broches.
* Apprendre à utiliser la fonction ``shiftOut()`` pour décaler des données.
* Construire un circuit de lumière clignotante en utilisant la puce 74HC595 et Arduino.
* Contrôler 8 LED en utilisant des données binaires et la puce 74HC595 pour créer un effet de lumière clignotante.

Comprendre la puce 74HC595
------------------------------

La puce 74HC595 se compose d'un registre à décalage de 8 bits et d'un registre de stockage avec des sorties parallèles à trois états. Elle convertit une entrée série en une sortie parallèle, ce qui permet de sauvegarder des ports d'E/S d'un microcontrôleur (MCU).

.. image:: img/24_74hc595.png
    :width: 300
    :align: center

**Fonctions des broches**

.. image:: img/24_74hc595_pin.png
    :width: 500
    :align: center

* **Q0-Q7** : Broches de sortie de données parallèles 8 bits, capables de contrôler directement 8 LED ou 8 broches d'un afficheur à 7 segments.
* **Q7'** : Broche de sortie série, connectée à DS d'une autre 74HC595 pour connecter plusieurs 74HC595 en série.
* **MR** : Broche de réinitialisation, active à un niveau bas ;
* **SHcp** : Entrée de séquence de temps du registre à décalage. À la montée du front, les données dans le registre à décalage se déplacent successivement d'un bit, c'est-à-dire que les données de Q1 se déplacent vers Q2, et ainsi de suite. À la descente du front, les données dans le registre à décalage restent inchangées.
* **STcp** : Entrée de séquence de temps du registre de stockage. À la montée du front, les données dans le registre à décalage sont transférées dans le registre de stockage.
* **CE** : Broche d'activation de sortie, active à un niveau bas.
* **DS** : Broche d'entrée de données série.
* **VCC** : Broche de tension d'alimentation positive.
* **GND** : Broche de mise à la terre.

**Principe de fonctionnement**

Lorsque MR (broche 10) est à un niveau haut et OE (broche 13) est à un niveau bas,
les données sont entrées à la montée du front de SHcp et vont dans le registre de stockage à la montée du front de STcp.

* Registre à décalage

    * Supposons que nous voulions entrer les données binaires 1110 1110 dans le registre à décalage du 74HC595.
    * Les données sont entrées à partir du bit 0 du registre à décalage.
    * À chaque montée du front d'horloge du registre à décalage, les bits du registre se décalent d'un pas. Par exemple, le bit 7 accepte la valeur précédente du bit 6, le bit 6 prend la valeur du bit 5, etc.

.. image:: img/24_74hc595_shift.png
    :width: 600
    :align: center

* Registre de stockage

    * Lorsque le registre de stockage est à l'état de montée, les données du registre à décalage sont transférées dans le registre de stockage.
    * Le registre de stockage est directement connecté aux 8 broches de sortie, Q0 à Q7 seront en mesure de recevoir un octet de données.
    * Le registre de stockage signifie que les données peuvent exister dans ce registre et ne disparaîtront pas avec une seule sortie.
    * Les données resteront valides et inchangées tant que le 74HC595 sera alimenté en continu.
    * Lorsque de nouvelles données arrivent, les données dans le registre de stockage seront écrasées et mises à jour.

.. image:: img/24_74hc595_storage.png
    :width: 600
    :align: center

Construire le circuit
-------------------------

**Composants nécessaires**

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 8 * LED
     - 8 * Résistance de 220Ω
     - 1 * 74HC595
   * - |list_uno_r3|
     - |list_red_led|
     - |list_220ohm|
     - |list_74hc595|
   * - 1 * Plaque de montage (breadboard)
     - Fils de connexion
     - 1 * Câble USB
     -
   * - |list_breadboard|
     - |list_wire|
     - |list_usb_cable|
     -

**Étapes de construction**

Suivez le schéma de câblage ou les étapes ci-dessous pour construire votre circuit.

.. image:: img/24_flow_light.png
    :width: 600
    :align: center

1. Insérez 8 LED sur la plaque de montage, dans la configuration de couleur de votre choix. Assurez-vous que toutes les cathodes (jambes courtes) des LED sont connectées au rail de mise à la terre sur la plaque, tandis que les anodes sont connectées à des rangées séparées.

.. image:: img/24_flow_light_led.png
    :width: 500
    :align: center

2. Connectez une résistance de 220Ω à chaque anode des LED.

.. image:: img/24_flow_light_resistor.png
    :width: 500
    :align: center

3. Localisez la puce 74HC595 et insérez-la dans la plaque de montage. Assurez-vous que la puce traverse la séparation centrale.

.. note::

    Faites très attention à l'orientation du 74HC595 pour éviter de l'endommager. Vous pouvez identifier l'orientation correcte en utilisant les indices suivants :

    * L'étiquette sur la puce est orientée vers le haut.
    * L'encoche sur la puce est à gauche.

.. image:: img/24_flow_light_74hc595.png
    :width: 500
    :align: center

4. Connectez les broches VCC et MR du 74HC595 au rail positif de la plaque de montage.

.. image:: img/24_flow_light_vcc.png
    :width: 500
    :align: center

5. Connectez les broches CE et GND du 74HC595 au rail négatif de la plaque de montage.

.. image:: img/24_flow_light_gnd.png
    :width: 500
    :align: center

6. Connectez les broches Q0-Q7 du 74HC595 aux rangées de la plaque de montage contenant les résistances de 220Ω.

.. image:: img/24_flow_light_q0_q7.png
    :width: 500
    :align: center

7. Connectez la broche DS du 74HC595 à la broche 11 de l'Arduino Uno R3.

.. image:: img/24_flow_light_pin11.png
    :width: 600
    :align: center

8. Connectez la broche ST_CP du 74HC595 à la broche 12 de l'Arduino Uno R3.

.. image:: img/24_flow_light_pin12.png
    :width: 600
    :align: center

9. Connectez la broche Sh_CP du 74HC595 à la broche 8 de l'Arduino Uno R3.

.. image:: img/24_flow_light_pin8.png
    :width: 600
    :align: center

10. Enfin, connectez les broches GND et 5V de l'Arduino Uno R3 aux rails négatif et positif de la plaque de montage, respectivement.

.. image:: img/24_flow_light.png
    :width: 600
    :align: center

11. Le tableau suivant montre les connexions des broches entre le 74HC595 et l'Arduino Uno R3.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - Arduino UNO R3
    *   - VCC
        - 5V
    *   - Q0~Q7
        - LEDs 
    *   - DS
        - 11
    *   - CE
        - GND
    *   - ST_CP
        - 12
    *   - SH_CP
        - 8
    *   - MR
        - 5V
    *   - GND
        - GND


Création du code - Allumer les LEDs
--------------------------------------------

L'Arduino Uno R3 envoie des groupes de données binaires à la puce 74HC595.
Les données binaires sont au cœur des ordinateurs et de nombreux dispositifs électroniques, utilisant des 0 et des 1 pour traiter des données complexes et des instructions.
En informatique et en électronique numérique, les données binaires sont essentielles, car elles constituent la base du traitement de l'information et du stockage dans les ordinateurs électroniques.
Ici, 0 et 1 peuvent être considérés comme des états d'un interrupteur, où 0 représente éteint (fermé), et 1 représente allumé (ouvert).

Pour les nombres binaires, vous devez comprendre deux concepts de base :

* Bit : Un bit est l'unité de base dans le système binaire, et chaque bit peut être soit 0, soit 1.
* Octet : Un octet est composé de 8 bits. C'est une unité courante de traitement des données dans les ordinateurs. (Et regardez, la puce 74HC595 accepte exactement 1 octet de données à la fois !)

Les nombres binaires sont ordonnés du bit le moins significatif au plus significatif, avec le bit le plus à droite étant le moins significatif et celui le plus à gauche étant le plus significatif.

.. image:: img/24_binary_bit.png
    :width: 500
    :align: center

Voyons maintenant comment le 74HC595 reçoit des données binaires et les envoie aux LEDs !

1. Ouvrez l'Arduino IDE et démarrez un nouveau projet en sélectionnant "New Sketch" dans le menu "File".
2. Enregistrez votre projet sous le nom ``Lesson24_Lighting_up_LEDs`` en utilisant ``Ctrl + S`` ou en cliquant sur "Save".

3. Le contrôle du 74HC595 ne nécessite que trois broches pour fournir des signaux d'impulsion, donc définissez-les comme des sorties.

.. code-block:: Arduino

    const int STcp = 12;  // Broche connectée à ST_CP du 74HC595
    const int SHcp = 8;   // Broche connectée à SH_CP du 74HC595
    const int DS = 11;    // Broche connectée à DS du 74HC595

    void setup() {
        // Définir les broches en mode sortie
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

4. Votre ordinateur envoie des données binaires à la broche ``DS`` (entrée de données) du 74HC595, puis utilise le signal d'horloge provenant de la broche ``SH_CP`` (entrée de l'horloge du registre à décalage) pour faire avancer chaque bit de données. Ce processus de transmission de données peut être implémenté à l'aide de la fonction ``shiftOut()``.

    * ``shiftOut(dataPin, clockPin, bitOrder, value)`` : Décale un octet de données un bit à la fois. Le décalage commence soit par le bit le plus significatif (MSB), soit par le bit le moins significatif (LSB). Chaque bit est écrit successivement sur une broche de données, puis une broche d'horloge est activée (passée de haut à bas) pour indiquer que le bit est disponible.

    **Paramètres**

        * ``dataPin`` : La broche sur laquelle chaque bit sera envoyé. Type de données accepté : int.
        * ``clockPin`` : La broche à basculer une fois que la broche de données a été définie sur la valeur correcte. Type de données accepté : int.
        * ``bitOrder`` : L'ordre dans lequel décaler les bits : ``MSBFIRST`` ou ``LSBFIRST`` (bit le plus significatif ou bit le moins significatif en premier).
        * ``value`` : Les données à décaler. Type de données accepté : byte.

    **Retourne**
        Rien

5. Ici, nous essayons d'envoyer un octet (8 bits) de données au registre à décalage 74HC595 en utilisant la fonction ``shiftOut()``.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop()
    {
        shiftOut(DS, SHcp, MSBFIRST, B11101110);  // Décale les données, MSB en premier
    }

* Cela envoie les données ``B11101110`` (binaire, B signifie binaire) au registre à décalage du 74HC595, en commençant par le bit le plus significatif.
* Chaque fois que la broche ``SH_CP`` reçoit un signal de front montant (moment où la tension passe de bas à haut), les bits dans le registre à décalage sont décalés d'une étape.
* Par exemple, le bit 7 accepte la valeur précédente du bit 6, le bit 6 obtient la valeur du bit 5, etc.

.. image:: img/24_74hc595_shift.png
    :width: 500
    :align: center

6. Après que tous les bits de données ont été entrés via la broche DS et décalés à leur position correcte à l'aide de plusieurs signaux d'horloge, l'étape suivante consiste à copier ces données du registre à décalage vers un registre de stockage.

.. code-block:: Arduino
    :emphasize-lines: 2,7

    void loop() {
        digitalWrite(STcp, LOW);  // Relie ST_CP (broche de verrouillage) à la terre et maintient-la à LOW pendant la transmission des données
        
        // Envoie des données au registre à décalage en utilisant MSBFIRST (Bit le plus significatif en premier)
        shiftOut(DS, SHcp, MSBFIRST, B11101110);
        
        digitalWrite(STcp, HIGH);  // Tire ST_CP à HIGH pour enregistrer les données sur les broches de sortie
        
        delay(1000);  // Attends une seconde avant de répéter
    }

* Lorsque la broche ``ST_CP`` reçoit un signal de front montant, les données dans le registre à décalage sont copiées dans le registre de stockage.
* Une fois que les données sont copiées dans le registre de stockage, les LEDs connectées aux broches de sortie correspondantes (Q0 à Q7) s'allumeront ou resteront éteintes selon que les données sont 1 ou 0.

.. image:: img/24_74hc595_storage_1data.png
    :width: 300
    :align: center

7. Voici votre code complet. Vous pouvez maintenant téléverser ce code sur l'Arduino Uno R3. Ensuite, vous verrez que les LEDs connectées à Q0 et Q4 restent éteintes tandis que les autres LEDs sont allumées.

.. code-block:: Arduino

    const int STcp = 12;  // Broche connectée à ST_CP du 74HC595
    const int SHcp = 8;   // Broche connectée à SH_CP du 74HC595
    const int DS = 11;    // Broche connectée à DS du 74HC595

    void setup() {
        // Configurer les broches en mode sortie
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        digitalWrite(STcp, LOW);  // Relie ST_CP à la terre et maintient à LOW pendant la transmission
        shiftOut(DS, SHcp, MSBFIRST, B11101110);  // Décale les données, MSB en premier
        digitalWrite(STcp, HIGH);  // Tire ST_CP à HIGH pour enregistrer les données
        delay(1000);  // Attends une seconde
    }

**Question**

Que se passe-t-il si nous changeons ``MSBFIRST`` en ``LSBFIRST`` dans ``shiftOut(DS, SHcp, MSBFIRST, B11101110);`` ? Pourquoi ?



Création du code - Lumière défilante
------------------------------------------

Comment pourrions-nous implémenter un effet de lumière défilante, où les LEDs s'allument une par une ?

1. Ouvrez l'esquisse que vous avez enregistrée précédemment, ``Lesson24_Lighting_up_LEDs``. 

2. Cliquez sur "Enregistrer sous..." dans le menu "Fichier", et renommez-la ``Lesson24_Flowing_Light``. Cliquez sur "Enregistrer".

3. Ici, nous voulons configurer un effet de lumière défilante, où les LEDs s'allument une par une. Nous allons écrire les états allumés/éteints de cette séquence de lumière défilante sous forme de tableau.

.. code-block:: Arduino
    :emphasize-lines: 4

    const int STcp = 12;  // Broche connectée à ST_CP du 74HC595
    const int SHcp = 8;   // Broche connectée à SH_CP du 74HC595
    const int DS = 11;    // Broche connectée à DS du 74HC595
    int datArray[] = {B00000000, B00000001, B00000011, B00000111, B00001111, B00011111, B00111111, B01111111, B11111111};

4. Ensuite, utilisez une boucle ``for`` pour appeler séquentiellement ce tableau.

.. code-block:: Arduino
    :emphasize-lines: 3,5

    void loop()
    {
        for (int num = 0; num <= 8; num++) {
            digitalWrite(STcp, LOW);                      // Relie ST_CP à la terre et maintient à LOW pendant la transmission
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Décale les données, MSB en premier
            digitalWrite(STcp, HIGH);                     // Tire ST_CP à HIGH pour enregistrer les données
            delay(1000);                                  // Attends une seconde
        }
    }

5. Votre code complet est présenté ci-dessous. Vous pouvez maintenant téléverser ce code sur l'Arduino Uno R3, et vous verrez les LEDs s'allumer une par une, comme une lumière défilante.

.. code-block:: Arduino

    const int STcp = 12;  // Broche connectée à ST_CP du 74HC595
    const int SHcp = 8;   // Broche connectée à SH_CP du 74HC595
    const int DS = 11;    // Broche connectée à DS du 74HC595
    int datArray[] = {B00000000, B00000001, B00000011, B00000111, B00001111, B00011111, B00111111, B01111111, B11111111};

    void setup ()
    {
        // Configurer les broches en mode sortie
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop()
    {
        for (int num = 0; num <= 8; num++) {
            digitalWrite(STcp, LOW);                      // Relie ST_CP à la terre et maintient à LOW pendant la transmission
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Décale les données, MSB en premier
            digitalWrite(STcp, HIGH);                     // Tire ST_CP à HIGH pour enregistrer les données
            delay(1000);                                  // Attends une seconde
        }
    }

6. Enfin, n'oubliez pas de sauvegarder votre code et de ranger votre espace de travail.

**Question**

Si nous voulons que trois LEDs soient allumées à la fois et qu'elles apparaissent en "flux", comment les éléments du tableau ``datArray[]`` devraient-ils être modifiés ?

**Résumé**

Dans cette leçon, nous avons exploré la structure et la fonctionnalité de la puce 74HC595, en apprenant comment décaler des données binaires à travers son registre à décalage et construire une expérience de lumière défilante. En utilisant la fonction ``shiftOut()`` pour contrôler la transmission des données binaires, nous avons réussi à gérer l'allumage séquentiel de 8 LEDs pour obtenir un effet de lumière défilante. Avec cette nouvelle connaissance, vous devriez maintenant être capable d'utiliser efficacement la puce 74HC595 pour ajouter des fonctionnalités d'éclairage impressionnantes à vos propres projets.

