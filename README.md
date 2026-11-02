![CI](https://github.com/PierreCESSOT/tasks-api/actions/workflows/ci.yml/badge.svg)

# tasks-api : fil rouge du cours GitOps & CI/CD

Petite API Flask de gestion de tÃ¢ches. On ne travaille pas sur l'application elle-mÃªme :
c'est un **prÃ©texte** pour apprendre Ã  automatiser les tests, la construction et le dÃ©ploiement.

## DÃ©marrage

### 1. CrÃ©er votre dÃ©pÃ´t

Sur la page GitHub de ce dÃ©pÃ´t, cliquez sur **Use this template**, puis **Create a new repository**.
Nommez-le `tasks-api` et laissez-le **Public** (GitHub Actions est gratuit sur les dÃ©pÃ´ts publics).

> PrÃ©fÃ©rez le modÃ¨le (*template*) au *fork* : avec un fork, GitHub dÃ©sactive les workflows
> jusqu'Ã  ce que vous cliquiez sur Â« I understand my workflows, go ahead and enable them Â» dans l'onglet Actions.

### 2. Cloner votre dÃ©pÃ´t

```bash
gh repo clone <votre-compte>/tasks-api
cd tasks-api
```

### 3. CrÃ©er l'environnement Python et installer les dÃ©pendances

| | macOS | Linux | Windows (PowerShell) |
|---|---|---|---|
| CrÃ©er | `python3.12 -m venv .venv` | `python3 -m venv .venv` | `py -3.12 -m venv .venv` |
| Activer | `source .venv/bin/activate` | `source .venv/bin/activate` | `.venv\Scripts\Activate.ps1` |

Une fois l'environnement activÃ© (votre terminal affiche `(.venv)`), c'est identique partout :

```bash
pip install -r requirements-dev.txt
```

### 4. Lancer les tests

```bash
pytest
```

Vous devez voir `10 passed`.

### 5. Lancer l'application

```bash
python -m app.main
```

Dans un **second terminal** :

| macOS / Linux | Windows (PowerShell) |
|---|---|
| `curl http://localhost:8000/health` | `curl.exe http://localhost:8000/health` |

Vous devez lire `{"status":"ok"}`. ArrÃªtez l'application avec `Ctrl + C`.

> Sous Windows PowerShell, Ã©crivez bien `curl.exe` : `curl` seul est un alias d'une autre commande.

## Structure

| Chemin | RÃ´le | Quand on y touche |
|---|---|---|
| `app/` | Le code de l'API | Jamais (sauf pour casser un test volontairement) |
| `tests/` | Les tests pytest | J1, J2 |
| `.github/workflows/` | Vos workflows GitHub Actions | **J1 Ã  J3** |
| `Dockerfile` | Ã€ complÃ©ter | J3 |
| `pipelines-a-reparer/` | Trois pipelines cassÃ©s Ã  rÃ©parer | Fin du J2 |
| `config-repo/` | ModÃ¨le du dÃ©pÃ´t de configuration Kubernetes | J4 |
| `argocd/` | DÃ©claration de l'application pour Argo CD | J4 |
| `scripts/` | Script utilisÃ© par le pipeline au J4 | Ne pas toucher |
| `docs/` | Ã‰noncÃ©s des TP (TP1 Ã  TP4) et modÃ¨le de dossier | Tous les jours |

## Endpoints

- `GET /` : message de bienvenue
- `GET /health` : Ã©tat de santÃ© (`{"status": "ok"}`)
- `GET /version` : version dÃ©ployÃ©e (variable d'environnement `APP_VERSION`)
- `GET /tasks` et `POST /tasks` : liste et crÃ©ation de tÃ¢ches

## Commandes utiles

```bash
pytest --cov=app --cov-fail-under=80   # tests + couverture
flake8 .                                # qualitÃ© du code (linter)
black --check .                         # formatage du code
```

## Ã‰valuation

Votre note finale = **10/20 pour le dossier de TP** (complet et correct, dÃ©pÃ´t GitHub public + tableur du formateur) + **10/20 pour le QCM**.
Le modÃ¨le du dossier est dans `docs/DOSSIER.md` : gardez vos captures d'Ã©cran **au fil des TP**.

