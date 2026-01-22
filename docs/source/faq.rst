.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Explorez plus en profondeur Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et relevez vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprenez et partagez** : Échangez des astuces et tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et concours** : Participez à des concours et à des promotions spéciales durant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

FAQ
====================

Que contient le kit ?
-------------------------------

Le kit comprend une carte Arduino Uno R3 ainsi qu’une variété de capteurs, de modules, de composants et d’accessoires pour réaliser des expériences et des projets.

Voir : :ref:`include_in_kit`


Quelle est la différence entre « Tutoriels vidéo » et « Leçons pratiques » ?
--------------------------------------------------------------------------------

* **Tutoriels vidéo** vous aident à comprendre les concepts et à voir des démonstrations.
* **Leçons pratiques** vous guident pour construire des circuits et écrire du code en utilisant les composants du kit.

Conseil :

* Regardez d’abord la vidéo, puis réalisez la leçon pratique pour une meilleure mémorisation.


Pourquoi l’Arduino UNO R3 ne peut pas être utilisé
---------------------------------------------------------------

Même en utilisant un Arduino UNO R3 officiel, la carte peut ne pas fonctionner correctement pour des raisons environnementales ou opérationnelles.  
Voici les causes et explications les plus courantes.

#. **Problèmes de pilote USB ou de système d’exploitation**

   L’Arduino UNO R3 utilise une puce d’interface USB **ATmega16U2**, qui est normalement reconnue automatiquement sous Windows 10 / 11 et macOS.
   
   Cependant, sur les systèmes plus anciens (comme Windows 7 ou des installations Windows légères), le pilote USB CDC requis peut être manquant.  
   Dans ce cas, l’ordinateur peut ne pas reconnaître le périphérique série Arduino.
   
   **Solution :**
   
   * Mettre à jour ou installer manuellement le pilote USB Arduino via le **Gestionnaire de périphériques**.
   * Il est recommandé d’inclure des instructions de mise à jour du pilote USB dans la FAQ pour référence.


#. **Carte ou port incorrect sélectionné dans l’IDE Arduino**

   Si la **Carte** ou le **Port** correct n’est pas sélectionné dans l’IDE Arduino, le téléversement des sketches échouera.
   
   Un message d’erreur courant est ::
   
       stk500_recv(): programmer not responding
   
   Il s’agit d’un problème de configuration et **n’indique pas un dommage matériel**.
   
   **Solution :**
   
   * Sélectionnez **Arduino UNO** dans *Outils → Carte*
   * Sélectionnez le port série correct dans *Outils → Port*


#. **Utilisation d’un hub USB ou d’un port USB instable**

   Si l’Arduino est connecté via :
   
   * des hubs USB
   * des ports USB d’écrans
   * des ports USB intégrés aux claviers
   
   L’alimentation et le signal peuvent être instables, ce qui peut empêcher l’énumération USB de l’Arduino.
   
   **Recommandation :**
   
   * Connectez l’Arduino **directement au port USB de l’ordinateur**.


#. Problèmes de port USB sur l’ordinateur

   Certains ports USB peuvent présenter des problèmes tels que :
   
   * une alimentation insuffisante (courant faible sur les ports USB en façade)
   * un mauvais contact physique
   * des ports USB endommagés
   
   **Recommandation :**
   
   * Essayez un autre port USB
   * Utilisez de préférence les **ports USB arrière de la carte mère**


#. Utilisation simultanée de l’alimentation USB et d’une alimentation externe

   Si l’Arduino est alimenté par USB tout en recevant une alimentation externe via **5V** ou **Vin**, cela peut provoquer :
   
   * un blocage du régulateur de tension
   * une surchauffe du circuit d’alimentation
   * une communication USB instable
   
   Cela peut faire apparaître l’Arduino comme déconnecté ou instable.
   
   **Recommandation :**
   
   * Évitez d’alimenter simultanément via USB et une alimentation externe, sauf si cela est nécessaire et correctement conçu.


#. **Erreurs de câblage provoquant des dommages à la puce USB**

   Lors de la connexion de modules externes, un câblage incorrect peut endommager la puce USB **ATmega16U2**, notamment :
   
   * inversion de **5V** et **GND**
   * application d’une tension élevée (comme 12V) sur les broches Arduino
   * conflits d’alimentation entre l’USB et les sources externes
   
   Dans ce cas, l’Arduino peut encore s’allumer, mais l’ordinateur ne reconnaîtra pas le port série.
   
   **Remarque :**
   
   Ce type de panne est causé par une mauvaise manipulation et **n’est pas un problème de qualité** de la carte Arduino elle-même.


Pourquoi le multimètre ne peut pas être utilisé
----------------------------------------------------------

Même si le multimètre lui-même fonctionne normalement, une utilisation incorrecte peut donner l’impression qu’il *ne s’allume pas* ou qu’il *ne peut pas mesurer*.  
Voici les causes et solutions les plus courantes.

#. **Batterie non installée**

   Bien qu’une pile 9V soit incluse dans le kit, elle doit être installée par l’utilisateur. Si aucune pile n’est installée, l’écran du multimètre ne s’allumera pas.
   
   Un tutoriel vidéo pour l’installation de la pile est disponible dans :ref:`use_multimeter`.

#. Cordons de test connectés aux mauvais ports

   Si le cordon rouge est inséré dans le port **10A** ou **mA**, le multimètre n’affichera pas de mesures lors de la mesure de tension ou de résistance.
   
   * Pour mesurer la tension ou la résistance :
   
     * Cordon rouge → **VΩ**
     * Cordon noir → **COM**

#. **Plage de mesure incorrecte sélectionnée**

   Si le mode sélectionné ne correspond pas à la mesure cible, par exemple :
   
   * Mesurer une tension DC avec la plage AC
   * Mesurer une tension en mode résistance
   
   Le multimètre n’affichera pas des valeurs correctes.
   
   **Solution :**
   
   * Sélectionnez la plage appropriée :
     * **DCV** pour la tension continue
     * **Ω** pour la résistance

#. Le multimètre s’allume mais ne peut pas mesurer

   Si le multimètre affiche des valeurs mais ne mesure pas avec précision, les cordons de test peuvent être endommagés.
   
   Des tractions ou torsions répétées peuvent provoquer une rupture interne des fils et un contact instable.
   
   **Solution :**
   
   * Remplacez les cordons de test si des lectures instables ou intermittentes se produisent


Comment exécuter mon premier programme Arduino ?
------------------------------------------------

1. Connectez la carte Arduino à votre ordinateur à l’aide d’un câble USB.
2. Ouvrez l’IDE Arduino et sélectionnez la **Carte** et le **Port** corrects.
3. Ouvrez un sketch d’exemple (comme Blink) et cliquez sur **Téléverser**.
4. Vérifiez le comportement de la LED intégrée pour confirmer que cela fonctionne.

Voir : :ref:`first_sketch`


Mon circuit ne fonctionne pas comme prévu. Que dois-je faire en premier ?
---------------------------------------------------------------------------------------

* Revérifiez le câblage par rapport au schéma du tutoriel (la plupart des problèmes sont des erreurs de câblage).
* Vérifiez la polarité des composants (sens des LED, polarité des condensateurs électrolytiques, etc.).
* Confirmez que l’alimentation et la masse sont correctement connectées.
* Utilisez un multimètre pour vérifier la tension aux points clés si disponible.

