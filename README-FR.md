# Spécification préliminaire de SHER-Bus
> **Avertissement**
> Le contenu n'est pas fixe et peut changer sans préavis !
>
# Spécification préliminaire de SHER-Bus
> **Avertissement**
> Traduit en francais par AI

**SHER-Bus** signifie :

**S**ystemwide **H**ub for **E**fficient **R**outing **Bus** 

et

**S**HER-Bus **H**andles **E**xtensive **R**esource **B**ridging, **U**nifying **S**ystems

![Disposition du bus](https://github.com/cdg66/SHER-BUS_figures/blob/main/BUS_layout.svg)

## Qu'est-ce que SHER-Bus ?

C'est un bus série conçu pour regrouper de nombreux bus série à basse vitesse que l'on trouve dans l'électronique moderne en un ou plusieurs paires de bus à haute vitesse en mode différentiel. Des exemples de bus série à basse vitesse sont SPI, I2C, CAN, PWM, PCM, etc. Fini le temps où vous vous rendiez compte que vous n'aviez pas assez de bus I2C ou d'UART.

Ce bus peut également prendre en charge des utilisations plus générales, telles que l'interface homme-machine (clavier, pavé numérique, manette de jeu, joysticks), l'audio (I2S, SPDIF), la vidéo à basse résolution (OLED monochrome, écran LCD TFT SPI), le contrôle moteur (moteur pas à pas), les entrées/sorties à usage général (GPIO), la gestion de la batterie (SOC, DOD, SOH, série, parallèle, courant de charge/décharge, tension, température), etc.

SHER-Bus est également idéal pour les communications à usage général (comme UART, JSON, protobuf, Modbus, etc.) entre les contrôleurs.

## Pourquoi SHER-Bus ?

Sherbus est né de la frustration de travailler avec de nombreux protocoles de communication gonflés, lents ou propriétaires dans les dispositifs embarqués. Sherbus est léger et facile à comprendre pour quiconque, du bricoleur au concepteur vétéran. Le protocole est modulaire (seule la couche de protocole [P] est obligatoire). Cette modularité donne aux implémentateurs la liberté de modeler la communication en fonction du produit et non l'inverse. Les implémentateurs n'auront pas besoin de gérer une pile complexe pour quelque chose de simple (comme par exemple une classe USB CDC complète pour un UART de base). La complexité du logiciel est conçue pour évoluer avec la complexité du bus. En d'autres termes, les tâches simples sont facilement accomplies sur un bus simple. En revanche, plus de fonctionnalités sont ajoutées, plus de précautions (par exemple, identification de la position du bus, canaux multiples, etc.) doivent être prises pour garantir l'intégrité du bus. Cela signifie que le seuil d'entrée est très bas, mais le bus est suffisamment puissant pour gérer des tâches complexes lorsque les implémentateurs en ont besoin. C'est là l'innovation que détient SHER-Bus, car les protocoles actuels sont soit trop complexes pour des tâches simples (une pile USB peut occuper la plupart de l'espace programme sur la plupart des microcontrôleurs, même Tiny-USB), soit trop simples pour des tâches complexes. SHER-Bus est à la fois simple pour des tâches simples et riche en ressources pour les utilisateurs avancés.

Un autre point expliquant pourquoi nous avons besoin d'un protocole comme SHER-Bus est que, tout comme RISC-V a contribué à ouvrir le marché des CPU aux IP sans licence pour les CPU, de nombreux systèmes sur puce nécessitent l'utilisation d'IP propriétaires pour leur connectivité. Un objectif de SHER-Bus est qu'un jour un SOC 100 % gratuit et open source fera son apparition sur le marché. Avec l'aide de SHER-Bus et de nombreux autres projets comme celui-ci, la communauté open source peut atteindre cet objectif.

