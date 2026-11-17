## Etape 1

1. **Pourquoi est-il nécessaire que Jenkins puisse communiquer avec VM-K8s et VM-Registry ?** Jenkins tourne sur une machine isolée et a besoin d'accéder au Registry pour push les images Docker qu'il construit et au cluster Kubernetes pour lui donner l'ordre de mettre à jour les applications avec ces nouvelles images.
2. **Quel est le rôle de Jenkins dans la chaîne CI/CD ?** Jenkins est le chef d'orchestre de la chaîne CI/CD. Il automatise, coordonne et exécute toutes les étapes (récupération du code, compilation, création d'artefacts et déploiement).

## Etape 2

1. **Quelles opérations réalisées manuellement dans le TP1 ont été automatisées par Jenkins ?** La récupération du code depuis Git, la construction des images et leur publication sur le registry.
2. **Votre pipeline comporte plusieurs étapes. Que se passe-t-il si la construction de l’image calculator-sub échoue ?** Le pipeline s'arrête immédiatement avec un statut d'erreur. Les étapes suivantes (publication, déploiement) sont annulées. L'application en production reste sur l'ancienne version, empêchant ainsi de déployer un code cassé.
3. **Le Webhook GitHub est la méthode la plus utilisée en entreprise dans une chaîne CI. Quelles opérations devriez-vous faire pour la mettre en place dans votre architecture ?** Le Webhook fonctionne en envoyant une notification à Jenkins à chaque fois qu'un commit est poussé sur GitHub. Il faudrait que la VM Jenkins soit accessible depuis Internet pour que le serveur GitHub puisse y accéder (attribuer une IP publique à VM-Jenkins et  mettre en place des règles de sécurité entrantes depuis l'extérieur).

## Etape 3

1. **Pourquoi Jenkins doit-il disposer d’un accès à l’API Kubernetes ?**
2. **Quelles étapes du job Jenkins correspondent à la CI, et lesquelles correspondent à la CD ?** CI: Checkout (récupérer le code depuis Git) et Build (construction des images Docker). CD: Push (publication des images dans le Registry) et Deploy (déploiement sur Kubernetes).
3. **Quel est le parcours d’une modification du code source depuis le "git push" jusqu’à l’application Calculator ? Pour chaque étape, indiquez l’outil ou la technologie qui intervient.**
