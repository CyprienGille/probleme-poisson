# Problème de Poisson

 *Matlab*

---
## Description
Ce projet implémente la résolution de **l'équation de la chaleur stationnaire**, aussi appelée [équation de Poisson](https://fr.wikipedia.org/wiki/%C3%89quation_de_Poisson), dans le cas de deux chambres possédant:

- une fenêtre et une porte non isolantes ([conditions aux limites de Dirichlet](https://fr.wikipedia.org/wiki/Condition_aux_limites_de_Dirichlet) non-homogènes)
- des murs isolants ([conditions aux limites de Neumann](https://fr.wikipedia.org/wiki/Condition_aux_limites_de_Neumann))
- un radiateur (terme source localisé)

Pour résoudre l'équation de Poisson, ce code implémente les [**schémas d'Euler explicites et implicites.**](https://fr.wikipedia.org/wiki/M%C3%A9thode_d%27Euler)

## Fichiers

`run.m` permet de lancer l'évaluation des cas présentés dans le tableau ci-dessous avec des paramètres ajustables.

| Fichier        | Solution      | Géométrie |
| :------------- |:-------------:|---|
| `poisson_stat1.m`      | Exacte | Chambre 1 | 
| `poisson_stat2.m`      | Exacte | Chambre 2 | 
| `poisson_instat1_exp.m`      | Euler explicite | Chambre 1 | 
| `poisson_instat2_exp.m`      | Euler explicite | Chambre 2 |
| `poisson_instat1_imp.m`      | Euler implicite | Chambre 1 |
| `poisson_instat2_imp.m`      | Euler implicite | Chambre 2 |
| `poisson_instat_imp_factorise.m` | Euler implicite factorisé | Chambre 1 |

`delsq.m` implémente le calcul de la matrice du [Laplacien discret](https://fr.wikipedia.org/wiki/Laplacien_discret) dans le cadre de la méthode des différences finies, selon un schéma à 5 points. Cette fonction est souvent déjà incluse dans des distributions de Matlab/Octave.

Note: Bien que le but soit de suivre l'evolution de la température avec le temps, j'ai également implémenté les solutions directes (i.e. stationnaires), ce qui permet de contrôler la convergence avec un critère de proximité avec la solution exacte.

### Note sur `poisson_instat_im_factorise.m`

Le schéma d'Euler implicite est plus lent (que l'explicite) car plus gourmand en calcul (il nécessite la résolution d'un système linéaire à chaque pas de temps). Il est possible de l'optimiser à l'aide d'une factorisation LU - c'est ce j'ai implémenté dans `poisson_instat_im_factorise.m`.
