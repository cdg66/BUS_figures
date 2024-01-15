# Énoncée de la problématique

La compagine AInc qui se spécialise dans l'internet des objet, l'automatisation et [l'intéligence artificielle sur la pointe](https://www.redhat.com/en/topics/edge-computing/what-is-edge-ai) mendate votre équipe pour l'aider a régeler un problème qui limite l'avancement de la recherche et development de ses produits.

La compagie as déja sur le marchée plusieurs produits qui chaqun on un ou des microcontroleurs/fpga de multiple vendeur. Cela ammème beacoup de gestions, car la base de code est segementée au travers des different environnement de dévelopement(IDE). De plus, l'équipe d'inventaire se plaind de devoir gérer l'inventaire de ses circuits intégrée. Il arrive souvent que le mauvais  IC se retrouve sur la mauvaise ligne d'assemblage. Cela entraine des délais et cout supplémentaire. La compagie a donc décider de limiter sa dépendance au microcontroleur grâce a un processeur embarquée maison(ASIC). Elle veux donc un processeur capable d'être utilisée dans tout ses produits. Apres s'être arrêter sur un processeur RISC-V, elle a, cepandant, vite remarquée que le choix des périfiériques serait plus difficile. Chaque produit étant unique il ont aussi des requis uniques. le premier prototype de ce circuit à 350 pins pour répondre au besoins du produit X alors que le Produit Y a besoins d'un IC faisant 3x3mm ce qui est physiquement impossible. Il ont besoin d'une solution inovante au problème.

Votre collègue Claude-David vous propose de concevoir un protocole de communication assez rapide permmentant d'ajouter virtuelement de périphériques (I2c,CAN,SPI, Ethernet, composant analogique, GPIO, etc) a n'importe quelle processeur qui suporte le bus. Le but étant d'ajouter des fonctionnalité en fonction du produit. Il vous porpose aussi les critère de performance suivant.

1. le coûts de l'implémentation soit minimale
2. le protocole doit être simple (Pensez UART simple)
3. le protocole doit être performant et rapide
4. le protocole doit laisser place a une évolutivitée de la communication
5. le protocole doit minimiser sont usage de mémoire vive et morte
6. le protocole doit être facile a implémenter et programmée
7. le protocole doit avoir des fonctionalitée utile (efficacitée des ressources)
8. le protocole doit avoir une basse consomation d'énergie

## Rédaction de la Spécification

La première étape consiste a rédiger la spécification du bus. Le but de ce document est que n'imorte qui puisse comprendre et implémenter le bus. [une préspécification](https://github.com/cdg66/SHER-Bus/blob/main/README.md) à été 



## Prototypage du bus 

Après la spécification fixée il faut vérifier sa faisabilitée. Il faut concevoir les pcbs(kicad) et logiciels(python, C,C++, rust) pour vérifier que les critères de performances cité précédément soit respecté.

## Produit démo
La compagie veux voir en action votre travail et pour épater les investisseurs. la compagine vous demmande de metre au point une preuve de concept mettant en valeur le bus. elle vous donne carte blance pour celui-ci. 

# Liscence
La compagnie pense que placer le protocole sous une liscence ouverte pour premettre aux autres de developer des produit qui seront indirectement bénéfique a la compagnie.


