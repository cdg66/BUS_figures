### Exemple 1: Drone

![VAMUdeS thirst trap](https://github.com/cdg66/SHER-Bus/blob/main/Figures/Drone.svg)

Dans une configuration de ce type, SHER-Bus pourrait théoriquement prendre en charge jusqu'à 24 moteurs BLDC. Il serait donc aisé d'adapter l'architecture du drone à un quadrirotor, hexacoptère ou heptacoptère, que ce soit pour une augmentation ou une diminution de l'échelle.

### Exemple 2: Ordinateur portable Framework

[Framework Laptop](https://frame.work/ca/en/products/laptop16-diy-amd-7040)

Si vous n'en avez pas encore connaissance, la société Framework a conçu un ordinateur portable capable de modifier ses périphériques et leur configuration "en temps réel" (*on-the-fly*) en utilisant l'USB 2.0. Cependant, cela implique une gestion complexe en arrière (avec l'utilisation de hubs, etc.) car les ports USB sont limités sur un ordinateur portable. Chaque port doit avoir sa propre paire différentielle ainsi qu'une alimentation, ce qui entraîne un câblage considérable et, par conséquent, une augmentation des coûts. Avec SHER-Bus, une seule paire pourrait desservir tous les modules et se connecter à un seul port USB (via un pont), économisant ainsi de précieuses ressources (câbles, ports USB, etc.).

### Exemple 3: Capture de mouvement

![mouvement](https://github.com/cdg66/SHER-Bus/blob/main/Figures/Mouvement.svg)

Un exemple concret serait la conception d'un vêtement (comme une chemise) permettant de suivre les mouvements d'une personne à des fins VR/AR/médicales. Sur le schéma ci-dessus, on remarque rapidement que plus le nombre d'IMU augmente, plus la complexité du câblage augmente, ce qui pose problème lorsque le produit doit être aussi léger que possible pour ne pas limiter les mouvements. De plus, l'I2C est un bus très lent, ce qui limite la vitesse d'acquisition et donc la quantité de données utilisables. Cependant, avec une adoption généralisée du bus SHER-Bus, un fabricant d'IMU pourrait proposer un capteur doté d'un port SHER-Bus natif.

### Exemple 4: Batterie pour véhicule électrique (EV)

![BMS](https://github.com/cdg66/SHER-Bus/blob/main/Figures/Battery.svg)
La majorité des contrôleurs de batterie pour véhicules électriques utilise le SPI isolé ([un exemple](https://www.analog.com/media/en/technical-documentation/data-sheets/LTC6806.pdf)). SHER-Bus serait très utile grâce à sa proximité matérielle et à son débit rapide, ce qui en ferait un candidat parfait pour cette application.

### Exemple 5: liaison de deux protocoles incompatible

![MQTT et CANopen](https://github.com/cdg66/SHER-Bus/blob/main/Figures/MQTT_CANopen.svg)

Dans cette application le système doit lier deux protocoles complètement différent et incompatible. Dans un cas nous avons une pile logicielle [MQTT](https://mqtt.org/) pour les applications IOT. De l'autre nous avons le [CANopen](https://www.can-cia.org/canopen/) une pille utilisant le CAN pour l'automation. Il existe bien des [Ponts matérielle](http://www.adfweb.com/download/filefold/MN67940_ENG.pdf) entre les deux. Cependant il sont limitée en fonction. Si les deux sont suportée par SHER-Bus alors le pont se peut faire très facilement. Comme on peut le voir sur le schéma l'_Application Processor_ fait le liens entre CANopen et MQTT et ce même s'il sont connectée sur le même bus. Les device MQTT ignore les message CANopen et inversement.

