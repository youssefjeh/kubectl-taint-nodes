## Imagine ceci :
  - **Les nœuds** dans Kubernetes sont comme des salles dans un bâtiment.
  - **Les pods** sont comme des personnes qui cherchent une salle pour s'installer.
  - **Taint (souillure)** est comme un panneau sur la porte de la salle qui dit : "Seules certaines personnes peuvent entrer ici".
  - **Toleration (tolérance)** est comme une carte spéciale que certaines personnes ont, leur permettant d'entrer malgré le panneau.

## Maintenant, prenons notre exemple :
```bash
kubectl taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule
```
1- `kubectl taint nodes controlplane :`
  - Ici, tu mets un panneau sur la salle appelée **controlplane**.
  - Ce nœud (`controlplane`) est une salle spéciale qui gère tout le bâtiment Kubernetes, donc tu ne veux pas que n'importe qui entre ici (pour éviter qu'il ne soit surchargé).
    
2- `node-role.kubernetes.io/control-plane :`

  - Ce panneau dit : "Cette salle est réservée pour ceux qui font partie du **groupe 'control-plane'"**.

3- `NoSchedule :`

  - La règle ici est que **personne de l'extérieur ne peut entrer dans cette salle**, à moins d’avoir une carte spéciale (une tolérance).

## Résultat :
Avec cette commande, tu as mis un panneau sur la porte du nœud `controlplane` qui dit **"Seules les personnes avec la carte spéciale 'control-plane' peuvent entrer, et tout le reste doit rester dehors"**.

Donc, après avoir utilisé cette commande :

  - **Les pods normaux** (les personnes sans carte spéciale) ne pourront pas entrer dans ce nœud.
  - **Les pods avec une tolérance spéciale** (ceux qui ont la carte "control-plane") peuvent entrer.
    
## Pourquoi faire cela ?
Tu ne veux pas que des applications normales (les pods) s'exécutent sur les nœuds du control-plane (qui gère ton cluster Kubernetes), car cela pourrait les ralentir ou les surcharger. Ces nœuds sont trop importants pour être utilisés par n'importe quelle application.

**En résumé :** Cette commande sert à réserver certains nœuds pour des tâches importantes et empêcher d'autres applications de s'y installer.
