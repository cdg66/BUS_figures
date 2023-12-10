# Précision quant au PMC

Voici quelques points que je voulais clarifier au niveau du projet Sher-Bus

## Objectif pas clair...

L'objectif final serait d'avoir du silicum complètement custom([ASIC](https://fr.wikipedia.org/wiki/Application-specific_integrated_circuit)) implémentant le bus de communication. Je sais très bien que c'est impossible dans le temps alouée. ALors je veux faire un prototype avec FPGA et Microcontroleur. le but avec ce bus est de réduire les cout de dévelopement et de maximiser l'amélioration continue(leaving room for growth) des produt embarquant des microcontroleurs. J'ai remarquée avec mon expérience dans le domaine que ces controleurs sont trop monolitique pour le cycle de vie des produits modernes. Les premiers microcontoleurs on  commencer à apparaitre dans les années 70 là ou le temps de dévelopement et le cyle de vie des produit était de quelques années. Aujourd'hui il sont souvent que de quelques mois. Les périféiques, les IO et la mémoire sont limitée sur ses peties boites noirs et il arrive souvent pendant le dévelopement que l'on manque d'une de ses ressources. [voici un exemple réel.](https://youtu.be/SFrUINyYcEA?feature=shared&t=52) Il serait bien pratique de pouvoir ajouter des périférique et IO tout en minimisant l'utilisations de la mémoire. C'est ça le but de SHER-Bus.

##  << Plusieurs protocoles open-source existants >>

A ce que je sache, les seuls protocole opensource que je connaisse sont l'ethernet et les protocoles tombée dans le domaine public tel que le SPI. 

En ce qui concerme l'Ethernet est supper pour ce qui est de la résautique a longe distance. cepandant il est atroce dans le monde de l'embarquée. Il a besoin d'une stack logicielle très complexe qui demmande beaucoup de flash. D'expérience ce qui coute cher sur un microcontroleur c'est la RAM la FLASH et les IO. L.ethernet prend baucoup de ces précieuse ressources.

En ce qui concerne les protocoles comme le SPI,I2C ceux ci sont difficile a utiliser pour une communication CPU à CPU.

## << pertinence quasi-nulle, car on implémente un protocole qui utilise les autres protocole >>,<< pas distinctif de ce qui est offert sur le marché (voir JESD-204) >>

le but n'est pas de concurencer les protocoles déjà existant mes bien de leur donner un valeur ajoutée. Je ne veux pas d'une autre format war(pensez [mini disk](https://fr.wikipedia.org/wiki/MiniDisc) et [memory stick](https://fr.wikipedia.org/wiki/Memory_Stick)). Par le passée plusieurs pesonne on déjà essayée d'ammener un noveau standard sur le marché et on échouée lamentablement. Les principales raisons sont le manque de support logiciel et de par le même fait le manque d'utilisateur(cercle vicieux). 

![standard](https://imgs.xkcd.com/comics/standards.png)

Disons le les programmeurs sont lazy. Il veulent réécrire du code le moins possible. le fait que le protocol demmande un minimum d'adaptation(un device i2c reste un device I2C juste différent niveau physique) de la codebase donne une plus value pour l'implémenteur en accélérant le temps de dévelopement. Par exemple, dans le monde de l'automotive/industriel repose déjà sur des stack CAN préétablis. Le fait que SHER-Bus soit déjà compatible avec un minimum d'overhead et un gros plus pour quiconque veux moderniser la communication de leur produit. Ces industries sont en lente tansition vers [le single pair ethernet](https://www.digikey.ca/en/resources/technology/single-pair-ethernet) mais cela demmande un redsing complet de la codebase existante et reviens un peux a l'argument précédent.


