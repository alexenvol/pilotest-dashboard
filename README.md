# Flightdeck — tableau de bord Pilotest

Petit tableau de bord gratuit et sans compte. Il transforme un export CSV Pilotest en historique consultable, courbe de progression par test et répartition des classes Stanine. Il s'agit d'une page statique, adaptée à un hébergement local ou à GitHub Pages.

## Démarrer

Pour un usage local, ouvrez PowerShell dans ce dossier et lancez :

   ```powershell
   python -m http.server 8000 --bind 127.0.0.1
   ```

Puis ouvrez [http://localhost:8000](http://localhost:8000) dans Chrome ou Edge. Choisissez **Importer un export** pour sélectionner un CSV, ou **Suivre mon CSV** pour importer et suivre un fichier.

Les imports fusionnent les lignes et écartent les doublons.

## Publier sur GitHub Pages

1. Avec GitHub Free, créez un dépôt GitHub **public** (GitHub Pages gratuit est disponible sur les dépôts publics). Le site publié sera lui aussi visible publiquement.
2. Ajoutez `index.html`, `.nojekyll`, `.gitignore` et ce `README.md` au dépôt. **N’ajoutez jamais votre CSV personnel.**
3. Dans GitHub, ouvrez **Settings → Pages**, sélectionnez **Deploy from a branch**, puis `main` et `/ (root)`.
4. Une fois le déploiement terminé, ouvrez l’adresse Pages indiquée par GitHub et importez votre CSV dans votre navigateur.

GitHub Pages héberge uniquement l’application. L’historique reste dans le stockage local de ce navigateur et cet appareil ; il ne se synchronise pas entre appareils. Utilisez HTTPS fourni par GitHub Pages pour activer la sélection de fichier suivie dans Chrome ou Edge.

## Suivi automatique

Avec **Suivre mon CSV**, le navigateur relit le fichier choisi toutes les 60 secondes pendant que la page reste ouverte. Après chaque nouvel export téléchargé depuis Pilotest, enregistrez-le au même emplacement et avec le même nom pour que le navigateur voie les nouvelles lignes. La permission de lecture reste dans le navigateur et peut être redemandée après fermeture ou redémarrage. Le suivi ne tourne pas en arrière-plan si l’onglet est fermé ou suspendu. Sur un site hébergé, le navigateur ne transmet pas le CSV au serveur ; il lit le fichier localement après votre sélection.

Chrome et Edge prennent en charge la sélection persistante de fichier nécessaire au suivi. Firefox et Safari peuvent importer les CSV manuellement mais ne proposent pas cette fonction de suivi de fichier dans ce tableau de bord.

## Limite de connexion directe

Pilotest propose l’export CSV dans « Tous mes résultats », avec les champs `test`, `score`, `stanine`, `at`. La FAQ décrit également les classes Stanine de 1 à 9 et leur variation possible lors du recalibrage des tests.

Les conditions d’utilisation françaises en vigueur indiquent explicitement que l’accès automatisé (robot, aspirateur de site, copie ou mise en miroir) est interdit. Ce projet ne se connecte donc pas au compte Pilotest, n’utilise pas d’API non documentée, ne stocke aucun cookie de connexion et ne fait aucune requête vers Pilotest. Il ne peut pas télécharger le CSV lui-même : il suit uniquement un fichier que vous avez choisi localement.

## Données et sauvegarde

L’historique est conservé dans IndexedDB sur cet appareil et dans ce navigateur. Il n’est pas envoyé au serveur GitHub Pages. Effacer les données du navigateur supprimera aussi l’historique. Pour préserver vos données, gardez une copie des CSV source.

Pour arrêter le serveur local, revenez dans PowerShell et faites `Ctrl+C`.
