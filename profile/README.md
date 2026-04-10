# ACTEE

**ACTEE** (Action des Collectivités Territoriales pour l'Efficacité Energétique) est un programme porté par la **FNCCR** (Fédération Nationale des Collectivités Concédantes et Régies) visant à accompagner les collectivités territoriales françaises dans leur transition énergétique et la rénovation de leur patrimoine bâti.

---

## Projets

### IPPER — Inventaire Public du Patrimoine, de l'Energie et de la Rénovation

Plateforme de gestion et de suivi de l'inventaire du patrimoine bâti des collectivités, avec des fonctionnalités de cartographie, d'analyse énergétique et d'intégration de données externes (DPE, Enedis SGE, RNB).

| Dépôt | Description | Stack |
|-------|-------------|-------|
| [`ipper-back`](https://github.com/FNCCR-ACTEE/ipper-back) | API REST métier | Python 3.14 · FastAPI · PostgreSQL/PostGIS · SQLAlchemy · Alembic |
| [`ipper-front`](https://github.com/FNCCR-ACTEE/ipper-front) | Interface utilisateur | Angular 20 · TypeScript · LESS · MapLibre GL · Keycloak |
| [`ipper-data`](https://github.com/FNCCR-ACTEE/ipper-data) | Pipeline ETL de données | Python · PySpark 3.5 · Delta Lake · Apache Sedona · AWS S3 |
| [`ipper-enedis`](https://github.com/FNCCR-ACTEE/ipper-enedis) | Suite de tests B2B Enedis SGE | Python · Zeep (SOAP) · mTLS · WSDL/XSD |
| [`ipper-api-referentiels-data`](https://github.com/FNCCR-ACTEE/ipper-api-referentiels-data) | API REST référentiels géographiques (RNB, BAN, Parcelles) | PostgREST · PostgreSQL 15 · PostGIS |
| [`ipper-inventaire`](https://github.com/FNCCR-ACTEE/ipper-inventaire) | *(Legacy)* Ancien système d'inventaire IPPER | Python 3.13 · Poetry · PostgreSQL · PostGIS |
| [`ipper-scripts`](https://github.com/FNCCR-ACTEE/ipper-scripts) | Scripts d'import et de migration de données | Python · psycopg2 · asyncio |

**Fonctionnalités principales :**
- Inventaire des bâtiments publics avec géolocalisation (PostGIS)
- Visualisation cartographique interactive (MapLibre GL)
- Pipeline de données Medallion (Raw → Bronze → Silver → Gold)
- Intégration B2B avec le système Enedis SGE via webservices SOAP
- Authentification SSO via Keycloak

---

### Lauréat V1 *(legacy)*

Première version de la plateforme de gestion des projets de rénovation énergétique. Développée sur une architecture monolithique ASP.NET Core.

| Dépôt | Description | Stack |
|-------|-------------|-------|
| [`laureat-v1`](https://github.com/FNCCR-ACTEE/laureat-v1) | Application full-stack | ASP.NET Core (C#) · ABP Boilerplate · Angular 15 · SQL Server/PostgreSQL |
| [`laureat-v1-monitoring`](https://github.com/FNCCR-ACTEE/laureat-v1-monitoring) | Stack de monitoring (Prometheus, Mimir, Grafana Alloy) | Prometheus · Mimir · Grafana Alloy · OVH S3 · Terraform |
| [`laureat-v1-terraform`](https://github.com/FNCCR-ACTEE/laureat-v1-terraform) | Infrastructure OVH Cloud | Terraform · OpenStack · OVH Public Cloud |

**Fonctionnalités principales :**
- Gestion des dossiers de rénovation énergétique
- Suivi des collectivités candidates
- Interface d'administration avec Material Design / AdminLTE
- Monitoring long-terme des métriques (rétention 365j via Mimir + OVH S3)
- Infrastructure as Code sur OVH Public Cloud (Terraform)

> Ce projet est en maintenance. Il est progressivement remplacé par Lauréat V2.

---

### Lauréat V2

Nouvelle génération de la plateforme Lauréat, repensée avec une architecture moderne, un monorepo TypeScript + Python, et un design system partagé.

| Dépôt | Description | Stack |
|-------|-------------|-------|
| [`laureat-v2`](https://github.com/FNCCR-ACTEE/laureat-v2) | Monorepo API + Frontend | FastAPI · Angular 20 · PostgreSQL · SQLModel · Alembic |
| [`laureat-v2-admin`](https://github.com/FNCCR-ACTEE/laureat-v2-admin) | Panneau d'administration | Angular 21 · Tailwind CSS 4 · NgRx Signal Store · Vitest · Playwright |
| [`laureat-v2-gitbook`](https://github.com/FNCCR-ACTEE/laureat-v2-gitbook) | Documentation utilisateur | GitBook |
| [`laureat-v2-playground`](https://github.com/FNCCR-ACTEE/laureat-v2-playground) | *(Archivé)* Interface de test API | Vanilla JS/HTML — archivé, remplacé par l'admin panel |

**Fonctionnalités principales :**
- Gestion des programmes de financement et des dossiers de rénovation
- Modèles d'actions et d'indicateurs configurables (règles JSONLogic)
- Interface d'administration pour la configuration métier
- Pagination curseur (HATEOAS), authentification JWT, RBAC
- Tests unitaires parallélisés (pytest-xdist) et E2E (Playwright)

---

### Design System

| Dépôt | Description | Stack |
|-------|-------------|-------|
| [`design-system`](https://github.com/FNCCR-ACTEE/design-system) | Bibliothèque de composants UI `@actee/design-system` | Angular 20 · Storybook 9 · Tailwind CSS · ng-packagr |

Bibliothèque de composants Angular partagée entre IPPER et Lauréat V2. Publiée sur le registre npm GitLab interne (`git.ipper.fr`). Comprend plus de 50 composants atomiques et composés (atoms → molecules → organisms), un système d'icônes SVG et les tokens de design issus de Figma.

---

### Infrastructure

Dépôts transverses gérant le déploiement, le monitoring et les environnements cloud de l'ensemble des projets ACTEE.

| Dépôt | Description | Stack |
|-------|-------------|-------|
| [`infra-vps-fnccr`](https://github.com/FNCCR-ACTEE/infra-vps-fnccr) | Infrastructure VPS FNCCR (Traefik, GitLab, GitLab Runner, VPN) | Docker Compose · Traefik · GitLab · WireGuard |
| [`infra-datas`](https://github.com/FNCCR-ACTEE/infra-datas) | Infrastructure plateforme data (Jupyter, Argo Workflows) | Kubernetes · Helm · JupyterLab · Argo Workflows · OVH Managed K8s |
| [`archive-ipper-infra-vps`](https://github.com/FNCCR-ACTEE/archive-ipper-infra-vps) | *(Archivé)* Ancienne infrastructure VPS IPPER | Docker Compose |

---

## Architecture technique

### Backend
- **Framework :** FastAPI (Python 3.14+) avec architecture en couches (Routes → Services → Modèles)
- **Base de données :** PostgreSQL — PostGIS pour les données géospatiales
- **ORM :** SQLAlchemy 2.0 (IPPER) · SQLModel (Lauréat V2)
- **Migrations :** Alembic
- **Validation :** Pydantic v2
- **Authentification :** JWT · Keycloak (IPPER)

### Frontend
- **Framework :** Angular 20/21 avec composants standalone
- **State management :** Angular Signals (sans NgRx côté Lauréat V2) · NgRx Signal Store (admin)
- **Style :** LESS · Tailwind CSS 4
- **Tests :** Vitest (unitaires) · Playwright BDD (E2E)
- **Change detection :** OnPush systématique

### Data
- **Traitement :** PySpark 3.5 + Delta Lake (architecture Medallion)
- **Géospatial :** Apache Sedona
- **Orchestration :** Kubernetes Spark Operator

### Infrastructure
- **Conteneurisation :** Docker + Docker Compose
- **CI/CD :** GitHub Actions
- **Déploiement frontend :** Vercel
- **APM :** OpenTelemetry + Grafana
- **Gestion des secrets :** SOPS

---

## Vue d'ensemble

```
FNCCR-ACTEE
├── IPPER
│   ├── ipper-back                   # API FastAPI + PostGIS
│   ├── ipper-front                  # Angular 20 + MapLibre
│   ├── ipper-data                   # ETL PySpark (Medallion)
│   ├── ipper-enedis                 # Tests SOAP B2B Enedis
│   ├── ipper-api-referentiels-data  # API référentiels géo (PostgREST)
│   ├── ipper-scripts                # Scripts import/migration
│   └── ipper-inventaire             # [Legacy] Ancien inventaire
│
├── Lauréat V1 (legacy)
│   ├── laureat-v1                   # ASP.NET Core + Angular 15
│   ├── laureat-v1-monitoring        # Prometheus + Mimir + Grafana Alloy
│   └── laureat-v1-terraform         # Terraform OVH Public Cloud
│
├── Lauréat V2
│   ├── laureat-v2                   # Monorepo FastAPI + Angular 20
│   ├── laureat-v2-admin             # Angular 21 admin panel
│   ├── laureat-v2-gitbook           # Documentation utilisateur
│   └── laureat-v2-playground        # [Archivé]
│
├── Transverse
│   └── design-system                # @actee/design-system (Storybook)
│
└── Infrastructure
    ├── infra-vps-fnccr              # VPS FNCCR (Traefik, GitLab, VPN)
    ├── infra-datas                  # K8s plateforme data (Jupyter, Argo)
    └── archive-ipper-infra-vps      # [Archivé] Ancienne infra VPS IPPER
```

---

*Programme ACTEE — FNCCR · Transition énergétique des collectivités territoriales*
