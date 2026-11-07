## Etape 1

1. **Quel est le rôle d’un réseau privé dans une infrastructure Cloud ? D’un routeur externe ?** Le réseau privé a pour rôle d'isoler les instances/VM que l'on créé sur ce sous-réseau des machines des autres utilisateurs du Cloud. Le routeur externe relie le sous-réseau au réseau externe du Cloud.
2. **Pourquoi un fournisseur Cloud propose-t-il autant de catégories de ressources différentes ?** Fournir beaucoup de catégories de ressources différentes permet de n'utiliser/payer que les services nécessaires au besoin exprimé. Cela permet alors une meilleure segmentation/partage des ressources.
3. **En observant la topologie générée par OpenStack, expliquez le chemin emprunté par un paquet réseau envoyé depuis l’extérieur vers une machine virtuelle sur net-discovery.**
Le paquet arrive depuis l'extérieur sur le routeur externe d'OpenStack. Le paquet est redirigé vers le réseau privé (net-discovery) via le routage défini par routerdefault, et atteint la VM si le groupe de sécurité l'autorise.

## Etape 2

1. **Quelles sont les étapes nécessaires pour pouvoir se connecter en SSH à une nouvelle machine virtuelle OpenStack depuis la machine hôte ?** Il faut démarrer une VM avec une paire de clés SSH, conserver la clé privée sur la machine hôte et associer une IP flottante à la VM pour la rendre visible de l'extérieur. Le groupe de sécurité doit autoriser le trafic ssh. Une fois la VM active, on se connecte.
2. **Quel est le rôle de l’adresse IP privée, de l’adresse IP flottante et des Groupes de Sécurité dans cette connexion ?** L'IP privée sert à la VM pour exister et discuter dans son réseau local. L'IP flottante la rend visible et accessible depuis l'extérieur et redirige vers l'IP privée. Le Groupe de Sécurité détermine si la connexion entrante est autorisée.
3. **Pourquoi OpenStack distingue-t-il une adresse IP privée d’une IP flottante publique, plutôt que d’attribuer directement une adresse publique à chaque machine virtuelle ?**  
Une IP flottante peut être transférée sur d'autres VM ce qui permet d'utiliser la même adresse publique si notre nouvelle VM utilise une adresse privée différente. Le Cloud propose des IP flottantes publiques uniquement pour les machines qui ont réellement besoin d'être joignables depuis l'extérieur car les adresses publiques sont limitées.

## Etape 3

1. **Pourquoi les Security Groups sont-ils indispensables même lorsqu’une machine virtuelle possède une adresse IP publique ?** Comme l'IP publique expose la machine à tout Internet, le groupe de sécurité est indispensable pour limiter les connexions qui peuvent atteindre la VM. Dans notre cas, le groupe de sécurité autorise les requêtes HTTP sur le port 5000. Les autres ports seront fermés ou auront d'autres règles de sécurité si nécessaire.
3. **Décrivez le chemin parcouru par une requête HTTP envoyée depuis votre ordinateur jusqu’à l’application hello-api exécutée sur votre machine virtuelle.** L'ordinateur envoie la requête à l'IP flottante sur le port 5000. Le routerdefault intercepte la requête et la transmet vers l'IP privée de la VM. La requête passe ensuite la règle du groupe de sécurité qui autorise le port 5000 et atteint le programme hello-api.   

## Etape 4 

1. **Quelles différences existe-il entre une image officielle et un snapshot ?** Une image officielle fourni un système d'exploitation de base. Un snapshot est une sauvegarde d'une VM à un instant précis, contenant l'OS et tous les logiciels, fichiers ajoutés...
2. **Quels avantages apporte le redimensionnement d’une machine virtuelle dans un environnement Cloud ?** Le redimensionnement permet d’ajuster les ressources allouées à la VM (en fonction des besoins/elasticité). On conserve le système et ses fichiers sans refaire l’installation.
3. **Dans quels contextes un administrateur système préférera-t-il créer une nouvelle machine à partir d’un snapshot plutôt que de repartir d’une image vierge ?** Un administrateur utilisera un snapshot s'il veut déployer rapidement plusieurs serveurs identiques sans avoir à reconfigurer ou pour sauvegarder un environnement de travail fonctionnel avant de faire une mise à jour.   
