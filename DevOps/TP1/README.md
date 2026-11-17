## Etape 1

1. **Quel est le rôle de VM-K8s dans l’architecture mise en place ? Quelle est la différence entre cette machine et les nœuds workers ?** VM-K8s est le noeud master (Control Plane) qui décide, coordonne et surveille l'état du cluster. Les noeuds workers sont les exécutants qui font concrètement tourner l'application conteneurisée.
2. **Pourquoi le Docker Registry et le master Kubernetes sont-ils installés sur deux VMs différentes ?** Le registry et le master sont sur deux VM différentes pour répartir la charge et isoler les rôles.
3. **Le script d’installation vous a permis d’installer Kubernetes sans exécuter manuellement toutes les commandes nécessaires. Citez les opérations importantes réalisées par le script master et expliquez très brièvement en quoi elles sont nécessaires au fonctionnement du cluster.** Le script configure le réseau pour permettre aux pods de communiquer, installe containered et le configure puis installe Kubernetes et les outils kubelet, kubeadm et kubectl. Le script initialise le cluster avec kubeadm (initialisation du Control Plane) et configure kubectl avec les accès administrateur. Enfin, le script génère le token et affiche la commande a exécuter sur les workers pour rejoindre le cluster.


## Etape 2

1. **Quel est le rôle d’un Deployment dans Kubernetes ? Pourquoi ne déploie-t-on pas directement un Pod ?** Le Deployment gère le cycle de vie de l'application (nombre de réplicas, mises à jour...). On ne déploie pas un directement Pod car s'il plante, Kubernetes ne le recréera pas automatiquement.
2. **Quelle est la différence entre une image Docker, un Pod et un Deployment ? Comment les 3 sont-ils liés ?** L'image Docker est le code empaqueté. Un Pod contient un ou plusieurs conteneurs en cours d'exécution qui utilisent des images. Le Deployment est la règle qui ordonne de créer et spécifie comment maintenir les Pods.
3. **Expliquez le principe de réconciliation. Quelle composante Kubernetes est responsable de ce comportement ?** Kubernetes compare en permanence l'état désiré (le YAML) avec l'état réel (le cluster). S'il y a un écart entre les deux, il le corrige comme par exemple recréer un pod qui a planté. C'est le Controller Manager (sur le Master) qui est responsable de la boucle de réconciliation.   

## Etape 3

1. **Pourquoi ne peut-on pas simplement utiliser l’adresse IP du Pod calc-service pour permettre à un utilisateur d’accéder à l’application ?** Les adresses IP des Pods sont éphémères. Si le Pod est détruit et recréé son IP change, ce qui ne permettrait plus à l'utilisateur d'y accéder avec l'ancien IP du pod.
2. **Comment Kubernetes sait-il que le Service calc-service doit transmettre les requêtes au Pod de calc-service ?** Dans le Deployement, on attribue aux pods un label spécifique. Le Service utilise ce label dans le champ selector pour cibler les bons pods et leur acheminer les requêtes.
3. **Quelle est la différence entre le port exposé, le port cible et le NodePort utilisés dans votre architecture ?** Le NodePort est le port de la machine elle-même, accessible depuis l'extérieur du cluster. C'est celui qui est utilisé pour accéder au service proposé. Le port exposé est le port interne du Service Kubernetes, il permetauw microservices de communiquer entre eux à l'intérieur du cluster. Enfin, le port cible est le port sur lequel l'application écoute réellement au sein du Pod

## Etape 4

1. **Pourquoi les quatre microservices utilisent-ils un port de type ClusterIP, tandis que calc-service utilise un port de type NodePort ?** Le NodePort expose le frontend à l'extérieur pour les utilisateurs. Les ports de type ClusterIP gardent les backends privés et sécurisés, ils ne sont accessibles que de l'intérieur du cluster.
2. **Comment Kubernetes permet-il au frontend de contacter le backend sans connaître l’adresse IP du Pod ?** Le frontend utilise le serveur DNS interne de Kubernetes. Il suffit d'appeler le nom du service, et le DNS le traduit automatiquement en la bonne adresse IP.
3. **On propose de configurer le frontend avec l’adresse IP actuelle des Pods backend (sum, sub...), par exemple "http ://10.x.x.x :<PORT>". Pourquoi cette solution n’est-elle pas adaptée à Kubernetes ?** Cette solution n'est pas adaptée dans Kubernetes, les Pods meurent et sont relancés constamment avec de nouvelles IPs. Coder l'IP en dur casserait l'application dès qu'un pod est recréé.   
