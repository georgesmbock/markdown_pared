---
jupytext:
  notebook_metadata_filter: rise
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
rise:
  auto_select: first
  autolaunch: false
  centered: false
  controls: false
  enable_chalkboard: true
  height: 100%
  margin: 0
  maxScale: 1
  minScale: 1
  scroll: true
  slideNumber: true
  start_slideshow_at: selected
  transition: none
  width: 90%
---

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

<center>

# Introduction générale - Cours 1

## Mise en place des données



+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Sommaire

</center>

1. Analyse de données en général
 
2. Analyse de données en Python et rappels de stats

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### À quelles questions répond une analyse de données?

* Quelles sont les *données* ? 
* Quelle est notre *objectif* et comment y répondre (par quels outils statistiques) ?
* Quels sont les résultats (nos *observations*) ?
* Quelles sont les conclusions (notre *interprétation*) ?

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

#### Quelles sont les *données* ?

Avant de commencer, il faut mettre en contexte vos données. Commencez par décrire en quelques mots la table que vous avez, c'est-à-dire indiquez le nombre de lignes, de colonnes et vérifiez que vous comprenez bien ce qu'il y a dedans (est-ce qu'on attend des chiffres ou des mots?)

```{code-cell}
---
editable: true
slideshow:
  slide_type: slide
tags: []
---
## 1. Téléchargement de la liste des prénoms si ce n'est déjà fait

!if [ ! -f liste_des_prenoms.csv ]; then  \
    curl --http1.1 https://opendata.paris.fr/explore/dataset/liste_des_prenoms/download/\?format\=csv\&timezone\=Europe/Berlin\&lang\=fr\&use_labels_for_header\=true\&csv_separator\=%3B -o liste_des_prenoms.csv; \
fi


#Importation des librairies et chargement de la table
import pandas as pd
prenoms = pd.read_csv('liste_des_prenoms.csv', sep=';')

#Début du tableau
prenoms.head()

#prenoms.describe()
```

```{code-cell}
---
editable: true
jupyterlab-deck:
  layer: fragment
slideshow:
  slide_type: fragment
tags: []
---
#Noms des colonnes
prenoms.columns
```

```{code-cell}
---
editable: true
jupyterlab-deck:
  layer: fragment
slideshow:
  slide_type: fragment
tags: []
---
# Dimensions de la table
prenoms.shape
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---

```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

#### Quel est notre *objectif* et comment y répondre (par quels outils statistiques) ?

Avec des données on peut faire tout et n'importe quoi mais c'est leur étude critique qui est intéressante. L'objectif correspond à la question à laquelle on cherche à répondre. Une question bien définie permet d'identifier les tests que l'on veut faire; les données que l'on va traiter.

Vous répondrez à  ce genre de question en TP:

* *Quel est le prénom le plus donné à Paris ?*
* *en 2010 ?*
* *Pour le sexe F ?*
* *M ?*
* *etc.*

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

#### Quels sont les résultats (nos *observations*)?

Ce point est essentiel, voire le plus important et pourtant il est souvent oublié. **OBSERVEZ** vos résultats : **décrivez** vos figures (que représentez vous sur l'axe des *x* et des *y* ?)

#### Quelles sont les conclusions (notre *interprétation*) ?

L'objectif est que vous soyez capable de diférencier vos observations de vos interprétations, ce sont 2 choses différents !!

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Le travail de data scientist

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

## Analyse de données *en Python*

Dans cette UE, vous allez calculer (et programmer) en Python 3. 

**Pourquoi Python?**

1. Python est du logiciel libre
2. Mondialement utilisé avec une large documentation (principalement en anglais!)
3. Avec de nombreuses librairies complètes et stables. En science des données, nous utiliserons principalement:
    * **Pandas** pour la structuration et manipulation des données; `import pandas as pd`
    * **Numpy** pour les calculs numériques, `import numpy as np`
    * **Matplotlib** pour la visualisation
    * **Scikit-learn** pour l'apprentissage statistique
  
Connaissez vous ces librairies ?

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Chargement des données 

#### Présentation de la librairie PANDAS
Depuis 2008, pandas (**pan**el **da**ta) implémente des outils d'analyses, de statistiques et des éléments qui rappelent les bases de données (*features*).
Initialement développé pour les analyses de données financières, pandas s'est rapidement popularisé grâce à sa documentation détaillée.

* Documentation : https://pandas.pydata.org/docs/user_guide/index.html

*Prenez le temps de vous balader sur ce site, vous y trouverez toutes les informartions nécessaires.*

#### Structures de données

Nous allons apprendre à manipuler des données. A notre niveau, nos données seront stockées dans une table unique de 1, 2 ou >2 dimensions!

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

##### Séries et tableaux de données (avec Pandas)

* Les <a href="http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html#pandas.Series">Séries </a> sont des tables à une seule dimension (vecteurs de données ou une variable). Elles peuvent etre de plusieurs types (entiers, chaines de caractères, décimaux, autres -en anglais: *intergers, strings, floating, others*)

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

* Les <a href="http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html#pandas.DataFrame">tableaux
  de données</a> (*DataFrame* en anglais) sont des tables d'au moins 2
  dimensions (une colonne de dataframe peut etre vu comme une serie).
  Les tableaux contiennent des entêtes (*headers*) c'est à dire des noms de colonnes.

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

##### Remarques 
* Une colonne/une série doit être *homogène* (les éléments sont de même type) mais 2 colonnes d'une dataframe n'ont pas a être homogènes.

* Pandas permet de filtrer et prétraiter les données, deux étapes indispensable avant la modélisation statistique.

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
#dimensions
#Nombre de lignes, nombre de colonnes:\n Le header n'est pas comptabilisé
prenoms.head(n=15)
```

```{code-cell}
---
editable: true
jupyterlab-deck:
  layer: fragment
slideshow:
  slide_type: fragment
tags: []
---
#type de chaque colonne: dtypes pour datatypes
prenoms.dtypes
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
#description des données - on revient en détail dessus plus tard
prenoms.describe(include='all')
#Certains indicateurs statistiques ne sont valables que pour les variables numériques
#(ex. Nombre de prénoms déclarés, Annee, Nombre total cumule par annee), 
#et inversemment pour les non-numériques (ex. top, freq, etc. pour Sexe, Prenoms),
#d'où les NaN dans certaines situations.
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Préparation des données

* **Gestion des données manquantes (*missing data*)**

Il est courant qu'un jeu de données ait des données manquantes. Elles seront indiquées `NaN` comme *Not a Number*

On peut supprimer les valeurs manquantes ou bien les remplacer par une valeur (par ex. la moyenne, ou bien des 0)

```{code-cell}
---
editable: true
slideshow:
  slide_type: slide
tags: []
---
sexe = prenoms[['Prenoms','Annee']].describe(include='all')
sexe
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
sexe.dropna()
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
sexe.fillna(0)
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Filtrage et prétraitement 

* **Accès aux variables**

Nous pouvons isoler les sous-ensembles d'observations répondant à des critères (définis sur les champs). 

Nous utiliserons préférentiellement la méthode .loc[,] dans ce cadre (spécifique à pandas).

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
#tableau ne contenant plus que les lignes dont le prénom est féminin
# les ":" indiquent qu'on veut sélectionner toutes les colonnes
prenoms.loc[prenoms['Sexe']=="F",:]
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
#En fait la condition dans le loc renvoit une *Serie* de
#booléens si le Sexe est "F" ou pas
prenoms['Sexe']=="F"
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Analyse descriptive - Statistiques utiles
Maintenant qu'on a péparé la table, qu'on a sélectionné les lignes qui nous intéressent, on peut décrire nos données pour les analyser.

On peut commencer par décrire notre table en calculant:
* Mean (moyenne),
* range (gamme de valeurs), 
* variance, 
* standard deviation (écart type)

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### A quelles questions permettent-elles de répondre ?

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
## minimum
mini=prenoms["Nombre prénoms déclarés"].min()
mini
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
## maximum 
maxi=prenoms["Nombre prénoms déclarés"].max()
maxi
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
## mean, average , moyenne
prenoms["Nombre prénoms déclarés"].mean()
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
## variance
prenoms["Nombre prénoms déclarés"].var()
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
## standard deviation
prenoms["Nombre prénoms déclarés"].std()
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
## range
rangeprenoms = maxi - mini
rangeprenoms
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Rappels de statistiques 

#### Min and Max

La valeur la plus petite (respectivement la plus grande) du jeu de données

#### Moyenne (*mean*)

Somme des valeurs divisées par le nombre de valeurs (Sum of values divided by number of values).

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

#### Variance

La moyenne des carrés des écarts à la moyenne:
$var = \sigma^2 = \frac{1}{n} \sum_{i=1}^n (x_i - \mu)^2$.

Ca a l'air complexe mais c'est assez intuitif:

* Une variance est toujours positive. 
* Sa valeur ne peut être interprétée que par comparaison avec une autre variance ou un attendu (test statistique). 
* Une variance nulle (var =0) indique que toutes les observations sont égales à la moyenne. 
* Plus la variance est élévée plus les valeurs sont dispersées
* La variance est très sensible aux valeurs extrêmes.

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

#### écart-type (*standard deviation*)

Racine carrée de la variance : $\sigma= \sqrt var$

En pratique, on préférera commenter l'écart-type car il s'exprime dans les mêmes unités que les données !

#### Gamme de valeurs (*range*)

Différence entre la valeur la plus grande et la plus petite. Donne des infos sur l'ordre de grandeur des données étudiées

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Analyse descriptive - autres statistiques utiles (2)
On peut aussi calculer:
* médiane, 
* quartiles, 
* quantiles (*percentiles*)

Qu'est-ce que c'est ?

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
#A quelles questions permettent-elles de répondre ?
print("Mediane:\n",prenoms["Nombre prénoms déclarés"].median(),"\n\n")
print("Quartile:\n", prenoms["Nombre prénoms déclarés"].quantile([.25, .5, .75]),"\n\n")
print("5% et 95% quantile:\n", prenoms["Nombre prénoms déclarés"].quantile([.05,0.95]))
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

#### Médiane

Valeur telle que la moitié des données est plus petite que cette valeur

(pour une définition formelle il faut préciser un peu plus)

À quoi peut servir la médiane? Discutons du cas des prénoms.

#### Quartile

Vient du mot quart = 1/4 

Valeurs tels que, respectivement 25%, 50% et 75%, des données sont
plus petites que cette valeur

Même idée pour quantile ou percentile (percent pour pourcent %)

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Calculs numériques sur des tableaux - NumPy

#### Présentation de la librairie

Numpy est une bibliothèque optimisée pour le calcul numérique sur des
tableaux.

La syntaxe diffère un peu de celle de Pandas. Cela peut porter à
confusion mais les deux librairies sont tellement complémentaires que ce
serait une erreur de ne pas vous l'introduire.

* Documentation : https://numpy.org/doc/stable/reference/

#### Les tableaux Numpy: Array

Les tableaux NumPy, `array`, sont similaires, en tant que structures
de données, aux `vector` de C++: ils sont indexés par 0,1,... et
doivent être homogènes.

Ils offrent en plus la **vectorisation des calculs**: utiliser
l'homogénéité pour appliquer des opérations comme l'addition à tous
les éléments sans boucle `for` explicite.

Ils peuvent être de dimension `n` quelconque: 1, 2, ...

```{code-cell}
---
editable: true
slideshow:
  slide_type: slide
tags: []
---
import numpy as np

x = np.array([[1, 2, 3], [4, 5, 6]])
x
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
type(x)
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
x.shape
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: slide
tags: []
---
# Remarque : On utilisera des tables 3D lors des TP de classification !!
x3D = np.array([[[1,10,100,1000], [2,20,200,2000], [3,30,300,3000]], [[4,40,400,4000], [5,50,500,5000], [6,60,600,6000]]])
x3D
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
type(x3D)
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
x3D.shape
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

#### Accès aux valeurs

Les array sont indexés à partir de 0 (comme dans pandas!). Pour accéder aux valeurs, on utilise les crochets  et on sépare les dimensions par des virgules

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
#On peut ne sélectionner que la deuxième couche du tableau
x3D[1,:,:]

#Quelle dimension ?
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
#On peut ne sélectionner que la dernière colonne de la dimension 3
x3D[:,:,3]
#Quelle dimension ? Qu'utiliseriez vous?
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

### Calculs numériques

Les comparaisons et autres calculs arithmétiques peuvent se faire sur l'array complet. Les fonctions classiques telles que mean, std, sort, argmin

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
x3D.max()
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
x3D[:,:,2].max()
```

```{code-cell}
---
editable: true
slideshow:
  slide_type: fragment
tags: []
---
 x3D[:,:,2].argmax()
```

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

# Conclusions

* **Initiation à la science des données**
    * tout est données
    * l'observation est primordiale, l'interprétation vient après
    * domaine interdisciplinaire avec la finance, les maths, la bio, les RH, etc.

* **Langage Python 3**
    * Pandas, pour la structuration et la manipulation de tables de données
    * Numpy, pour les calculs numériques

+++ {"editable": true, "slideshow": {"slide_type": "slide"}, "tags": []}

# Perspectives

* **TP 1**
    * Utilisation de Pandas et NumPy
    * Analyse du jeu de données des prénoms + autres
    * Les exercices *sans* $\clubsuit$ sont à maîtriser d'une séance à l'autre (cela reste valide pour tous les TP)
    
* **CM 2 : analyses de données**
    * Visualisation des données: histogrammes
    * Corrélation et tests statistiques
