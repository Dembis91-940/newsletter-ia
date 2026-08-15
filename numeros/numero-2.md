# IA PRATIQUE — NUMÉRO 02

**Titre :** Data science sans maths : commencez par l'analyse
**Durée :** 20 minutes · **Niveau :** débutant · **Coût :** 0 €
**Promesse :** à la fin de cette session, vous aurez chargé un vrai jeu de données, produit 3 visualisations qui racontent une histoire, et répondu à une vraie question avec des chiffres.

---

> **Le principe du numéro :** la data science, ça commence par regarder les données. Les maths viendront plus tard — et peut-être jamais, selon le métier que vous viserez.

## Ce que vous saurez faire dans 20 minutes

- Ouvrir un « notebook » gratuit dans votre navigateur (zéro installation)
- Charger un vrai jeu de données
- Poser 3 types de questions à vos données (comparer, distribuer, relier)
- Produire 3 graphiques qui répondent visuellement à ces questions

---

## 1. La leçon en 5 minutes : l'analyse avant les maths

Il y a un malentendu : beaucoup croient que la data science commence par les équations. C'est faux. Elle commence par **une question et un tableau de données**.

Un tableau de données, vous en manipulez déjà : une liste de courses, un planning, un tableur. La data science, c'est la même chose, en plus grand et avec des outils conçus pour ça. **pandas** est l'outil principal : une bibliothèque Python qui lit, trie, filtre et résume les tableaux. Vous n'aurez besoin d'aucune formule au-delà de la moyenne et du pourcentage — et pandas les calcule pour vous.

Les 3 questions de base que pose un analyste :

1. **Comparer** : « Ce groupe est-il différent de celui-ci ? » → graphique en barres
2. **Distribuer** : « Comment les valeurs sont-elles réparties ? » → histogramme
3. **Relier** : « Deux choses varient-elles ensemble ? » → nuage de points

C'est tout. Le reste (statistiques, tests, modèles) vient après, quand vous aurez besoin de répondre à des questions plus fines.

**À retenir :** vous n'apprenez pas les maths pour faire de la data. Vous apprenez à poser des questions et à lire des graphiques. Les maths s'invitent plus tard, seulement si vous en avez besoin.

---

## 2. L'atelier : pandas en 20 minutes, dans votre navigateur

On utilise **Google Colab** : un notebook Python gratuit qui tourne dans le navigateur. Rien à installer, rien à payer.

### Étape 1 — Ouvrir votre atelier (2 minutes)

1. Allez sur **colab.research.google.com** et connectez-vous avec un compte Google.
2. « Nouveau notebook » → un carnet vide s'ouvre, avec une cellule de code.
3. Chaque bloc de code ci-dessous se colle dans une cellule (cliquez sur « + Code » pour en ajouter). Exécutez avec **Maj + Entrée**.

### Étape 2 — Charger un vrai jeu de données (3 minutes)

Collez ceci dans la première cellule et exécutez :

```python
# Installation de seaborn : elle contient des jeux de données réels
!pip install -q seaborn

import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Le jeu de données "tips" : les additions et pourboires d'un restaurant américain
df = sns.load_dataset("tips")
print("Nombre de lignes :", len(df))
df.head()
```

**Ce que vous voyez :** un tableau de 244 additions réelles, avec le montant (`total_bill`), le pourboire (`tip`), le jour (`day`), le moment (`time`) et la taille de la table (`size`). C'est un vrai jeu de données, collecté par un serveur qui notait ses additions en 1990. **Un tableau + une question = de la data science.**

### Étape 3 — Faire connaissance avec les données (3 minutes)

```python
# Un résumé automatique : chaque colonne, son type, ses valeurs manquantes
df.info()
```

```python
# Les statistiques de base, calculées par pandas (moyenne, min, max...)
df.describe()
```

**Lisez ça comme un humain :** l'addition moyenne est d'environ **19,8 $**, le pourboire moyen **3 $**. On a déjà une histoire : le pourboire, c'est environ 15 % de l'addition. Vérifions avec une question de comparaison.

### Étape 4 — Question 1, comparer : le pourboire moyen selon le jour (4 minutes)

```python
# Graphique 1 : le pourboire moyen pour chaque jour de la semaine
sns.barplot(data=df, x="day", y="tip")
plt.title("Pourboire moyen par jour")
plt.show()
```

**Ce que ça dit :** le dimanche, les pourboires sont plus élevés. Question suivante : est-ce parce que les additions sont plus grosses, ou parce que les clients sont plus généreux ? Un analyste pose toujours la question d'après.

### Étape 5 — Question 2, distribuer : la répartition des additions (4 minutes)

