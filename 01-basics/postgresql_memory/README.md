<h1>Déploiement PostgreSQL sur Kubernetes</h1>
Ce projet contient un fichier YAML permettant de déployer un serveur PostgreSQL minimal (basé sur l’image postgres:15) dans un cluster Kubernetes.

Le déploiement crée 1 pod et expose le port 5432 pour le trafic TCP.

📂 Contenu du projet <br>
Contient la définition du déploiement Kubernetes avec :

<li>1 pods PostgreSQL</li>

<li>Un sélecteur de labels </li>

<li>La configuration des containers et du port exposé </li>

<li>Un service permettant d'exposer le service PostgreSQL aux autres pods du cluster Kube</li>

🚀 Prérequis<br>
Avant d’utiliser ce projet, assure-toi d’avoir :

<li>Un cluster K3s fonctionnel</li>

<li>kubectl installé</li>

📦 Déploiement<br>
Clone ou copie ce projet sur ta machine.

Applique le manifeste Kubernetes avec la commande : <br>
<code> kubectl apply -f postgresql.yaml </code> <br>

Vérifie que les pods sont bien créés : <br>
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

📌 Notes <br>
Un service est déployé parralèlement au pods, ce mécanisme permet d'exposer la base de données aux autres pods la consomant.
Seul les pods du cluster Kube y ont accès.