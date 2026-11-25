# Fonctionnement

Comment l'extension est faite, pour la personne qui la relit ou la fait évoluer.

## Fichiers

| Fichier | Rôle |
|---|---|
| `legacy/include/exemple/Exemple.php` | la logique : le nom affiché d'un compte, forme juridique à la fin |
| `tests/ExempleTest.php` | ses tests unitaires |

La logique vit dans des classes testées sans SuiteCRM (`legacy/include/<slug>/`) ; les
déclarations faites à SuiteCRM (`legacy/Extension/…` : hooks, champs, libellés) ne font que
les appeler.

## Données en base

Les champs, tables ou réglages que l'extension crée ou modifie. Écrire « aucune » s'il n'y
en a pas.

## Installation et désinstallation

Ce que font `database/install.php` (une seule fois, à la première installation) et
`database/uninstall.php`, et ce qui reste en base après une désinstallation. Sans ces
scripts : la réparation rapide lancée par le Chargeur de module suffit.

## Points d'attention

Ce qu'un développeur doit savoir avant de modifier l'extension : comportement de SuiteCRM
contourné, interaction avec une autre extension, piège rencontré.
