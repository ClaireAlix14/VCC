Etape 1 :

1. Une VM est un software qui reproduit un environnement de machine physique.
2. La virtualisation permet de reproduire plusieurs environnement sans avoir à partitionner un disque dur (si on doit alterner entre linux et Windows par exemple). 
La virtualisation permet aussi une portabilité qui pourrait charger un environnement de travail sur différentes machines (PC fixe sur site, PC portable en télétravail etc...).
3. Du point de vue utilisateur, il n y a pas de différences notables une fois qu'elle est configurée. Cependant, la configuration d'une VM peut être plus difficile qu'un simple démarrage de machine physique (problèmes allocation mémoire, performances…). De plus, la connexion réseau est toujours plus fastidieuse sur VM (connaissance des IPs, id ssh…). Sur machine physique, on allume le PC et on est sur le réseau.


Etape 2 :
1. Un conteneur est un environnement d'une seule application (avec ses dépendances).
2. La machine virtuelle a son propre OS alors quel le conteneur partage celui de la machine hôte.
3. Les conteneurs sont rapide par rapport à une VM, et leurs légèreté sont propices au déploiement dans le cloud

Etape 3 :

1. Un dockerfile est beaucoup plus rapide et permet la portabilité. D'autant plus que cela va permettre d'avoir la même configuration pour tous les conteneurs utilisant une même image.
2. L'image contient l'application, et le conteneur est une instance cette l'image (c'est l'environnement de l'app en gros).



Etape 4 :

1. Docker compose permet de lancer plusieurs conteneurs en même temps. Cela est très utiles lorsqu'on doit déployer plusieurs applications en même temps (ça évite de run plusieurs fois).
2.Le fichier docker-compose.yml précise la configuration des conteneurs (services, les ports…)
3. Si on veut déployer des insatnces qui doiveent communiquer, il va falloir configurer des réseaux virtuels de manière exponentielle.
