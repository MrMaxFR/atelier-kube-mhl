# Rendu — Atelier Kubernetes

> Complétez ce fichier au fil de l'atelier, puis faites un commit et un push (voir la section « Rendu » du README).

**Nom / Prénom :**
**Groupe :**

---

## Exercice 1 — Cluster

1. Combien de nœuds affiche `kubectl get nodes` ? Quel est le rôle de chacun ?
   > 3 noeuds sont présents, est le control plane et les deux autres n'ont pas de rôle, mais sont des worker
2. Que montre `docker ps` ? Qu'est-ce qu'un « nœud » dans k3d, concrètement ?
   > Le docker ps montre que chaque membre du cluster k3s est un container, plus un proxy. Un noeud est un container docker pour simplifier le lab.

## Exercice 2 — Premier déploiement

3. Quels objets Kubernetes ont été créés par `kubectl create deployment` ? (indice : `kubectl get all`)
   > Des services, replica et les pods
4. Vous avez supprimé le pod `web-...` : que s'est-il passé, et pourquoi ?
   > Il a été recréé instantanémment, car ce qui a été créé lors du déploiement ce n'est pas le pod, mais la "méthode" de déploiement et les données, si le pod est supprimé il sera recréé selon ce qui a été défini.

## Exercice 3 — Modifier un conteneur en direct

5. Après suppression du pod, votre message « Bienvenue... » a-t-il survécu ? Pourquoi ?
   > car les données sont restés malgré que le pod ai été supprimé
6. Pourquoi le `port-forward` a-t-il cessé de fonctionner après la suppression du pod ?
   > car le forward de port a créé un tunnel, donc lorsqu'on a supprimé l'une des extrêmité du tunnel, le tunnel a été supprimé lui aussi.

## Exercice 4 — Déclaratif

7. Quelle différence entre `kubectl create` et `kubectl apply` ?
   > kubectl create permet de faire "à la main" (un peu comme docker run) et kubectl apply un peu comme docker compose, c'est à dire en déclarant les variables et la configuration qu'on souhaite pour qu'il l'applique.
8. À quoi sert le `selector` d'un Service ? Que se passe-t-il s'il ne correspond à aucun pod ?
   > le selector permet de savoir quel pod va recevoir le trafic. La liste d'endpoint est vide.

## Exercice 5 — Scaling & mises à jour

9. Sur quels nœuds se trouvent vos 3 réplicas ? Collez la sortie de `kubectl get pods -l app=site -o wide`.
   ```
NAME                   READY   STATUS    RESTARTS   AGE     IP          NODE               NOMINATED NODE   READINESS GATES
site-75775484b-9g5m4   1/1     Running   0          19s     10.42.2.6   k3d-lab-agent-0    <none>           <none>
site-75775484b-lr8sj   1/1     Running   0          19s     10.42.1.6   k3d-lab-server-0   <none>           <none>
site-75775484b-mk6sz   1/1     Running   0          2m13s   10.42.0.7   k3d-lab-agent-1    <none>           <none>
   ```
10. Avec l'image `nginx:9.99`, quel statut avait le pod ? Quelle commande vous a donné la cause ?
    > ErrImagePull, kubectl get pods
11. Pendant la panne, le site restait-il accessible ? Pourquoi ?
    > Oui, car il a testé de déployer un pod avant de remplacer les anciens.

## Exercice 6 — Portainer & Mario

12. URL publique de votre Mario :
    > https://laughing-system-5454pq7564g37q94-8585.app.github.dev/
13. Retrouvez le Deployment `mario` en ligne de commande. Portainer et `kubectl` parlent-ils au même composant ? Lequel ?
    > kubectl get deployment mario permer de retrouver le déploiement de Mario . Portainer et kubectl parlent à L'API de kubernetes

## Bonus (facultatif)

14. Bonus réalisés et remarques :
    >

---

**Score obtenu avec `./scripts/check.sh` :** 15 / 18
