# 🪞 MindMirror

**Sors de ta bulle algorithmique** — outil pédagogique 100 % local et 100 % privé pour mesurer ta diversité d'information et détecter tes biais cognitifs.

> **Aucune donnée ne quitte ton navigateur.** Pas d'IA cloud, pas de tracking, pas de compte. Code open source, inspectable.

---

## 🔗 Live demo

👉 **[wilf974.github.io/MindMirror](https://wilf974.github.io/MindMirror/)** (mobile-first, installable PWA, fonctionne hors-ligne)

---

## Problem

À l'ère des algorithmes :
- **70 %** des contenus que tu vois en ligne sont sélectionnés par un algo (Google, YouTube, TikTok, X)
- Tu reçois ce qui te conforte, jamais ce qui te dérange
- Les bulles algorithmiques amplifient les biais cognitifs naturels (confirmation, ancrage, halo)
- Personne ne te dit ton score d'enfermement — par design

**MindMirror** te donne une **mesure objective et auditable** de ta bulle, en 3 minutes, sans rien révéler de toi à personne.

---

## Pipeline

```
                    ┌──────────────────┐
                    │  Tu colles tes   │
                    │   liens récents  │ → Audit local
                    └────────┬─────────┘
                             │
                             ▼
            ┌────────────────────────────────┐
            │  Diversité  Concentration       │
            │   ratio       top source        │
            └────────────────┬───────────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │  Score d'ouverture   │
                  │   (60% div + 40%     │
                  │    inv-concentration)│
                  └──────┬───────────────┘
                         │
                         ▼
                  ┌──────────────┐
                  │   Niveau :   │
                  │  🟢 OUVERT   │
                  │  🟡 PROTÉGÉ  │
                  │  🟠 CONCENTR.│
                  │  🔴 BULLE    │
                  └──────────────┘

  + Test de 12 questions → détecte 6 biais cognitifs majeurs
  + Onglet Formation → 8 biais + 6 manipulations + checklist info saine
```

---

## Modules

| Onglet | Fonction |
|---|---|
| **🔗 Audit** | Colle 10-30 URLs récentes (YouTube, X, TikTok, articles…). Calcul automatique : diversité, concentration, score d'ouverture, top 5 sources |
| **🧠 Test** | 12 questions gamifiées → score sur 10 par biais : confirmation, ancrage, halo, disponibilité, autorité, conformité |
| **📚 Formation** | 8 biais cognitifs expliqués + antidotes + 6 techniques de manipulation à reconnaître + checklist info saine 7 réflexes |
| **📋 Synthèse** | Plan d'action personnalisé selon résultats + audit log + export bilan (clipboard ou .txt) |
| **📖 Méthode** | Toutes les formules, sources scientifiques (Kahneman, Cialdini, Ariely, Pariser) |
| **🎯 Profils** | 4 simulations : bulle politique / divertissement / tech-bro / équilibré |

---

## Niveaux & action

Le bandeau du haut affiche **toujours l'action concrète** à suivre :

| Niveau | Score | Action |
|---|---|---|
| 🟢 **OUVERT** | 75-100 | « Ton info est diverse, continue à explorer » |
| 🟡 **PROTÉGÉ** | 50-74 | « Quelques angles morts, voici 3 sources opposées » |
| 🟠 **CONCENTRÉ** | 25-49 | « Bulle moyenne, attention au biais de confirmation » |
| 🔴 **BULLE FORTE** | 0-24 | « Tu es enfermé, plan désintox 7 jours proposé » |

---

## Architecture

```js
// Pure scoring engine — deterministic, no DOM, no side effects
engine.diversity_ratio(unique, total)           → ∈ [0, 100]
engine.top_concentration(topCount, total)       → ∈ [0, 100]
engine.bias_score(biased, total)                → ∈ [0, 10]
engine.openness_score(diversity, concentration) → ∈ [0, 100]
engine.bubble_level(score)                      → ∈ {0, 1, 2, 3}

// URL parser — normalize hosts (x.com → twitter.com, etc.)
parser.extractDomain(url) → string | null
parser.normalize(host)    → unified domain
```

Toutes les fonctions sont **pures** : pas d'accès DOM, pas d'effet de bord, **déterministes**. Toute la logique tourne dans ton navigateur.

---

## Garanties formelles

```
@invariant  diversity_ratio   ∈ [0, 100]
@invariant  top_concentration ∈ [0, 100]
@invariant  bias_score        ∈ [0, 10]
@invariant  openness_score    ∈ [0, 100]
@invariant  bubble_level      ∈ {0, 1, 2, 3}
@invariant  diversity_safe(_, ≤ 0) = 0  (jamais NaN même en entrée invalide)
```

Si un invariant est violé à l'exécution, un **toast d'erreur visible** s'affiche immédiatement (au lieu d'un crash silencieux).

