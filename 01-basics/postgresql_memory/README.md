<h1>Déploiement Nginx sur Kubernetes</h1>
Ce projet contient un fichier YAML permettant de déployer un serveur Nginx minimal (basé sur l’image nginx:alpine) dans un cluster Kubernetes.

Le déploiement crée 2 réplicas et expose le port 5432 pour le trafic TCP.

📂 Contenu du projet <br>
Contient la définition du déploiement Kubernetes avec :

<li>2 pods PostgreSQL</li>

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

📌 Notes <br>
Un service est déployé parralèlement aux pods, ce mécanisme permet d'exposer la base de données aux autres pods la consomant
Seul les pods du cluster Kube y ont accès