```python
# Graphique 2 : la distribution des montants d'addition
sns.histplot(data=df, x="total_bill", bins=30, color="#064BD9")
plt.title("Répartition des additions")
plt.show()
```

**Ce que ça dit :** la plupart des additions se concentrent entre 10 $ et 25 $, avec une longue traîne de grosses additions rares. C'est la forme classique d'une distribution : on l'appelle « en cloche » quand elle est symétrique, ici elle penche à gauche.

### Étape 6 — Question 3, relier : l'addition et le pourboire (4 minutes)

```python
# Graphique 3 : le pourboire en fonction du montant de l'addition
sns.scatterplot(data=df, x="total_bill", y="tip")
plt.title("Pourboire en fonction de l'addition")
plt.show()
```

**Ce que ça dit :** plus l'addition est grosse, plus le pourboire est élevé — les points montent en diagonale. C'est une **corrélation** : deux variables qui varient ensemble. On peut même estimer la règle du restaurant : environ 15 % de l'addition.

---

## 3. Lire vos graphiques : le réflexe de l'analyste

Vous avez maintenant trois graphiques. Voici le raisonnement professionnel qui va avec :

1. **Je compare** (barres) → « le dimanche se distingue des autres jours ».
2. **Je distribue** (histogramme) → « la majorité des additions sont modestes ».
3. **Je relie** (nuage de points) → « les deux variables suivent la même direction ».

Chaque graphique répond à une question, et **chaque réponse en pose une nouvelle**. C'est exactement le travail d'analyse : un dialogue avec les données. La prochaine étape (compter, tester, modéliser) ne sert qu'à rendre ce dialogue plus précis — elle ne change pas la méthode.

> ⚠️ **Piège à éviter :** une corrélation n'est pas une cause. Les gros pourboires accompagnent les grosses additions, mais cela ne prouve pas que « payer plus rend généreux ». On dit : corrélation n'est pas causalité. Gardez ce réflexe en tête, il vous évitera 90 % des erreurs d'interprétation.

---

## 4. L'exercice de la semaine (15 minutes)

**Mission : analysez un autre vrai jeu de données — les manchots de Palmer.**

Les manchots (penguins), c'est le jeu de données le plus célèbre pour apprendre : 344 manchots de 3 espèces, mesurés dans la vraie vie par une équipe de recherche.

1. Reprenez votre notebook et remplacez `tips` par `penguins` :
   `df = sns.load_dataset("penguins")`
2. Explorez avec `df.info()` et `df.head()`.
3. Répondez à ces 3 questions avec 3 graphiques (réutilisez les mêmes fonctions) :
   - **Comparer** : quelle espèce a le plus long bec en moyenne ? (`sns.barplot(data=df, x="species", y="bill_length_mm")`)
   - **Distribuer** : comment se répartit la masse des manchots ? (`sns.histplot(data=df, x="body_mass_g")`)
   - **Relier** : la longueur des ailes et la masse varient-elles ensemble ? (`sns.scatterplot(data=df, x="flipper_length_mm", y="body_mass_g")`)

**Critère de réussite :** vous avez produit 3 graphiques ET vous pouvez raconter ce qu'ils montrent en 2 phrases chacun, à voix haute. Si vous savez le dire, vous savez le faire.

---

## 5. Ressources

- **Google Colab** : colab.research.google.com — votre atelier gratuit, sans installation.
- **Aide-mémoire pandas (en français)** : « pandas cheat sheet » — imprimez-le, c'est le seul document dont vous aurez besoin pendant des mois.
- **Seaborn gallery** : seaborn.pydata.org/examples — des dizaines de graphiques prêts à copier.
- **Glossaire express** :
  - **DataFrame** : le tableau de pandas (lignes + colonnes).
  - **Series** : une seule colonne de ce tableau.
  - **`head()` / `info()` / `describe()`** : vos 3 premiers réflexes (voir, comprendre, résumer).
  - **Histogramme** : la répartition des valeurs d'une colonne.
  - **Corrélation** : deux variables qui varient ensemble (positif : même direction ; négatif : directions opposées).
  - **Causalité** : l'une provoque l'autre. Beaucoup plus rare que la corrélation.

---

## À la semaine prochaine

Vous savez charger des données et les faire parler. La semaine prochaine : **« Gagner de l'argent avec l'IA : les 5 pistes qui marchent en 2026 »** — avec les tarifs honnêtes et la vérité sur le travail nécessaire. Aucune promesse de richesse facile : uniquement des chemins réels.

**En attendant :** ouvrez un fichier qui vous appartient — vos dépenses du mois, vos notes de cours — et posez-lui une question de comparaison. La compétence, c'est de l'habitude.

— IA Pratique · « L'IA qui se retient, c'est l'IA qu'on applique. »
