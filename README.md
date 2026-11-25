# Exemple (`exemple`)

> **Ce dépôt est le modèle des extensions SuiteCRM.** Pour créer une extension, suivre
> [Créer une extension](docs/developpement.md#créer-une-extension-à-partir-de-ce-modèle),
> puis remplacer ce README et les pages de `docs/` par ceux de la nouvelle extension, en
> gardant leur plan. Supprimer ce paragraphe.

Ce que fait l'extension, en deux ou trois phrases, en mots métier : pour qui, sur quels
écrans, ce qui change pour l'utilisateur. Exemple : ajoute la forme juridique à la fin du
nom des comptes (« Dupont SARL »).

| Fiche | |
|---|---|
| Version de SuiteCRM | 8.10 (`>=8.10 <9`) |
| Types | `logic-hook` |
| Dépend de | — |
| Installée d'office | non |

## Installer

Sur une instance, par **Administration → Chargeur de module** : l'extension y figure dans
la liste des paquets disponibles, il suffit de cliquer sur **Installer**. Depuis le
terminal, dans suitecrm-core :

```bash
make extensions@install SLUGS="exemple"
```

La désinstallation se fait au même endroit.

## Documentation

| Page | Contenu |
|---|---|
| [Utilisation](docs/utilisation.md) | ce que voient l'administrateur et les utilisateurs, réglages, données de démo |
| [Fonctionnement](docs/fonctionnement.md) | fichiers, hooks, données en base, installation et désinstallation |
| [Développement](docs/developpement.md) | créer, vérifier, tester en local, publier une version |

Les commandes, la CI et le format des extensions sont décrits dans la documentation de
[suitecrm-devkit](https://github.com/david-grosskost/suitecrm-devkit#documentation).
