# Relevé MT — Grands comptes (version 1.0.0)

Application de relevé mensuel des compteurs Moyenne Tension, construite sur le fichier
`RELEVE MT.xlsx` du Bureau : 22 cadrans (EAIHL … PAIHC), index précédent / index actuel /
différence, historique par compteur et export Excel au format exact du fichier de référence.
Elle fonctionne hors ligne ; les données restent sur le téléphone (rien n'est envoyé sur Internet).

## 1. Les 7 fichiers à mettre sur GitHub (tous ensemble, sans sous-dossier)

| Fichier | Rôle |
|---|---|
| `index.html` | L'application complète (code, écrans, copie intégrée de RELEVE MT.xlsx) |
| `manifest.json` | Carte d'identité de l'appli : nom, icônes, plein écran — **obligatoire pour « Installer »** |
| `service-worker.js` | Fonctionnement hors ligne et mises à jour automatiques |
| `icon-192.png`, `icon-512.png` | Icônes — **obligatoires pour « Installer »** (Chrome refuse sans elles) |
| `icon-maskable-512.png` | Icône adaptée aux formes d'icônes Android |
| `apple-touch-icon.png` | Icône pour iPhone / iPad |

Ce fichier `LISEZ-MOI.md` peut être envoyé aussi : il ne gêne pas.

> Cause n° 1 du message « Impossible d'installer l'application » : seul `index.html` a été
> envoyé, ou les icônes sont restées dans un sous-dossier. Les 7 fichiers doivent être à la
> racine du dépôt, à côté de `index.html`.

## 2. Mise en ligne sur GitHub Pages (première fois)

1. Sur github.com : **New repository** → nom `releve-mt` → **Public** → **Create repository**.
   (Un dépôt dédié : ne pas mélanger avec une autre application.)
2. **Add file → Upload files**. Ouvrez le dossier `RELEVE MT` du Bureau, sélectionnez
   **tous les fichiers** (Ctrl + A) et faites-les glisser dans la page — pas le dossier
   lui-même. Puis **Commit changes**.
3. **Settings → Pages** : Source = **Deploy from a branch**, Branch = **main** / **(root)** →
   **Save**. Vérifiez que **Enforce HTTPS** est coché.
4. Après 1 à 2 minutes, l'adresse est : `https://VOTRE-NOM.github.io/releve-mt/`

Le dépôt public ne contient que le code et le modèle vierge : les relevés et les fiches
clients ne quittent jamais les téléphones.

## 3. Installation sur le téléphone

**Android (Chrome)** : ouvrez l'adresse dans Chrome (pas dans WhatsApp / Facebook : utilisez
« Ouvrir dans Chrome »), attendez quelques secondes puis menu **⋮ → Installer l'application**
(ou le bouton « Installer » en haut de l'appli).

**iPhone (Safari)** : bouton **Partager → Sur l'écran d'accueil → Ajouter**.

### Si « Impossible d'installer l'application » s'affiche

1. Dans l'appli : **⋮ → Installer l'application** : la vérification automatique indique en
   rouge le fichier manquant ou mal placé sur GitHub.
2. **Xiaomi / Redmi / POCO** : Paramètres → Applications → Gérer les applications → Chrome →
   Autorisations (« Autres autorisations ») → activer **« Raccourcis sur l'écran d'accueil »**
   et « Afficher les fenêtres pop-up en arrière-plan », puis réessayer.
3. Désinstaller l'ancienne version si elle existe (appui long sur l'icône → Désinstaller).
   Ne pas effacer les données du site dans Chrome : les relevés y sont.
4. Mettre à jour **Chrome** et **Services Google Play**, redémarrer le téléphone.
5. Solution qui marche partout : menu ⋮ → **Ajouter à l'écran d'accueil → Créer un raccourci**.
   L'icône ouvre la même application, hors ligne compris, avec les mêmes données.
6. Huawei / Honor sans services Google : solution 5, ou Microsoft Edge.

## 4. Utilisation

1. **Tournée du mois** : l'écran d'accueil affiche le mois de consommation (au 1er octobre :
   « Septembre 2026 ») et l'avancement (compteurs relevés / à relever / brouillons).
2. **Compteurs** : bouton « + Compteur » (N° contrat et N° série obligatoires, raison sociale,
   réf. SRM, adresse, contact, téléphone / WhatsApp / e-mail, position GPS, notes), ou
   import d'une liste Excel / CSV (⋮ → Importer un fichier).
3. **Recherche** par N° de contrat, N° de série ou nom du client, puis « Saisir le relevé ».
4. **Saisie** : les 22 cadrans en grille (ordre du fichier Excel) ou en **saisie guidée**, un
   cadran à la fois dans l'ordre de l'afficheur (N° 1 → 22). L'index précédent est repris
   automatiquement du relevé du mois d'avant (0 s'il n'existe pas, modifiable) ; la différence
   est calculée à chaque chiffre tapé. La saisie est gardée en brouillon automatiquement.
5. **Enregistrer** : icône 💾 en haut à droite (ou bouton « Enregistrer » en bas). Un contrôle
   signale les cadrans vides, un index actuel inférieur au précédent, un total TT différent de
   HL + HP + HC ou une consommation inhabituelle — sans jamais bloquer.
6. **Export** : « Exporter Excel » sur l'accueil → un seul fichier `RELEVE MT - <mois>.xlsx`
   avec **une feuille par contrat relevé**, identique au modèle (option : feuille
   « Récapitulatif »). Téléchargement ou partage (WhatsApp, e-mail…) selon le téléphone.

Le mois suivant, l'index actuel enregistré devient automatiquement l'index précédent.

### Cellules remplies dans chaque feuille (le reste du modèle est conservé tel quel)

| Cellule | Contenu |
|---|---|
| E3 | Raison sociale |
| E4 | N° Contrat |
| E5 | Adresse |
| E6 | `MOIS:` + mois de consommation (+ date du relevé) |
| B6 | Réf SRM |
| D7 | N° Série |
| G / H / I (lignes 10 à 32) | Index précédent / Index actuel / Différence (formule `=H−G`) |

Si le fichier `RELEVE MT.xlsx` change, il peut être chargé dans l'appli :
⋮ → Données & paramètres → Modèle Excel → « Utiliser un autre modèle… ».

## 5. Données et sauvegarde

Chaque téléphone garde ses propres données. Pour les copier ou changer de téléphone :
⋮ → Données & paramètres → **Sauvegarder** (fichier .json), puis **Restaurer** sur l'autre
appareil. Un export Excel peut aussi être réimporté : ses relevés rejoignent l'historique.

## 6. Mises à jour

Remplacer `index.html` dans le dépôt suffit : l'appli installée prend la nouvelle version à
l'ouverture suivante avec Internet. Si des fichiers sont ajoutés ou renommés, augmenter
aussi `VERSION` en haut de `service-worker.js`.
