# ImmoSolver — Spécification fonctionnelle & technique

**CRM immobilier location & vente · Édition 2026 · v1.1**

Document de référence du produit **ImmoSolver**, établi à partir du code source déployé (84 fichiers, 10 647 lignes) et de l'application en production. Il couvre la vision produit, les 10 modules fonctionnels, le modèle de données, l'architecture, le design system, la sécurité, l'audit de maturité, la feuille de route, l'exploitation et le guide d'intégration de la vidéo de démonstration.

| | |
|---|---|
| **Application déployée** | <https://immosolver.store/> |
| **Dossier produit en ligne** | <https://immosolver.store/descriptif/> |
| **PDF de la spécification** | [`spec.pdf`](./spec.pdf) — 43 pages, A4, 4,6 Mo |
| **Source imprimable** | [`spec.html`](./spec.html) — HTML + CSS d'impression |
| **Captures** | [`assets/`](./assets) — 14 écrans de l'application |
| **Date** | 7 novembre 2026 |

> **Nouveau en v1.1 — réception WhatsApp réelle.** Le Radar se connecte au WhatsApp de l'agence par QR code ou code d'appairage à 8 chiffres. Un service Node.js / Baileys dédié gère plusieurs connexions nommées, les agents de terrain, la réception du texte, des photos et des vidéos, l'extraction du prix et des détails, puis la validation des biens en location ou en vente. Voir la section 8.6 du PDF et le mode d'emploi sur <https://immosolver.store/descriptif/#whatsapp>.

---

## Télécharger

- **PDF complet (43 pages)** : [`spec.pdf`](./spec.pdf)
- **Version imprimable / convertible** : [`spec.html`](./spec.html) — ouvrir dans un navigateur puis « Imprimer → Enregistrer en PDF ». Les captures sont dans `assets/`, à conserver à côté du fichier HTML.
- **Version en ligne** : <https://immosolver.store/descriptif/spec.pdf>

---

## Sommaire du document

### Comprendre le produit
1. **Résumé exécutif** — fiche d'identité, chiffres clés, périmètre réellement livré, hors périmètre assumé.
2. **Contexte et problème métier** — le terrain, cinq douleurs / cinq réponses, la promesse, cinq principes de conception.
3. **Utilisateurs et rôles** — quatre personas, matrice des droits théorique et réalité de l'accès.
4. **Cartographie fonctionnelle** — les 10 modules, la navigation contextuelle, le cycle de vie d'une donnée.

### Spécification fonctionnelle
5. **Analyse module par module** — objectif, fonctions implémentées, dictionnaire de données, règles, limites constatées, capture d'écran.
6. **Parcours utilisateurs** — agent commercial, gestionnaire locatif, direction, mise en route.
7. **Modèle de données** — 8 entités, dictionnaires de champs, 4 stores Zustand, persistance, 7 anomalies à corriger.

### Spécification technique
8. **Architecture technique** — couches, stack et versions, volumétrie, build, routage SPA, performance mesurée.
9. **Design system** — tokens OKLCH, surfaces en verre, typographie, 46 composants, états, responsive, accessibilité.
10. **Internationalisation et RTL** — français / arabe, 15 namespaces, bascule complète de direction.
11. **Sécurité, données et conformité** — surface d'attaque, 8 risques classés, loi 09-08 / CNDP, valeur juridique de la signature.

### Décider et exploiter
12. **Audit de maturité** — notation par module, dette technique, qualité du code.
13. **Feuille de route** — 3 phases, livrables, critères d'acceptation, choix d'architecture recommandé.
14. **Exploitation et déploiement** — environnement, procédure de publication, sauvegarde, checklist de mise en production.
15. **Guide d'intégration vidéo** — spécifications, iframe, storyboard 12 plans, script voix off.
16. **Annexes** — routes, dépendances, 14 captures, glossaire, traçabilité.

---

## Les 10 modules documentés

| # | Module | Route | Maturité |
|---|---|---|---|
| 01 | Tableau de bord | `/` | Complet |
| 02 | Portefeuille de biens | `/portefeuille` | Complet |
| 03 | Fiche bien et galerie | `/portefeuille` | Complet |
| 04 | Locataires et clients | `/locataires` | Complet |
| 05 | Paiements et impayés | `/paiements` | Complet |
| 06 | Contrats et signature | `/contrats` | Complet |
| 07 | Maintenance et charges | `/maintenance` | Complet |
| 08 | Le Radar (leads) | `/radar` | Fonctionnel |
| 09 | Analytique et performance | `/analytique` | Partiel |
| 10 | Système (navigation, i18n, thème) | transverse | Complet |

---

