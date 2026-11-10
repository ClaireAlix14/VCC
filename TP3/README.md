## Etape 1

<img width="820" height="711" alt="architecture drawio" src="https://github.com/user-attachments/assets/84329397-11ba-4c59-b438-20d66b31cf03" />

## Etape 2

1. **Quels sont les différents rôles de la VM connectée à Internet dans votre architecture ?** La VM connectée à Internet sert de point d'entrée de l'application qui reçoit les requêtes des clients et fait appel aux VM sur lesquelles sont déployés les autres services. La VM sert aussi de proxy réseau qui permet de se connecter en ssh à nos différentes VM qui ne possèdent pas d'adresses IP flottantes
2. **Quels avantages apporte ce déploiement par rapport à une exécution de tous les services sur une seule machine ?** Ce déploiement permet de mieux tolérer les pannes, si un service tombe en panne, les autres ne sont pas impactés. Une meilleure répartition de la charge et une meilleure sécurité avec les VM cachées dans le réseau privé.

## Etape 3

1. **Quels flux réseau sont nécessaires au fonctionnement de votre application ?** Pour que l'application fonctionne, le flux public http depuis Internet vers la VM proxy est nécessaire pour que les clients accèdent au service. Des flux privés internes entre la VM proxy et les VM privées (microservices) sont également nécessaires.
2. **Pourquoi est-il préférable d’ouvrir uniquement les ports nécessaires plutôt que d’autoriser tout le trafic ?** Cela est préférable par mesure de sécurité pour réduire la surface d'attaque.
3. **Pouviez-vous utiliser Docker Compose pour déployer les services sur toutes les VM en simultané ? Pourquoi ?** Il n'était pas possible d'utiliser Docker Compose pour déployer les services sur toutes les VM en simultané car Docker Compose est conçu pour déployer des conteneurs sur une seule machine hôte or nous avons déployé notre application sur plusieurs VM distinctes.   