**71 exemples / 16 invariants** validés par tests d'invariants formels lors du développement.

---

## Confidentialité

- ✅ **Aucune URL n'est envoyée** — tout est analysé en JS local
- ✅ **Aucun stockage** — tu fermes l'onglet, tout disparaît
- ✅ **Aucun tracking** — pas de Google Analytics, pas de cookie tiers
- ✅ **Aucune dépendance externe** au runtime (sauf polices Google, mises en cache)
- ✅ **Code source ouvert** — inspectable en 30 minutes

> Tu peux **déconnecter ton wifi** après le premier chargement, MindMirror fonctionne 100 % offline.

---

## Sources scientifiques

| Référence | Apport |
|---|---|
| **Kahneman, D.** (2011) — *Thinking, Fast and Slow* | Système 1/2, biais cognitifs majeurs |
| **Cialdini, R.** (1984) — *Influence: The Psychology of Persuasion* | 6 leviers de persuasion |
| **Ariely, D.** (2008) — *Predictably Irrational* | Décisions économiques irrationnelles |
| **Pariser, E.** (2011) — *The Filter Bubble* | Personnalisation algorithmique |
| **EU DisinfoLab** — [disinfo.eu](https://www.disinfo.eu/) | Typologies de manipulation contemporaines |
| **AFP Factuel** — [factuel.afp.com](https://factuel.afp.com/) | Fact-checking français |

> ⚠️ Les seuils de classification (25/50/75) et la pondération diversité/concentration (60/40) sont des **hypothèses pédagogiques**, pas des standards scientifiques. Voir l'onglet « Méthode » de l'app pour la transparence complète.

---

## Limites de validation

- **Pas un test psychométrique clinique.** 12 questions ne valent pas un MMPI ou un Big Five (200+ items).
- **Bias blind spot.** Reconnaître ses biais ne suffit pas à les éviter — il faut un effort actif et continu.
- **Audit URL limité.** Sans accès aux exports complets (Takeout YouTube, archive Twitter), l'analyse est sur un échantillon.
- **Pas de classification politique.** L'app ne juge pas l'orientation de tes sources, seulement leur diversité — par design, pour rester neutre.
- **Hypothèses simplificatrices.** Le score d'ouverture est une métrique composite, pas une vérité absolue.

---

## Stack

- **HTML / CSS / Vanilla JS** — un seul fichier `index.html` (~62 KB)
- **PWA** — `manifest.webmanifest`, `sw.js` (cache-first), 3 icônes SVG (palette violette)
- **Polices** — DM Sans + JetBrains Mono (Google Fonts, mises en cache)
- **Aucune dépendance JS** — pas de framework, pas de build, pas de bundler
- **Aucun backend, aucun serveur** — tout est statique

---

## Lancer en local

```bash
git clone https://github.com/wilf974/MindMirror.git
cd MindMirror
python -m http.server 8000
```

Puis ouvre `http://localhost:8000/`.

---

## Installation PWA

- **Android (Chrome)** : bouton « ⤓ Installer » dans le header. Ou menu ⋮ → « Installer ».
- **iOS (Safari)** : Partager ⎋ → « Sur l'écran d'accueil ».
- **Desktop (Chrome / Edge)** : icône d'installation dans la barre d'URL.

---

## Roadmap

- [ ] Parser d'export Google Takeout YouTube (analyse complète historique)
- [ ] Mode "comparaison entre amis" anonyme (sans serveur, via QR code)
- [ ] Plan désintox 7 jours guidé (notifications locales)
- [ ] Plus de questions (35 au lieu de 12) pour fiabilité accrue
- [ ] Internationalisation (anglais, espagnol, allemand)
- [ ] Mode "famille / éducation" pour ados

---

## License

[MIT](LICENSE) — © 2026 wilf974

---

## Crédits

Conçu en **Vanilla HTML/CSS/JS**. Inspiré du projet sœur [HeatGuard](https://github.com/wilf974/HeatGuard) (prévention coup de chaleur), [FireOps](https://github.com/wilf974/FireOps) (sapeurs-pompiers) et [MedTriage](https://github.com/wilf974/MedTriage) (scoring clinique). Tous suivent la même philosophie : déterministe, auditable, sans backend.

Si tu es enseignant, formateur, journaliste, parent ou simplement curieux, **tes retours sont précieux** via les Issues.
