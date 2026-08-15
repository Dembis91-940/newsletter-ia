# IA PRATIQUE — Newsletter hebdomadaire

**Positionnement :** « Chaque semaine, une technique IA que vous pouvez appliquer le jour même. Gratuit. »

**Cible :** alternants, étudiants et débutants tech qui veulent maîtriser l'IA par l'action — pas par la théorie.

**Promesse d'identité :** *« L'IA qui se retient, c'est l'IA qu'on applique. »*

---

## 1. Positionnement

Le marché de la formation IA est saturé de cours longs, de vidéos et de promesses de richesse. IA Pratique prend le contre-pied :

| Le bruit ambiant | IA Pratique |
|---|---|
| Cours de 6 heures | 5 minutes de lecture |
| Théorie d'abord | Action d'abord |
| Jargon de chercheurs | Français simple, termes définis |
| « Gagnez 10 000 €/mois » | Tarifs honnêtes, effort assumé |
| On regarde l'IA | On la fait travailler |

**Le contrat éditorial (tenu dans chaque numéro) :**
1. Une seule technique, expliquée en 5 minutes.
2. Un exemple réel, du début à la fin.
3. Un exercice applicable le jour même (15 à 30 minutes).
4. Des ressources et un glossaire express.
5. Zéro jargon non traduit, zéro promesse mensongère.

**Le squelette d'un numéro :** promesse mesurable → leçon actionnable → atelier pas à pas → exercice avec critère de réussite → ressources → teaser du prochain numéro.

---

## 2. Les 3 premiers numéros (livrés)

| N° | Titre | Compétence acquise | Durée |
|---|---|---|---|
| 01 | [Vos premiers agents IA en 30 minutes](numeros/numero-1.md) | Monter un agent de veille réel (n8n + Groq + Telegram), 0 € | 30 min |
| 02 | [Data science sans maths : commencez par l'analyse](numeros/numero-2.md) | Charger un vrai jeu de données (pandas/Colab), 3 graphiques qui répondent à 3 questions | 20 min |
| 03 | [Gagner de l'argent avec l'IA : les 5 pistes qui marchent en 2026](numeros/numero-3.md) | Choisir une piste (freelance, micro-outils, contenus, automatisations, audits) et produire son premier livrable | 20 min |

---

## 3. Plan des 10 prochains numéros

| N° | Titre | Compétence |
|---|---|---|
| 04 | Automatisez votre recherche d'alternance ou de premier emploi | Workflow candidatures : détection d'offres, préparation, relances automatiques |
| 05 | Votre premier chatbot pour un vrai site | Assistant FAQ + capture de leads, déployé en une session |
| 06 | L'IA qui lit pour vous | Résumés de PDF, d'articles et de rapports longs (documents réels) |
| 07 | SQL en 30 minutes | Interroger une vraie base de données avec des requêtes qui servent |
| 08 | Créer des images IA sans ressembler à tout le monde | Style cohérent, prompt structurel, usages honnêtes |
| 09 | Vos premiers pipelines | Enchaîner données + modèle + livrable de façon propre et reproductible |
| 10 | Un LLM sur votre ordinateur | Lancer un modèle local, gratuit, hors ligne (première exécution guidée) |
| 11 | Excel + IA : le tableur devient une machine d'analyse | Analyser un fichier réel, formules assistées, automatisation |
| 12 | Vendre ses compétences : prix, contrats, premiers clients | Devis, cadrage, livraison : la mécanique d'une mission |
| 13 | Le projet fil rouge : votre portfolio IA en une semaine | Assembler les acquis en 3 projets montrables |

**Logique de progression :** semaines 1-3 = fondations (agents, données, monétisation) → semaines 4-6 = outils du quotidien (candidatures, chatbot, lecture) → semaines 7-10 = montée en compétence (SQL, images, pipelines, local) → semaines 11-13 = business et portfolio.

---

## 4. Modèle de revenus

### Version gratuite (toujours)
- Un numéro par semaine, intégralement gratuit.
- 5 minutes de lecture + exercice.
- Jamais de contenu « gratuit » amputé : le numéro de la semaine est complet.

### Version Pro — 9 €/mois
Pour ceux qui veulent aller plus loin, sans changer le contrat de la version gratuite :
- **2 techniques supplémentaires par mois** (au-delà du numéro hebdomadaire).
- **Fichiers et templates prêts à l'emploi** : workflows n8n exportés, notebooks pandas, prompts documentés, grilles d'audit.
- **Accès aux archives complètes** (la version gratuite ne garde que les 4 derniers numéros visibles).
- **Communauté Pro** : un fil de questions-réponses et les exercices corrigés.

**Paiement :** virement ou message privé (Stripe en attente d'activation). L'inscription Pro se fera via le formulaire EmailJS du site, avec récapitulatif complet de la commande dans l'email reçu.

**Le principe de loyauté :** la version gratuite promet un numéro complet par semaine — elle le livre, quoi qu'il arrive. La version Pro finance la newsletter ; elle n'est jamais une porte de sortie du contrat gratuit.

---

## 5. Structure du projet

```
newsletter-ia/
├── index.html            # Landing EXCELLENCE ULTRA adaptée (identité éditoriale)
│                         #   hero Forge LIRE → APPLIQUER → MAÎTRISER
│                         #   formulaire EmailJS réel (nom + email + métier)
│                         #   compteur d'abonnés réel (0 — pas de fake)
│                         #   sections : arguments, numéros, pour qui, FAQ, chatbot
├── numeros/
│   ├── numero-1.md       # Agents IA en 30 minutes (complet)
│   ├── numero-2.md       # Data science sans maths (complet)
│   └── numero-3.md       # Gagner de l'argent avec l'IA (complet)
└── README.md             # Ce document
```

**EmailJS (réel, câblé dans index.html) :** service `service_cy1ytdb` · template `template_xpo58cv` · clé publique `8Pui4ZEqxW2jRVF7h` · payload `{site, name, email, question}` où `question` = « Inscription newsletter IA Pratique — métier/objectif : … ». Le SDK est chargé à la demande dans le gestionnaire de soumission (aucune course async).

**Design :** DNA EXCELLENCE ULTRA (abyss `#041019` + paper `#f8f7f3`, CTA `#064BD9`, titres géants, hero Forge interactif, film de conversion, triade, compteurs animés, révélations au scroll, fond 3D WebGL, chatbot) **adapté** à une identité éditoriale propre : logo « IA·PRATIQUE », typographie serif (Fraunces) pour les titres de numéros et citations, sections numéros, pour-qui, FAQ. Pas de copier-coller : le template n'est que la base structurelle.

---

## 6. Prochaines étapes

1. **Vérification finale** de la landing (structure, EmailJS, orthographe) avant mise en ligne.
2. **Déploiement** du site sur GitHub Pages (repo `Dembis91-940/newsletter-ia`) — à faire uniquement sur validation explicite.
3. **Premier envoi** : déclencher l'envoi du numéro 01 aux premiers inscrits (bascule manuelle vers l'outil d'envoi retenu).
4. **Boucle d'apprentissage** : mesurer à chaque numéro — ouverture, taux d'exercice complété (réponses reçues), désinscriptions — et ajuster le contenu.
5. **Version Pro** : activer les paiements (virement/DM dans un premier temps), préparer le premier pack de templates Pro (workflows n8n + notebooks des numéros 1 et 2).

**KPI de lancement (30 jours) :** 100 abonnés · 40 % d'ouverture · 1 exercice complété sur 5 · 0 plainte.

---

*IA Pratique — « L'IA qui se retient, c'est l'IA qu'on applique. »*
