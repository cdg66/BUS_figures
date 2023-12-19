# Précisions concernant le PMC

Voici quelques points que je souhaite clarifier concernant le projet Sher-Bus :

## Objectif peu clair...

L'objectif final serait de développer un silicium entièrement personnalisé ([ASIC](https://fr.wikipedia.org/wiki/Application-specific_integrated_circuit)) implémentant le bus de communication. Je suis conscient que c'est impossible dans le temps imparti. Ainsi, je vise à concevoir un prototype avec FPGA et microcontrôleur. L'objectif de ce bus est de réduire les coûts de développement et de maximiser l'évolutivité des produits embarquant des microcontrôleurs. Mon expérience dans ce domaine m'a montré que ces contrôleurs sont trop monolithiques pour le cycle de vie des produits modernes. Les premiers microcontrôleurs sont apparus dans les années 70, à une époque où le cycle de développement et de vie des produits était de quelques années. Aujourd'hui, il est souvent réduit à quelques mois. Les périphériques, les Entrées/Sorties et la mémoire sont limités sur ces petites boîtes noires, et il arrive fréquemment, durant le développement, que l'une de ces ressources vienne à manquer. [Voici un exemple concret.](https://youtu.be/SFrUINyYcEA?feature=shared&t=52) Pouvoir ajouter des périphériques et des Entrées/Sorties tout en minimisant l'utilisation de la mémoire est l'objectif de SHER-Bus. Pour plus de clarté, j'ai composé quelques [exemples](https://github.com/cdg66/SHER-Bus/blob/main/PMC/Examples_application.md) où SHER-Bus aurait sa place comme technologie principale.

##  << Plusieurs protocoles open-source existants >>

À ma connaissance, les seuls protocoles open-source que je connais sont l'Ethernet et ceux qui sont tombés dans le domaine public, comme le SPI.

En ce qui concerne l'Ethernet, il est excellent pour les réseaux à longue distance, mais inadapté pour les systèmes embarqués. Il requiert une pile logicielle complexe consommant beaucoup de mémoire flash. En expérience, ce qui coûte cher sur un microcontrôleur, ce sont la RAM, la FLASH et les E/S. L'Ethernet utilise abondamment ces précieuses ressources.

Quant aux protocoles comme le SPI et l'I2C, ils sont lent difficiles à utiliser pour une communication CPU à CPU. Pour cela on utilise le bon vieux uart,mais ne trouvez vous pas cela triste que dans les produits modernes on utilise encore des technologie de communication dévelopée dans les années 60?

## << Pertinence quasi-nulle, car on implémente un protocole qui utilise les autres protocoles >>, << Pas distinctif de ce qui est offert sur le marché (voir JESD-204) >>

Le but n'est pas de concurrencer les protocoles déjà existants, mais de leur apporter une valeur ajoutée. Je ne cherche pas à créer une guerre de formats (pensez [mini disk](https://fr.wikipedia.org/wiki/MiniDisc) et [memory stick](https://fr.wikipedia.org/wiki/Memory_Stick)). Par le passé, plusieurs personnes ont tenté d'introduire de nouveaux standards sur le marché et ont échoué lamentablement. Les principales raisons en sont le manque de support logiciel et, par conséquent, le manque d'utilisateurs (un cercle vicieux).

![standard](https://imgs.xkcd.com/comics/standards.png)

De plus, soyons honnêtes, les programmeurs sont paresseux. Ils veulent réécrire le moins de code possible. Le fait que le protocole nécessite un minimum d'adaptation (un périphérique I2C reste un périphérique I2C mais à un niveau physique différent) dans la base de code apporte une valeur ajoutée à l'implémenteur en accélérant le temps de développement. Par exemple, dans l'industrie automobile/industrielle, l'utilisation de piles  CAN préétablies est courante. Le fait que SHER-Bus soit déjà compatible avec un minimum de surcharge et offre un avantage considérable à quiconque souhaite moderniser la communication de son produit. Ces industries sont en transition lente vers [l'Ethernet à paire unique](https://www.digikey.ca/en/resources/technology/single-pair-ethernet), mais cela nécessite une refonte complète de la base de code existante, ce qui rejoint un peu l'argument précédent.
