# IA PRATIQUE — NUMÉRO 01

**Titre :** Vos premiers agents IA en 30 minutes
**Durée :** 30 minutes · **Niveau :** débutant · **Coût :** 0 €
**Promesse :** à la fin de cette session, vous aurez construit un agent IA qui travaille pour vous — pas une démo, un vrai agent qui tourne.

---

> **Le principe du numéro :** une leçon, un exemple réel, un exercice. On ne regarde pas l'IA, on la fait travailler.

## Ce que vous saurez faire dans 30 minutes

- Expliquer ce qu'est un agent IA en une phrase, sans jargon
- Choisir le bon outil gratuit selon le besoin
- Monter un agent de veille qui vous envoie un résumé automatique chaque lundi
- Comprendre la différence entre un chatbot et un agent

---

## 1. Qu'est-ce qu'un agent IA ? (la leçon en 5 minutes)

Un **chatbot** attend votre question et y répond. Un **agent** reçoit une mission, la décompose en étapes, utilise des outils, et rend un résultat — souvent sans qu'on lui repose une question.

Pensez à un **stagiaire consciencieux** :

- Vous lui donnez une mission : « Chaque lundi matin, lis les 5 dernières actualités IA et envoie-moi un résumé de 3 lignes. »
- Il va chercher l'information (**outil : la lecture**), la résume (**outil : l'écriture**), puis vous l'envoie (**outil : l'email**).
- Il le refait tout seul, chaque lundi. Vous n'avez rien à relancer.

Un agent IA, c'est exactement ça : **un modèle de langage + des outils + un déclencheur + une mission**.

| Élément | Rôle | Dans notre exemple |
|---|---|---|
| Déclencheur | Quand l'agent se met au travail | Chaque lundi à 9 h |
| Outils | Ce que l'agent peut utiliser | Lire un flux, résumer, envoyer un email |
| Modèle | Le « cerveau » qui raisonne | Un LLM gratuit |
| Mission | L'instruction permanente | « Résume et envoie » |

**À retenir :** un agent n'est pas magique. C'est une recette : *déclencheur → outils → modèle → mission*. Vous allez maintenant la cuisiner vous-même.

---

## 2. Les 3 outils gratuits pour débuter

| Outil | Ce que c'est | Version gratuite | Quand l'utiliser |
|---|---|---|---|
| **n8n** (n8n.io) | Plateforme d'automatisation visuelle : on branche des « nodes » (blocs) entre eux | Cloud gratuit : ≈ 2 000 exécutions/mois, applications illimitées | Automatiser une routine (veille, emails, notifications) |
| **Dify** (dify.ai) | Studio pour créer des agents avec mémoire et connaissances, avec une interface de chat partageable | Cloud gratuit : crédits offerts au démarrage | Créer un agent conversationnel que vous pouvez envoyer à quelqu'un |
| **Groq** (console.groq.com) | API de modèles de langage, très rapide, compatible OpenAI | Gratuite : clé API avec limites de débit, sans carte bancaire | Donner un « cerveau » gratuit à vos automatisations |

**La logique :** n8n est le chef d'orchestre, Groq est le musicien, Dify est la salle de concert. Vous n'avez besoin que d'un compte gratuit pour chacun.

> ⚠️ **Honnêteté d'abord :** les offres gratuites ont des limites (nombre d'exécutions, vitesse). Pour un premier agent qui tourne une fois par semaine, elles sont largement suffisantes. Vous n'aurez besoin de payer que le jour où vous voudrez automatiser des milliers de tâches.

---

## 3. Le mini-workflow réel, pas à pas (25 minutes)

**Votre mission :** un agent de veille qui, chaque lundi à 9 h, lit les dernières actualités tech, les résume en 3 puces en français, et vous les envoie sur Telegram. Tout est gratuit.

### Étape 1 — Créer vos comptes (5 minutes)

1. Allez sur **n8n.io** → « Start for free » → créez un compte avec votre email. Restez sur l'offre gratuite (Free).
2. Allez sur **console.groq.com** → « Sign in » (compte Google ou email) → menu **API Keys** → « Create API Key » → copiez la clé (elle commence par `gsk_`). Gardez-la dans un fichier texte : c'est votre « laissez-passer ».
3. Sur Telegram, écrivez à **@BotFather** → commande `/newbot` → choisissez un nom (ex. « Mon agent de veille ») → BotFather vous donne un **token** (il ressemble à `123456:ABC-DEF...`). Copiez-le aussi.

> 🔐 **Règle d'or :** une clé API est comme un mot de passe. Ne la partagez jamais, ne la mettez jamais dans un email. Si elle fuit, vous pouvez la révoquer depuis le tableau de bord Groq.

### Étape 2 — Monter le workflow dans n8n (15 minutes)

