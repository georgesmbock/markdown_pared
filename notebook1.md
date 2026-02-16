---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.19.1
kernelspec:
  name: python3
  display_name: Python 3 (ipykernel)
  language: python
rise:
  autolaunch: false
  slideNumber: true
  scroll: true
---

```{code-cell} ipython3
!pip show rise
```

# Cours Démo : Introduction à Python

Bienvenue dans ce cours interactif.  
Objectifs :
- Comprendre les bases de Python
- Exécuter du code simple
- Visualiser des résultats

```{code-cell} ipython3
# Affichage simple
print("Bonjour, bienvenue dans le cours de Python !")
```

## Variables et types de données

En Python, on peut stocker des valeurs dans des variables.  
Exemple :
- `x = 5` (entier)
- `y = 3.14` (flottant)
- `nom = "Georges"` (chaîne de caractères)


```{code-cell} ipython3
x = 5
y = 3.14
nom = "Georges"

print("x =", x)
print("y =", y)
print("nom =", nom)
```

## Exercice

Crée une variable `age` et affiche :  
`Je m'appelle Georges et j'ai <age> ans.`

```{code-cell} ipython3
!jupyter nbconvert notebook1.ipynb --to slides --post serve
```

```{code-cell} ipython3
!voila notebook1.ipynb
```
