# Projet Majeur de Conception

## 1. Session 6 - Été 2024

### 1.1 Planification

Gestion de PMC avec un PLM de type MVP. Utilisation des outils comme  gantt... Toute la documentation se fera avec des fichier texte simple (markdown ou autre) pour éviter la dépendace au outils propriétaire. Tous graphiques seront au fromat .svg fait avec draw.io ou avec l'aide de [mermaid](https://github.com/mermaid-js/mermaid/tree/develop).

exemple de gants tirée de mermaid

```mermaid
gantt
    section S6
    Completed :done,    des1, 2024-01-06,2014-01-08
    Active        :active,  des2, 2024-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
```

### 1.2 Test préliminaire du niveau physique

Réaliser des tests pour choisir le niveau physique que SHER-Bus repose. Puisque c'est sr quoi repose tous ce que nous batirons nous devos s'assurer le plus tôt possible. les possiblitée sont M-LVDS,LVDS,B-LVDS, émulation de paire différentielle par io cmos. Nous devons faire ce travail avant de commencer a écrire la spécification car la spec dépend du niveau physique.

D'un autre côté, il faut évaluer la possibilitée d'ajout d'une *shear bolt* dans le bus. En effet, un des problème des comunication sur Bus (I2C,CAN, etc) est que si un circuit brise il amène toute la communication avec lui. Il faut ajouter une mesure pour que le bus fail de manière controlée et determinée. Cela permet de 

### 1.3 spécification

La spécification est le livrable le plus important du projet. Il permet a n'importe qui d'implémenter notre projet. C'est pour cela qu'elle doit être écrite le plus rapidement possible. la Session 7 permettra de valider la faisabilitée de la spécification.

### 1.4 Dévelopement d'Outils

Aucun outil n'est actuellement disponibles pour dévemiller un BUS SHER-Bus. Nous devons donc les créer. Pour ce faire nous devon nous mettre au plus vite a la création de ces outils. Il y a un simulteur de tramme python, un décodeur pour analyseur logique, et un générateur de séquence pseudo aléatoire.

#### 1.4.1 Simulateur python

Conception d'un convertisseur de trame binaire a un signal discrétisée dans le temps. 

#### 1.4.2 Décodeur [Sigrok/PulseView](https://sigrok.org/wiki/PulseView)

Pour vérifier l'intégritée des messages, il va falloir utiliser un décodeur. cette tache peut-etre fait a la main, mais elle est fastidieuse. Un programme qui convertis un trains de bits en information facilement lisible aide au débogage. [Le simulateur Python](https://github.com/cdg66/SHER-Bus/edit/add-PMC.md/PMC.md#141-simulateur-python) sera utilisée pour valider le décodeur.

#### 1.4.3 Générateur de *pseudorandom binary sequence (PRBS)*

Pour des test de bas niveau il va falloir vérifirer l'intégritée du diagramme en oeuil (*eye diagram* en anglais). La concepton sur RP2040 d'un PRBS vas nous permettre de facilement vérifirer les problème liée au paires croisée.

## 2. Automne 2024

### 2.1 Publication de la spécification et retour de la communautée open source

Lors du stage T4 la spécification sera publiée et la communautée open source sera invitée a discuter du projet. Elle sera invitée a proposer différent type d'application que le SHER-Bus pourrait suporter en plus de ceux déja pensée par l'équipe. 


## 3. Session 7 - Hiver 2024

### 3.1 Partie Matérielle

#### 3.1.1 Banc de Test

#### 3.1.2 Carte controleur/Bridge

### 3.2 Partie Logicielle

#### 3.2.1 VHDL PHY (Xilinx/Lattice)

#### 3.2.2 VHDL AXI2SHER-Bus (Xilinx)

#### 3.2.3 VHDL Bridge (Lattice)

#### 3.2.4 PIOasm Contrôleur (RP2040)

#### 3.2.5 C/C++ SHER-Bus middleware (RP2040/Xilinx)

#### 3.2.6 C/C++ USB2SHER-Bus end-bridge (RP2040)

## 4. Session 8 - Été 2025

### 4.1 conception d'un produit démo pour MégaGéniale

Bien qu'un la conception d'un bus 100% __*opensource*__ soit très intéressante, il est fort problable que cela captive pas l'attention du citoyen lambda. Avec tout ce qui a été concu avec la S7, la S8 sera consacrée a la production d'un produit démo ( bras robotisée, imprimante 3D, CNC, Casque audio, Grappe de serveurs [cluster-computer] ,etc,) utilisant SHER-Bus comme technogie principale. Le but est de montrer la technologie dans son meilleur état. le but étaut aussi de faire découvrir au concepteur la puissance de ce Bus comparée au alternative. 

