# 📈 Statut Kanta — [status.kanta.fr](https://status.kanta.fr): <!--live status--> **Tous les systèmes sont opérationnels**

Page de statut publique des services Kanta : **[status.kanta.fr](https://status.kanta.fr)**

Le monitoring est propulsé par [Upptime](https://github.com/upptime/upptime) (checks toutes les 5 minutes via GitHub Actions). La page publique, elle, est une **page statique custom** maintenue dans [`site-custom/`](./site-custom) — pas l'UI Upptime par défaut.

[![Uptime CI](https://github.com/Kanta-Inc/kanta-uptime/workflows/Uptime%20CI/badge.svg)](https://github.com/Kanta-Inc/kanta-uptime/actions/workflows/uptime.yml)
[![Response Time CI](https://github.com/Kanta-Inc/kanta-uptime/workflows/Response%20Time%20CI/badge.svg)](https://github.com/Kanta-Inc/kanta-uptime/actions/workflows/response-time.yml)
[![Static Site CI](https://github.com/Kanta-Inc/kanta-uptime/workflows/Static%20Site%20CI/badge.svg)](https://github.com/Kanta-Inc/kanta-uptime/actions/workflows/site.yml)
[![Summary CI](https://github.com/Kanta-Inc/kanta-uptime/workflows/Summary%20CI/badge.svg)](https://github.com/Kanta-Inc/kanta-uptime/actions/workflows/summary.yml)

## 📊 Statut en direct

> **→ [status.kanta.fr](https://status.kanta.fr)**
>
> Le statut, l'uptime sur **30 jours** et le temps de réponse de chaque service y sont mis à jour en continu (via `summary.json`). Détail et incidents par service :
> [Application](https://status.kanta.fr/history/application) · [API](https://status.kanta.fr/history/api) · [Site vitrine](https://status.kanta.fr/history/site-vitrine)

> ℹ️ Ce README **n'embarque volontairement pas** le tableau ni les graphes générés par Upptime. La génération des `api/*.json` et des PNG de courbes (`@upptime/graphs`) est cassée en amont depuis Upptime v1.41.5 (mai 2026, échec de la dépendance native `canvas`) : embarquer ces ressources produisait des badges et images en 404. La source de vérité reste `summary.json` et la page custom.

## 🛠️ Fonctionnement

| Brique             | Rôle                                                                                                       |
| ------------------ | ---------------------------------------------------------------------------------------------------------- |
| `Uptime CI`        | Teste les services toutes les 5 min ; journalise dans `history/` (commit uniquement sur changement d'état) |
| `Response Time CI` | Enregistre un point de temps de réponse dans `history/` une fois par jour                                  |
| `Graphs CI`        | Génère `api/*.json` + les PNG de courbes — ⚠️ **KO en amont depuis Upptime v1.41.5**                       |
| `Summary CI`       | Régénère `history/summary.json` toutes les 30 min (consommé par la page custom)                            |
| `Static Site CI`   | Assemble [`site-custom/`](./site-custom) + `summary.json` et publie sur GitHub Pages (`status.kanta.fr`)   |

La page publique ([`site-custom/index.html`](./site-custom/index.html)) lit **uniquement** `summary.json` en live : aucune donnée n'est codée en dur, et si la donnée est indisponible elle affiche un état d'erreur plutôt qu'un faux chiffre. L'uptime affiché est sur **30 jours**.

> ⚠️ **`Setup CI` et `Update Template CI` sont volontairement désactivés** (au niveau GitHub).
> Ils régénèrent les workflows depuis le template Upptime à chaque push et réinstallent l'UI Upptime par-dessus la page custom. En contrepartie, Upptime ne se met plus à jour automatiquement : pour récupérer une nouvelle version, il faut les réactiver, lancer la mise à jour, puis restaurer `site.yml`.

## 🌐 Services surveillés

| Service      | URL surveillée                   |
| ------------ | -------------------------------- |
| Application  | https://app.kanta.fr             |
| API          | https://app.kanta.fr/api/v1/info |
| Site vitrine | https://kanta.fr                 |

La configuration se modifie dans [`.upptimerc.yml`](./.upptimerc.yml).

## 📄 Licence

- Monitoring : [Upptime](https://github.com/upptime/upptime) — code sous [MIT](./LICENSE)
- Données du dossier `./history` : [Open Database License](https://opendatacommons.org/licenses/odbl/1-0/)
