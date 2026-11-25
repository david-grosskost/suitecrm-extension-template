# Développement

Les commandes `make`, la CI et le format des extensions viennent de
[suitecrm-devkit](https://github.com/david-grosskost/suitecrm-devkit#documentation), à la
version de `composer.json`. Cette page ne décrit que ce qui est propre à l'extension.

## Créer une extension à partir de ce modèle

Avec Claude, même sans connaissance technique : le plugin
[`suitecrm-extensions`](https://github.com/david-grosskost/suitecrm-devkit/blob/main/plugins/suitecrm-extensions/README.md)
guide de l'entretien sur le besoin jusqu'à la pull request. À la main :

1. Sur GitHub, **Use this template → Create a new repository**, nommé
   `suitecrm-ext-<slug>`, le slug en anglais (ex. `suitecrm-ext-french-company-validation`).
2. Poser les [réglages GitHub](https://github.com/david-grosskost/suitecrm-devkit/blob/main/docs/reglages-github.md)
   du dépôt.
3. Le cloner, puis lancer `make` : le devkit s'installe (Docker suffit, pas besoin de PHP).
4. Remplacer l'exemple :
   - `extension.json` : `slug`, nom, description en mots métier, types ;
   - `composer.json` : `name` en `…/suitecrm-ext-<slug>`, description, espace de noms ;
   - `legacy/include/exemple/`, `tests/ExempleTest.php` : son code et ses tests ;
   - `README.md` et `docs/` : sa documentation, en gardant leur plan.
5. Vérifier, puis ouvrir la pull request (voir ci-dessous).

## Vérifier

```bash
make extension@validate   # format : manifeste, composer.json, place des fichiers
make quality@lint         # style du code, scripts
make quality@stan         # analyse statique (PHPStan, niveau max)
make test@unit            # tests unitaires
make package@build        # paquet du Chargeur de module, dans build/
make package@scan         # le paquet passe le scanner de SuiteCRM
```

La CI relance les mêmes contrôles sur chaque pull request.

## Tester sur une instance locale

1. `make package@build` : le paquet est dans `build/exemple-<version>.zip`.
2. Sur l'instance locale de suitecrm-core, **Administration → Chargeur de module** :
   **Choisir un fichier**, **Télécharger**, puis **Installer**.
3. Vérifier les écrans de [Utilisation](utilisation.md), puis lancer le test de régression
   dans suitecrm-core : `make test@regression`.

Avant un essai qui touche aux données : `make db@dump` dans suitecrm-core, pour revenir en
arrière avec `make db@restore`.

## Publier une version

Pull request relue, puis merge (squash) : release-please ouvre la pull request
« chore(main): release x.y.z ». La merger crée le tag, la release GitHub et son paquet.
L'image de suitecrm-core la récupère avec
`make composer@update PACKAGES="david-grosskost/suitecrm-ext-exemple"`.

Mettre à jour `README.md` et `docs/` dans la même pull request que le changement qu'ils
décrivent.