## Chiffres clés mesurés

- **84** fichiers source · **10 647** lignes · **10** modules · **9** routes · **46** composants d'interface
- **2** langues : français (défaut) et arabe avec direction RTL native
- Bundle : **1,33 Mo** de JavaScript (**382 Ko** gzip) · **140 Ko** de CSS
- **0** serveur, **0** API, **0** base de données à opérer
- Maturité fonctionnelle moyenne : **3,7 / 5** · **8 / 10** modules utilisables en démonstration
- **0 / 10** modules persistés côté serveur

---

## Périmètre : ce qui existe, ce qui n'existe pas

**Livré et fonctionnel**

- CRUD complet des biens, avec photos, vidéo, statut et référence `BIEN-XXXX`
- Dossiers locataires (CIN, contact d'urgence, score de fiabilité, filtres, archivage)
- Suivi des loyers, statuts d'impayé, relance WhatsApp contextualisée
- Quatre types de contrats (bail, mandat de gestion, engagement de vente, compromis) avec signature au doigt ou au stylet
- Tickets de maintenance, priorités, prestataires, coûts, rappels de charges
- Le Radar : qualification des leads, publication au portefeuille ou rejet
- Bascule complète location ↔ vente et français ↔ arabe (RTL)
- Thème sombre / clair, notifications, recherche, responsive mobile

**Hors périmètre de cette version**

- Authentification, rôles, cloisonnement des données
- Persistance serveur et travail multi-appareils
- Vitrine publique (écran « Phase 2 » uniquement)
- Comptes multi-utilisateurs et rôles par agence pour le service WhatsApp (mono-clé aujourd'hui)
- Quittances PDF, envoi de contrats par e-mail, signature qualifiée
- Coût par lead, ROI publicitaire, attribution de campagne
- Comptabilité, rapprochement bancaire, multi-agences
- Tests automatisés, intégration continue, supervision

> L'application est un **démonstrateur avancé et crédible**, prêt pour la démonstration commerciale, mais **non prêt pour une exploitation réelle** sans le socle serveur décrit au chapitre 13.

---

## Intégrer la vidéo de démonstration

La page <https://immosolver.store/descriptif/> contient un cadre 16:9 responsive avec une iframe de remplacement. Dans `descriptif/index.html`, section `#video` :

```html
<div class="video-wrap">
  <iframe
    src="about:blank"
    title="Démonstration ImmoSolver"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
  <div class="video-ph">…</div>
</div>
```

Remplacer `src="about:blank"` par l'URL d'embed (YouTube : `https://www.youtube.com/embed/VIDEO_ID`, Vimeo, Loom) puis supprimer le bloc `.video-ph`. Le storyboard 12 plans, le script voix off et la checklist de publication figurent au chapitre 15 du PDF.

---

## Régénérer le PDF

Le PDF a été produit depuis `spec.html` avec Chromium en mode headless, format A4, en-têtes et pieds de page paginés, couverture pleine page fusionnée.

```bash
npm install puppeteer-core
node gen-pdf.mjs   # voir la procédure détaillée en fin de spec.html
```

Ou plus simplement : ouvrir `spec.html` dans Chrome / Edge, `Imprimer`, format A4, marges par défaut, activer « Graphiques d'arrière-plan ».

---

## Structure du dépôt

```
.
├── README.md          # ce document
├── spec.pdf           # spécification complète, 43 pages A4
├── spec.html          # source imprimable (CSS d'impression inclus)
└── assets/            # 14 captures de l'application déployée
    ├── 01-dashboard.jpg
    ├── 02-portefeuille.jpg
    ├── 03-bien-detail.jpg
    ├── 04-locataires.jpg
    ├── 05-paiements.jpg
    ├── 06-contrats.jpg
    ├── 07-maintenance.jpg
    ├── 08-maintenance-charges.jpg
    ├── 09-radar.jpg
    ├── 10-analytique.jpg
    ├── 11-mode-vente.jpg
    ├── 12-mode-vente-portefeuille.jpg
    ├── 13-arabe-rtl.jpg
    └── 14-mobile.jpg
```

---

## Avertissement

Les données visibles dans les captures et dans l'application sont des **données de démonstration**. Les noms, biens, montants et coordonnées ne correspondent à aucune personne ni transaction réelle. La signature intégrée est une signature manuscrite numérisée : elle ne constitue pas une signature électronique qualifiée au sens de la loi 43-20 ou d'eIDAS.

---

*Document établi le 5 novembre 2026, mis à jour le 7 novembre 2026 avec l'intégration WhatsApp (v1.1), à partir du code source et de l'application déployée sur <https://immosolver.store/>.*
