#Example 

voici 3 exemples ou SHER-Bus résaurait un/des problèmes au niveau de l'électronique moderne.

## 1 drone

## 2 [framework laptop](https://frame.work/ca/en/products/laptop16-diy-amd-7040)

Si vous ne le savez pas déjà la compagnie framework on concu un portable capable de changer ses périférique et leur configuration *on-the-fly* il on réussi cet exploit en utilisant l'USB 2.0. Cepandant cela implique une lourde gestion *under-the-hood* (utilisation de hub etc) car les ports USB sont limitée sur un portable. Chaque port doit avoir sa paire différentielle plus alimentation ce qui fait beacoup de cablage et ainsi augmentant les coûts. Avec SHER-Bus une seule paire déservirait tout les modules et se connecterait a un seul port usb(via un BRIDGE) économisant ainsi les précieuse ressource(cables, ports usb ,etc).

## 3 Capture de mouvement.

![mouvement](https://github.com/cdg66/SHER-Bus/blob/main/Figures/Mouvement.svg)

L'exemple suivant serait la conception d'un vêtement(chemise) perettant le sivit de mouvement d'une personne pour des application VR/AR/Médicale. sur le diagramme du haut on se rend vite compte que plus le nombre d'IMU augemente plus la complexitée du cablage augemente ce qui est un problème quand le produit doit être le plus léger possible pour ne pas restreindre les mouvements. De plus l'i2c est un bus très lent ce qui limite la vitesse d'acquision et ainsi la quantitée de donnée utilisable.