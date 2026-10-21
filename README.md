# TP1 – MVC vs MVVM : filtre de Todo-list

- **Logique du filtre en MVC** : dans `TodoModel.filtrer()`. Le Controller ne fait
  que mémoriser le filtre courant et demander la liste filtrée au modèle ; la View
  affiche ce qu'on lui donne, sans aucun `.filter`.
- **Logique du filtre en MVVM** : toujours dans `TodoModel.filtrer()`, mais le filtre
  courant devient un état observable (`filtre`) du `TodoViewModel`, qui recalcule
  `visibles` et `restantes`. La page HTML ne fait que s'abonner et appeler des
  commandes.
- **Testé sans navigateur en MVC** : seulement le Model (`filtrer`, `restantes`,
  validation). Le Controller et la View dépendent du DOM, donc ne sont pas testés ici.
- **Testé sans navigateur en MVVM** : le ViewModel complet (ajout, erreur sur titre
  vide, filtre, compteur, filtre inconnu), avec 5 tests Node.
- **Fichiers modifiés pour ajouter le filtre en MVC** : `index.html`, `TodoModel.js`,
  `TodoView.js`, `TodoController.js`, soit 4 fichiers (plus `TodoModel.test.js` pour
  le test).
- **Choix pour un tableau de bord QueenBee (mesures en temps réel)** : MVVM. Les
  mesures arrivent en continu, et les valeurs observables mettent l'écran à jour
  automatiquement, sans que le Controller rappelle `render()` à chaque mise à jour.
  Le ViewModel reste testable sans écran.
  - **Bonus « Supprimer les tâches faites » en MVVM** : 3 fichiers modifiés
  (`TodoModel.js`, `TodoViewModel.js`, `index.html`), plus un test. La page ne fait
  que transmettre le clic ; `visibles` et `restantes` se mettent à jour tout seuls.
  En MVC, il aurait fallu aussi toucher la View et le Controller.