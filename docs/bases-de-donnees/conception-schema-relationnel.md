# Conception d'un schéma relationnel

Une même BDD peut être représentée par plusieurs schémas relationnels.

Prenons par exemple la relation :

| sommet | face | année | altitude |
|--------|------|-------|----------|
| Everest | S | 1953 | 8848 |
| Annapurna | SO | 1972 | 8048 |
| Everest | N | 1970 | 8848 |

Cette représentation pose des problèmes lors de la mise à jour :

- **Insertion** : on ne peut insérer un sommet que si une première ascension de ce sommet a été réalisée.
- **Suppression** : supprimer une première peut entraîner de la perte de données (en l'occurrence l'altitude d'un sommet).
- **Modification** : modifier une altitude doit être fait sur toutes les lignes concernant le même sommet (**redondance**).

La solution apportée est de **normaliser** le schéma, qui consiste à décomposer les relations.

Formellement :

$$X = X_1 \cup \ldots \cup X_n \qquad R_i(X_i)$$

$$R(X) = (R_1(X_1) \text{ JOIN } R_2(X_2)) \text{ JOIN } \ldots \text{ JOIN } R_n(X_n)$$

*(On décompose la "grosse" table en de multiples "petites" tables à partir desquelles on peut reconstruire la table initiale à l'aide de jointures naturelles.)*

Une telle normalisation s'appuie sur les **dépendances fonctionnelles (DF)**.

Il y a une **dépendance fonctionnelle** entre un ensemble d'attributs X et un ensemble d'attributs Y d'une relation R, si dans toute extension R la valeur des attributs de X détermine fonctionnellement celle des attributs de Y.

On note : $X \rightarrow Y$

---

## Dépendances fonctionnelles

**Exemples :**

- $\text{nomSommet} \rightarrow \text{altitude}$
- $\text{nomSommet, face} \rightarrow \text{année}$

**DF triviales :** $\text{nomSommet, face} \rightarrow \text{nomSommet}$

À partir d'un ensemble $F$ de dépendances fonctionnelles, on construit la **fermeture de F**, notée $F^+$, avec les opérations suivantes :

- **Réflexivité** : si $Y \subseteq X$ ($Y$ est un sous-ensemble de $X$) alors $X \rightarrow Y$
- **Augmentation** : si $X \rightarrow Y$ alors $X \cup W \rightarrow Y \cup W$
- ⭐ **Transitivité** : si $X \rightarrow Y$ et $Y \rightarrow Z$ alors $X \rightarrow Z$

*(Pseudo-transitivité : si $X \rightarrow Y$ et $Y \cup W \rightarrow Z$ alors $X \cup W \rightarrow Z$)*

La recherche d'une bonne décomposition passe par l'utilisation des dépendances fonctionnelles.

À l'aide de ces DF et de la notion de clé, on va définir 4 degrés de normalisation qui indiquent la qualité de votre schéma relationnel.

---

## Dépendances fonctionnelles & clés

Un ensemble d'attributs X d'une relation $R(A_1, A_2, \ldots, A_n)$ est une **clé de R** si :

- $X \rightarrow A_1, A_2, \ldots, A_n$
- *(minimalité)* il n'existe pas de sous-ensemble strict Y de X tel que $Y \rightarrow A_1, A_2, \ldots, A_n$

Une même relation peut posséder plusieurs clés. On appelle **attribut clé** d'une relation R, un attribut qui fait partie d'une clé de R.

Un **attribut non-clé** est un attribut qui ne fait partie d'aucune clé.

Un ensemble d'attributs est une **super-clé** s'il contient une clé.
