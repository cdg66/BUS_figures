# Problématique

La compagnie AInc, experte en Internet des objets, automatisation et [intelligence artificielle de pointe](https://www.redhat.com/en/topics/edge-computing/what-is-edge-ai), missionne votre équipe pour résoudre un problème freinant la recherche et le développement de ses produits.

La compagnie a déjà lancé plusieurs produits sur le marché, chacun équipé de microcontrôleurs/FPGA provenant de divers vendeurs. Cette diversité engendre une gestion complexe, la base de code étant segmentée à travers différents environnements de développement (IDE). De plus, l'équipe d'inventaire se plaint de la gestion des circuits intégrés, avec des erreurs fréquentes dans les lignes d'assemblage, entraînant des retards et des coûts supplémentaires. Ainsi, la compagnie souhaite réduire sa dépendance aux microcontrôleurs en adoptant un processeur embarqué maison (ASIC) pour une utilisation homogène dans tous ses produits. Après avoir opté pour un processeur RISC-V, le défi se porte sur le choix des périphériques, chaque produit ayant des besoins uniques. Par exemple, le premier prototype de circuit a 350 broches pour répondre aux besoins du produit X, tandis que le Produit Y nécessite un CI de 3x3 mm, ce qui est physiquement impossible. Une solution innovante est nécessaire.

Claude-David propose de concevoir un protocole de communication rapide permettant d'ajouter virtuellement des périphériques (I2C, CAN, SPI, Ethernet, composant analogique, GPIO, etc.) à n'importe quel processeur prenant en charge le bus. L'objectif est d'ajouter des fonctionnalités adaptées à chaque produit. Il propose également des critères de performance :

1. Coût minimal d'implémentation.
2. Simplicité du protocole (pensée comme un UART simple).
3. Performance et rapidité du protocole.
4. Évolutivité de la communication.
5. Minimisation de l'utilisation de mémoire vive et morte.
6. Facilité d'implémentation et de programmation du protocole.
7. Efficacitée
8. Basse consommation d'énergie du protocole.

## Rédaction de la Spécification

La première étape consiste à rédiger la spécification du bus. L'objectif est que tout individu puisse comprendre et implémenter le bus. [Une pré-spécification](https://github.com/cdg66/SHER-Bus/blob/main/README.md) a été 

## Prototypage du bus 

Après avoir fixé la spécification, la vérification de sa faisabilité est nécessaire. Il faut concevoir les PCBs (KiCad) et les logiciels (Python, C, C++, Rust) pour s'assurer du respect des critères de performances mentionnés précédemment.

## Produit démo

La compagnie souhaite voir en action votre travail pour impressionner les investisseurs. Elle vous demande de développer une preuve de concept mettant en valeur le bus. Vous avez carte blanche pour cela.

# Licence

La compagnie envisage de placer le protocole sous une licence ouverte pour permettre à d'autres de développer des produits bénéfiques indirectement à la compagnie.
