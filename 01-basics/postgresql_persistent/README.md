<h1>Déploiement PostgreSQL sur Kubernetes</h1>
Ce projet contient un fichier YAML permettant de déployer un serveur PostgreSQL minimal (basé sur l’image postgres:15) dans un cluster Kubernetes.

Le déploiement crée 1 pod et expose le port 5432 pour le trafic TCP.

📂 Contenu du projet <br>
Contient la définition du déploiement Kubernetes avec :

<li>1 <i>pods</i> PostgreSQL</li>

<li>Un sélecteur de labels </li>

<li>La configuration des containers et du port exposé </li>

<li>Un <i>Service</i> permettant d'exposer le service PostgreSQL aux autres pods du cluster Kube</li>

<li>Un <i>PVC (Permanent Volume Claim)</i> permettant de rattacher notre pod à un PV (Persistant Volume), garantissant la conservation des données au redémarrage du/des pod</li>

🚀 Prérequis<br>
Avant d’utiliser ce projet, assure-toi d’avoir :

<li>Un cluster K3s fonctionnel</li>

<li>kubectl installé</li>

📦 Déploiement<br>
Clone ou copie ce projet sur ta machine.

Applique le manifeste Kubernetes avec la commande : <br>
<code> kubectl apply -f postgresql.yaml </code> <br>

Vérifie que le pod est bien créés : <br>
<code> kubectl get pods </code>

Connecte toi au pod : <br>
<code>kubectl exec -it <nom-pod-principal> -- psql -U postgres</code>

Dans le pod tu peux vérifier le bon fonctionnement du postgres en lecture <br>
<code>\l</code><br>
<code>\dt</code><br>
<code>SELECT version();</code>

Vérifier le bon fonctionnement des actions d'écritures: <br>
<code> CREATE TABLE test_cluster (id SERIAL PRIMARY KEY, data TEXT); </code><br>
<code> INSERT INTO test_cluster (data) VALUES ('test1'), ('test2'); </code><br>
<code> SELECT * FROM test_cluster; </code><br>

Puis on valide la non persistance des données :<br>
En supprimant le pod actuellement running<br>
<code> kubectl delete pod <nom-pod-principal></code><br>
Un nouveau pod est automatiquement crée pour respecter le nombre de replicas demandé<br>
On se connecte à ce nouveau pod<br>
<code>kubectl exec -it <nom-nouveau-pod-principal> -- psql -U postgres</code><br>
On accède en lecture aux données précédement insérées<br>
<code> SELECT * FROM test_cluster; </code><br>

On observe l'absence de la table test_cluster car le pod n'est pas rattaché à un volume persistant<br>

📌 Notes <br>
Un service est déployé parralèlement au pods, ce mécanisme permet d'exposer la base de données aux autres pods la consomant.<br>
Seul les pods du cluster Kube y ont accès.