## Etape 1 :

1. **Expliquez, avec vos propres mots, ce qu’est une machine virtuelle.** Une VM est un logiciel qui simule le comportement d'une machine physique avec ses propres ressources (CPU, mémoire, disque) virtuelles pour faire tourner un système d'exploitation isolé.
2. **Citez deux avantages de la virtualisation dans un environnement professionnel.** La virtualisation permet de reproduire plusieurs environnements sans avoir à partitionner un disque dur (si on doit alterner entre Linux et Windows par exemple). La virtualisation permet aussi une flexibilité et portabilité : il est facile de déplacer un environnement de travail entier d'une machine à une autre.
3. **Quelle différence existe-t-il entre travailler directement sur votre ordinateur et travailler dans une machine virtuelle ?** Du point de vue utilisateur, il n y a pas de différences notables une fois que la VM est configurée. Cependant, la configuration d'une VM peut être plus difficile qu'un simple démarrage de machine physique (problèmes allocation mémoire, performances, réseaux…). De plus, la connexion réseau est toujours plus fastidieuse sur VM (connaissance des IPs, id ssh…) pour pouvoir communiquer avec l'extérieur. Sur machine physique, on allume le PC et on est sur le réseau.

## Etape 2 :

1. **Expliquez, avec vos propres mots, ce qu’est un conteneur Docker.** Un conteneur encapsule et isole une seule application avec toutes les dépendances dont elle a besoin pour fonctionner, sans virtualiser une machine complète.
2. **Quelle différence fondamentale existe-t-il entre une machine virtuelle et un conteneur ?** La machine virtuelle a son propre OS alors quel le conteneur partage celui de la machine hôte.
3. **Pourquoi les conteneurs sont-ils particulièrement adaptés au déploiement d’applications dans le Cloud ?** Les conteneurs sont légers et rapides à démarrer par rapport à une VM comme ils ne contiennent pas d'OS complet. Cela les rend adaptés au déploiement d'application dans le Cloud et optimise les ressources des serveurs.

## Etape 3 :

1. **Pourquoi un Dockerfile est-il préférable à la configuration manuelle d’un conteneur ?** Un dockerfile est beaucoup plus rapide et permet la portabilité et l'automatisation de la création de l'environnement. D'autant plus que cela permet d'avoir la même configuration pour tous les conteneurs utilisant une même image.
2. **Quelle différence existe-t-il entre une image Docker et un conteneur Docker ?** L'image contient l'application (l'image est un modèle), et le conteneur est une instance de l'image.

## Etape 4 :

1. **Pourquoi Docker Compose est-il préférable au lancement manuel de plusieurs conteneurs ?** Docker compose permet de lancer plusieurs conteneurs en même temps. Cela est très utile lorsqu'on doit déployer plusieurs applications en même temps (ça évite de lancer et configurer chaque composant un par un).
2. **Quel est le rôle du fichier "docker-compose.yml" ?** Le fichier docker-compose.yml précise l'architecture de l'application, la configuration des conteneurs (images à utiliser, services, les ports, les réseaux…) 
3. **Dans quels cas Docker Compose pourrait-il avoir ses limites ?** Si on veut déployer des instances qui doivent communiquer, il va falloir configurer des réseaux virtuels de manière exponentielle. De plus, Docker Compose est conçu pour fonctionner sur une seule machine hôte. Si l'application doit être déployée de manière répartie sur plusieurs serveurs physiques, Docker Compose n'est plus suffisant.
