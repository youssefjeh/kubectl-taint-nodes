# Kubernetes - Utilisation de `kubectl taint nodes`

Dans Kubernetes, la commande `kubectl taint nodes` permet de marquer (ou "souiller") un ou plusieurs nœuds d'un cluster. Cela empêche certains pods de s'exécuter sur ces nœuds, sauf si ces pods ont explicitement une tolérance définie.

## Explication

- **Nœud** : Une machine physique ou virtuelle dans le cluster Kubernetes qui exécute des pods.
- **Taint (souillure)** : Une règle appliquée à un nœud pour empêcher des pods de s'y exécuter, à moins qu'ils ne possèdent une tolérance correspondante.
- **Toleration (tolérance)** : Une configuration d'un pod qui lui permet d'ignorer la souillure et de s'exécuter sur un nœud souillé.

### Utilisation de base

La commande suivante ajoute une souillure (taint) à un nœud spécifique pour empêcher tout pod sans tolérance de s'y exécuter :

```bash
kubectl taint nodes my-node key=value:NoSchedule
```
 - **my-node** : Nom du nœud à souiller.

 - **key=value** : Paire clé-valeur qui identifie la souillure.

 - **NoSchedule** : Action à prendre, ici cela signifie qu'aucun pod ne sera programmé sur ce nœud, sauf s'il possède une tolérance.

## Exemple concret

Si l'on souhaite empêcher tout pod de s'exécuter sur le nœud worker-1 à moins qu'il ne possède une tolérance pour une souillure spécifique, on peut utiliser la commande suivante :

```bash
kubectl taint nodes worker-1 env=production:NoSchedule
```
Cela va "souiller" le nœud worker-1 avec la clé env=production et empêcher tout pod qui n'a pas la tolérance correspondante de s'y exécuter.

## Retirer une souillure

Pour retirer une souillure d'un nœud, utilisez la commande suivante :
```bash
kubectl taint nodes my-node key=value:NoSchedule-
```
Le signe - à la fin permet de retirer la souillure.

## Pourquoi utiliser les taints et tolérances ?

L'ajout de taints et de tolérances permet de mieux contrôler sur quels nœuds les pods s'exécutent dans un cluster Kubernetes. Voici quelques raisons d'utiliser cette fonctionnalité :

  - **Réserver des nœuds spécifiques** pour certains types de workload (par exemple, des nœuds avec plus de ressources ou des nœuds dédiés à une application critique).
  - **Empêcher des pods** d'être déployés sur des nœuds en maintenance ou ayant des contraintes particulières.
  - **Gérer les ressources** de manière plus granulaire en segmentant les nœuds par environnement ou par rôle (ex. production, test).