![FreeSOC](https://github.com/cdg66/SHER-BUS_figures/blob/main/SOC.svg)

## Conception du bus
> **Avertissement**
> MLVDS n'est pas un choix fixe et est sujet à des tests et à des comparaisons de prix (les transmetteurs MLVDS sont chers !)

Le bus est basé sur le M-LVDS (alias TIA/EIA-899). Il est conçu pour prendre en charge le multipoint dès le départ. Le bus est câblé en mode "ou" (niveau élevé dominant). Jusqu'à 32 périphériques (30 contrôleurs/ponts et 2 ponts de terminaison) peuvent être connectés à une seule voie différentielle. Bien que 30 périphériques puissent sembler limités, la limite théorique de périphériques I2C sur SHER-Bus est de 22098 ![^1]. Des connexions série multiples (comme dans un châssis arrière) peuvent être ajoutées pour augmenter le débit. L'horloge est intégrée dans le flux de données, il n'est donc pas nécessaire d'ajouter une voie d'horloge. Une horloge optionnelle peut être ajoutée pour synchroniser des fonctions telles que l'audio. Il utilise un codage de 8 bits à 10 bits sur la couche physique pour garantir l'équilibre continu et offrir une première couche de vérification des erreurs.

[^1] : 127 périphériques I2C * 6 ports maîtres I2C sur 1 pont * 29 ponts (nous avons besoin d'au moins 1 contrôleur) = 22098

## Périphériques du bus

![Types de périphériques](https://github.com/cdg66/SHER-BUS_figures/blob/main/Controller_Bridge.svg)

Il n'y a que 3 types de périphériques qui remplissent différentes fonctions dans le réseau de bus.

Tout d'abord, il y a le contrôleur qui génère des paquets de données pour que d'autres les analysent. Ils donnent au bus sa fonction. Par exemple, le contrôleur peut donner des commandes à un pont pour qu'il lise un capteur de température I2C. Le contrôleur interprète ensuite ces données et ajuste un DAC SPI pour générer une valeur pour le contrôle d'un ventilateur. Ils peuvent également donner des commandes à d'autres contrôleurs sur le même bus. Autrement dit, leur rôle est d'être le cerveau de la communication. Ils se composent principalement de microcontrôleurs, d'ordinateurs embarqués (Raspberry Pi) ou de FPGA.

![Exemple de contrôleur](https://github.com/cdg66/SHER-BUS_figures/blob/main/Controler_example.svg)

Deuxièmement, il y a le pont, dont le rôle est de combler l'écart entre le nouveau bus et le protocole déjà existant. Ils peuvent prendre en charge de nombreux bus série (jusqu'à 6 et 1 canal de contrôle général utilisant [BPI]). Ils se composent principalement d'ASIC ou de FPGA. Bien qu'au moment de la rédaction de ce document, aucun code ASIC ou FPGA n'ait été fabriqué/écrit. Les microcontrôleurs peuvent également agir en tant que ponts. Les ponts peuvent être intégrés dans des conceptions déjà existantes sur puce ou dans des boîtiers multi-puces. En suivant la conception, une fois réutilisée, elle contribue à réduire la complexité de la refonte et à accélérer le délai de mise sur le marché. Les implémentateurs de pont doivent être attentifs à la licence des bus existants, car certains ne sont pas libres d'utilisation.

![Conception multi-puces](https://github.com/cdg66/SHER-BUS_figures/blob/main/Intergrated_bridge.svg)

Troisièmement, il y a le pont de terminaison, dont le rôle est de connecter plusieurs SHER-Bus ensemble ou d'autres bus à HAUTE VITESSE (comme l'USB, le SDIO ou l'Ethernet). Ils terminent le bus (là où se trouvent les résistances de terminaison), c'est pourquoi il y a une limite de 2 qui peuvent être connectés au bus. Ils sont complexes et non obligatoires.

## Architecture des paquets

L'architecture des paquets suit la même philosophie que l'architecture CPU RISC-V. Un seul ensemble d'instructions est obligatoire, et chaque ensemble est étiqueté par une lettre (par exemple, I M C A F D Q pour le CPU RISC-V) ou un mot/acronyme (par exemple, Zicsr). Ce qui est différent en raison de la nature de la communication, c'est que chaque couche est intégrée dans la charge utile des couches situées en dessous. Par exemple, un paquet audio (A) est intégré dans un paquet d'identification du protocole de bus [BPI], qui est à son tour intégré dans un paquet de flux (S), qui est à son tour intégré dans un paquet de protocole (S). Nous avons des structures comme P(S(BPI(A))), mais si ce message audio est adressé à tout le monde sur le bus, nous pouvons supprimer la couche BPI et avoir des messages structurés de la sorte : P(S(A)). Cela augmente considérablement la flexibilité du bus. Un récepteur peut effectuer un masque ET sur l'ensemble du message pour voir s'il est d'intérêt pour lui et éliminer ceux qui ne le sont pas (par exemple, un pont I2C ne se soucie pas d'un message audio (A), mais un pont I2S le fait).

![Transaction](https://github.com/cdg66/SHER-BUS_figures/blob/main/Protocol_stack.svg)

### Couche de protocole (P)

La couche de protocole est la seule couche obligatoire de la spécification. Elle gère le minimum pour qu'une transaction soit valide. Les implémentateurs utilisent cette couche pour envoyer des messages de très bas niveau, tels qu'une communication de type point à point similaire à un UART, car l'adressage est géré uniquement à un niveau supérieur, seule une configuration de bus en point à point ou multidiffusion est possible en utilisant uniquement ce niveau. C'est une fonctionnalité, car dans de nombreuses applications, vous ne voudriez pas d'une pile lourde pour quelque chose de simple. Cela accorde également aux implémentateurs la liberté de créer des piles de protocoles personnalisées pour les applications qui ne sont pas couvertes par la pile existante (par exemple, SAE J1939 et CanOPEN sont toutes deux des piles construites sur la nature non contraignante du protocole CAN, SHER-Bus essaie de faire la même chose, mais gratuitement, en ayant une pile commune, ce qui aide l'implémenteur de pont et l'implémenteur de bus à avoir un terrain commun pour travailler). Le premier octet sert à indiquer s'il s'agit d'un paquet standard ou personnalisé. Un un (1) sur le MSB du premier octet indique que la charge utile est un message conforme à SER-Bus. Les implémentateurs peuvent envoyer des messages personnalisés en réglant le premier octet sur 0 (0x00).

![Types de périphériques](https://github.com/cdg66/SHER-BUS_figures/blob/main/(P).svg)

### Couche réseau

![Types de périphériques](https://github.com/cdg66/SHER-BUS_figures/blob/main/(CIBS).svg)

#### Messages de contrôle (C)

Les messages de contrôle sont utilisés pour modifier la façon dont le bus ou un périphérique réagit. Par exemple, un implémentateur peut effectuer une réinitialisation de périphérique. Ils sont également utilisés par la couche [BPI] pour l'adressage dynamique.

#### Messages d'interruption (I)

Les messages d'interruption sont conçus pour être aussi proches que possible des interruptions informatiques. Ils peuvent utiliser la couche [BPI], mais ils sont destinés davantage à l'attention du bus. Par exemple, un convertisseur A/N peut envoyer une interruption pour indiquer qu'il est prêt à être lu.

#### Messages de boomerang (B)

Les messages de boomerang, comme leur nom l'indique, sont destinés à revenir à l'expéditeur. À la réception d'un message (B), le récepteur l'utilise pour effectuer une action, puis renvoie le même message avec des modifications en fonction de cette action. Les messages (B) sont une exception car ils doivent prendre en charge les messages d'identification de la position du bus, sinon tout le monde sur le bus renverrait le message. Le renvoi du même message garantit également qu'il a été reçu correctement et permet la désynchronisation des transactions (l'aller-retour peut se produire avec d'autres messages pour les séparer). Un exemple serait une lecture I2C sur le bus. Un contrôleur pourrait demander la lecture de l'adresse W X du slave I2C sur le bus Y I2C du pont Z. Le pont répondrait après avoir effectué la lecture qu'il a reçu n octets de données de l'adresse W X du slave I2C sur le bus Y I2C en renvoyant le même message mais en échangeant les octets récepteur/transmetteur de la couche [BPI] et en ajoutant les données lues.

#### Messages de flux (S)

Les messages de flux sont destinés aux cas où l'intégrité des données n'est pas importante, mais un flux constant de données l'est. Les messages de flux sont destinés à un flux audio, par exemple. Il n'est pas grave si un ou deux paquets sont perdus, il vaut mieux avoir un flux constant de paquets. Les messages de flux sont plus performants s'ils sont sur un bus séparé, car ils ont la priorité la plus basse.

### Identification de la position du bus (BPI)

L'identification de la position du bus donne au contrôleur un moyen de parler à un périphérique spécifique tandis que les autres restent inchangés. Les ponts doivent prendre en charge le BPI car ils ne savent jamais à quel bus ils appartiendront. Chaque périphérique peut avoir jusqu'à 7 sous-périphériques. Le sous-périphérique 0 est réservé au contrôle ou lorsque les sous-périphériques ne sont pas utilisés. Les périphériques peuvent obtenir une adresse de 3 manières possibles : statiquement, pseudo-dynamiquement et dynamiquement.

![Transaction](https://github.com/cdg66/SHER-BUS_figures/blob/main/(BPI).svg)

#### Adressage statique

Chaque périphérique sur le bus a une adresse prédéterminée qui ne change pas. Il incombe à l'implémenteur du bus de définir une adresse unique à chaque périphérique présent sur le bus. Ce mode d'adressage est utile lorsque l'implémenteur connaît la disposition du bus et qu'elle ne change pas, comme dans un système complètement clos sans ports extérieurs. À documenter.

#### Adressage pseudo-dynamique

Chaque périphérique obtient son adresse en utilisant une méthode externe. Par exemple, dans un châssis arrière, chaque emplacement est étiqueté électroniquement (GPIO ou EEPROM I2C) avec une adresse unique. Les périphériques SHER-Bus lisent cette adresse au démarrage et l'utilisent pour la communication. À documenter.

#### Adressage dynamique

Chaque périphérique obtient son adresse en demandant au SHER-Bus à l'aide d'un message de contrôle (C). À documenter.

### Messages de haut niveau
> **Avertissement**
> À écrire
### Exemple de transaction
![Pile de protocoles](https://github.com/cdg66/SHER-BUS_figures/blob/main/example_message.svg)