1. Dans n8n, cliquez sur **« + Create Workflow »**, puis donnez un nom : `Agent de veille IA`.
2. **Premier node — le déclencheur :** cherchez **Schedule Trigger** dans la palette à gauche, glissez-le sur le canvas. Configurez : « Field Type » = *Weeks*, « Trigger at Hour » = *9*, « Trigger at Minute » = *0*, « Trigger on Weekdays » = *Monday*. C'est votre « chaque lundi à 9 h ».
3. **Deuxième node — l'outil lecture :** cherchez **RSS Read** et branchez-le après le Schedule Trigger. Dans « RSS Feed URL », mettez un vrai flux, par exemple :
   `https://www.lemonde.fr/informatique/rss_full.xml`
   (vous pouvez en tester d'autres en cherchant « flux RSS » sur le site de votre choix).
4. **Troisième node — le cerveau :** cherchez **OpenAI** (n8n le propose même avec des clés compatibles), branchez-le après RSS Read, et configurez :
   - **Base URL :** `https://api.groq.com/openai/v1`
   - **API Key :** votre clé `gsk_...`
   - **Model :** `llama-3.3-70b-versatile`
   - **Messages :** Content = `Résume ces actualités en 3 puces en français, maximum 12 mots par puce. Actualités : {{ $json.title }}`
   > 💡 Le `{{ $json... }}` est le langage de n8n pour dire « prends les données du node précédent ». C'est votre premier pas dans la logique d'automatisation.
5. **Quatrième node — la livraison :** cherchez **Telegram**, branchez-le après OpenAI. Config :
   - **Credential :** créez une nouvelle credential Telegram avec le token de BotFather.
   - **Chat ID :** envoyez un message à votre bot, puis ouvrez `https://api.telegram.org/bot<VOTRE_TOKEN>/getUpdates` dans votre navigateur : le `chat.id` est le nombre qui apparaît dans la réponse. Collez-le.
   - **Text :** `📬 Veille de la semaine :\n{{ $json.output }}`
6. Cliquez sur **« Execute workflow »** en bas à droite. Vous devez voir passer les données d'un node à l'autre, puis le message arriver sur votre téléphone.

### Étape 3 — Lancer l'agent (5 minutes)

- Cliquez sur **« Active »** en haut à droite du workflow : l'agent est désormais en service.
- **Testez le déclencheur :** dans le Schedule Trigger, cliquez sur « Test step » puis « Execute workflow » pour simuler un lundi matin.
- Félicitations : **vous venez de créer un agent.** Il lira, résumera et enverra tout seul, chaque lundi, sans que vous touchiez à rien.

**Si quelque chose coince :** 9 fois sur 10, c'est la clé API (espace en trop au début/fin) ou le Chat ID. Vérifiez l'onglet « Executions » de n8n : il montre où le workflow s'est arrêté, avec le message d'erreur exact.

---

## 4. L'exercice de la semaine (20 minutes)

**Mission : l'agent correcteur de vos emails.**

1. Reprenez le workflow de veille et dupliquez-le (« ⋯ » → Duplicate).
2. Remplacez le RSS Read par un node **Webhook** (déclencheur qui attend une requête) *ou* gardez le Schedule Trigger et changez la mission.
3. Changez le message du modèle par :
   `Corrige ce texte en français impeccable, en gardant le ton : {{ $json.text }}`
4. Branchez un node **Email (SMTP)** ou restez sur Telegram pour recevoir le résultat.
5. Envoyez-lui un de vos vrais emails mal rédigés (celui que vous n'avez jamais osé envoyer). Comparez.

**Critère de réussite :** vous avez utilisé l'agent sur **un vrai texte à vous**, et vous avez reçu une correction que vous jugez meilleure que votre brouillon. Si oui : la compétence est acquise.

**Pour aller plus loin :** ajoutez un node « If » (condition) pour que l'agent ne corrige que les emails de plus de 50 mots, ou branchez un second modèle qui vérifie la correction. Un agent se construit par petites briques.

---

## 5. Ressources

- **Documentation n8n (en français)** : docs.n8n.io — la page « Workflow » et « Nodes » suffisent pour ce numéro.
- **Documentation Dify** : docs.dify.ai — pour l'étape suivante (agents conversationnels avec mémoire).
- **Console Groq** : console.groq.com — vos clés et les modèles disponibles.
- **BotFather** : t.me/BotFather — pour créer vos bots Telegram.
- **Glossaire express** :
  - **Node** : un bloc d'action dans un workflow (lire, résumer, envoyer).
  - **Workflow** : l'enchaînement de nodes qui forme votre automatisation.
  - **Trigger** : l'événement qui démarre le workflow (horaire, message, clic).
  - **API** : le « guichet » qui permet à deux programmes de se parler.
  - **Clé API** : votre laissez-passer pour utiliser ce guichet.
  - **LLM** : le « cerveau » du système (Large Language Model).

---

## À la semaine prochaine

Vous avez construit votre premier agent. La semaine prochaine : **« Data science sans maths »** — vous ouvrirez un vrai jeu de données et vous en tirerez trois visualisations, sans une seule équation. Rien à installer : tout se passe dans votre navigateur.

**En attendant :** un conseil. L'erreur n° 1 des débutants, c'est de tout lire et de ne rien construire. Vous venez de construire. Continuez sur cette lancée : même dix minutes par semaine valent mieux que dix heures de vidéos.

— IA Pratique · « L'IA qui se retient, c'est l'IA qu'on applique. »
