# Extension SuiteCRM

Ce dépôt est **une extension SuiteCRM 8** des projets de David Grosskost : un paquet Composer
(`suitecrm-extension`) que l'image de suitecrm-core (ou d'un projet client) met à
disposition, et que chaque instance installe ou non depuis le Chargeur de module.

## Avec qui tu travailles

La personne en face n'est pas forcément développeur : un commercial ou un consultant peut
créer une extension. Parle en français, en mots métier, sans jargon ; fais toi-même le
travail technique et explique ce que tu vérifies et pourquoi. Pour créer ou modifier une
extension, suis le skill **nouvelle-extension** du plugin Claude `suitecrm-extensions`. S'il
n'est pas installé, demande à la personne de l'installer (Claude Code :
`/plugin marketplace add david-grosskost/suitecrm-devkit`, puis
`/plugin install suitecrm-extensions@suitecrm-devkit`) avant d'aller plus loin.

## Règles qui ne se discutent pas

- **Ne jamais modifier SuiteCRM** : une extension ajoute, elle ne remplace pas. Pas de
  fichier hors des emplacements prévus (`make extension@validate` les refuse).
- **Refuser et renvoyer vers un développeur** : modifier le cœur de SuiteCRM ou le core,
  envoyer des données hors de SuiteCRM (API externe, e-mail automatique à des tiers),
  manipuler des secrets (mots de passe, clés d'API), toucher aux droits et à la sécurité.
- **Tout passe par une pull request relue par un humain** : jamais de push sur `main`,
  jamais de merge sans relecture.
- **Aucun secret** dans le code, les tests, les commits ou la conversation.
- Code, commentaires et messages de commit **en anglais** (Conventional Commits :
  `feat: …`, `fix: …`) ; libellés et textes visibles par l'utilisateur **en français**.

## Où mettre quoi

| Dossier | Copié dans SuiteCRM | Pour |
|---|---|---|
| `legacy/Extension/…` | `public/legacy/custom/Extension/…` | déclarations (hooks, champs, libellés), assemblées à la réparation rapide ; le slug dans chaque nom de fichier |
| `legacy/include/<slug>/` | `public/legacy/custom/include/<slug>/` | les classes PHP : toute la logique, testée sans SuiteCRM |
| `legacy/themes/<Nom>/` | `public/legacy/custom/themes/<Nom>/` | un thème propre à l'extension |
| `backend/`, `config/` | `extensions/<Nom>/` | la couche SuiteCRM 8 (Symfony) ; `<Nom>` : le slug en PascalCase |
| `app/` → `public/` | `extensions/<Nom>/public/` | le module Angular (`make front@build`, `public/` versionné) |
| `database/install.php`, `uninstall.php` | — | lancés une seule fois à l'installation, et à la désinstallation |
| `database/seeders/<slug>/` | catalogue de l'image | données de démo ; une classe de l'extension s'y charge depuis `custom/include/<slug>/`, jamais par un chemin relatif vers `legacy/` |
| `tests/` | — | tests unitaires (PHPUnit) |

Le détail est dans la documentation du devkit :
[extensions](https://github.com/david-grosskost/suitecrm-devkit/blob/main/docs/extensions.md).

## Commandes (Docker suffit, pas besoin de PHP)

```bash
make extension@validate   # format de l'extension
make quality@lint         # style du code
make quality@stan         # analyse statique (PHPStan, niveau max)
make test@unit            # tests unitaires
```

Les quatre doivent passer avant toute pull request : la CI refait les mêmes. Les commandes,
la CI et les règles viennent de suitecrm-devkit (version dans `composer.json`), que
Dependabot propose de mettre à jour.

## Documentation

`README.md` (fiche de l'extension, installation, table des pages) et `docs/`
(`utilisation.md`, `fonctionnement.md`, `developpement.md`) suivent le plan du modèle.
Toute pull request qui change le comportement de l'extension met ces pages à jour : ce
qu'elles disent doit rester vrai.
