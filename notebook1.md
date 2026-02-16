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
---

+++ {"editable": false, "slideshow": {"slide_type": "slide"}}

# Cours Démo : Introduction à Python

Bienvenue dans ce cours interactif.  
Objectifs :
- Comprendre les bases de Python
- Exécuter du code simple
- Visualiser des résultats

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: slide
---
# Affichage simple
print("Bonjour, bienvenue dans le cours de Python !")
```

+++ {"editable": false, "slideshow": {"slide_type": "slide"}}

## Variables et types de données

En Python, on peut stocker des valeurs dans des variables.  
Exemple :
- `x = 5` (entier)
- `y = 3.14` (flottant)
- `nom = "Georges"` (chaîne de caractères)


```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: slide
---
x = 5
y = 3.14
nom = "Georges"

print("x =", x)
print("y =", y)
print("nom =", nom)
```

+++ {"editable": false, "slideshow": {"slide_type": "slide"}}

## Exercice

Crée une variable `age` et affiche :  
`Je m'appelle Georges et j'ai <age> ans.`

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: subslide
---
age = 30
print(f"Je m'appelle {nom} et j'ai {age} ans.")
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: skip
---
!jupyter nbconvert notebook1.ipynb --to slides --post serve
```

```{code-cell} ipython3

```
