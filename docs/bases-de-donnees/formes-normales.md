# Différentes formes normales

## 1NF — Première forme normale

Une relation est en **première forme normale (1NF)** si tous les attributs prennent des valeurs atomiques (1 valeur).

**Exemple :**

| Lac | nomSommet | Pays |
|-----|-----------|------|
| Everest | Chine, Népal | ← *non atomique* |
| Annapurna | Népal | |

> *Loc n'est pas atomique*

C'est pourquoi on a créé la table `LOCALISATION(nomSommet, Pays)`.

---

## 2NF — Deuxième forme normale

Une relation est en **deuxième forme normale (2NF)** si elle est en 1NF et si chaque attribut non-clé dépend totalement et non-partiellement des clés.

**Exemple :**

| nomSommet | face | année | altitude |
|-----------|------|-------|----------|
| Everest | S | 1953 | 8863 |
| Annapurna | S | 1972 | 8195 |
| Everest | SO | 1975 | 8863 |

La clé de cette relation est `{ nomSommet, face }`.

Les attributs non-clé sont : `année` et `altitude`.

On observe les dépendances fonctionnelles suivantes :

- `nomSommet, face → altitude, année`
- `nomSommet → altitude`

Donc :
- `nomSommet, face → année`
- mais `nomSommet ↛ année`
- et `face ↛ année`

L'attribut `année` dépend totalement de la clé.

En revanche :

- `nomSommet, face → altitude`
- mais aussi `nomSommet → altitude`

L'attribut non-clé `altitude` dépend **partiellement** de la clé.

Donc la relation `Prom` est en 1NF mais **pas en 2NF**.

Pour obtenir un schéma relationnel en 2NF, il faut décomposer la relation `Prom` en 2 relations :

1. Identifier la DF partielle : `nomSommet → altitude`
2. Enlever de la relation l'attribut cible de cette DF (`altitude`)

**Première** :

| nomSommet | face | année |
|-----------|------|-------|
| Everest | S | 1953 |
| Annapurna | S | 1972 |
| Everest | SO | 1975 |

**Sommet** :

| nomSommet | altitude |
|-----------|----------|
| Everest | 8863 |
| Annapurna | 8195 |

> `nomSommet → altitude`

Cette décomposition a 2 qualités :

- **Préserve les DF** :
  - `nomSommet, face → année` (Première)
  - `nomSommet → altitude` (Sommet)
- **Sans perte de données** : la relation `Prom` s'obtient par jointure des relations `Première` et `Sommet`.

---

## 3NF — Troisième forme normale

Une relation est en **3ème forme normale (3NF)** si elle est en 1NF et s'il n'existe aucun attribut non-clé qui dépend fonctionnellement et non trivialement d'un ensemble d'attributs qui n'est pas une sur-clé.

> Si R est en 3NF, alors elle est en 2NF.

**Exemple :**

| Grimpeur | ville | Pays |
|----------|-------|------|
| Jossner | Berlin | Allemagne |
| Turing | Londres | Angleterre |
| Hillary | Londres | GB |

Les DF :
- `Grimpeur → ville, Pays`
- `ville → pays`

La relation est en 1NF. `Grimpeur` est la clé de cette relation.

`ville` et `pays` sont les attributs non-clés qui dépendent totalement de `Grimpeur` → 2NF (1NF avec une clé mono-attribut → 2NF).

Cette relation n'est **pas en 3NF** à cause de `ville → pays`.

```
Grimpeur → ville → pays
              ↑
         DF transitive
```

Pour normaliser la relation, il faut décomposer :
1. Isoler la DF transitive
2. Enlever l'attribut cible de la relation initiale

**S₁** :

| Grimpeur | ville |
|----------|-------|
| Jossner | Berlin |
| Turing | Londres |
| Hillary | Londres |

> `Grimpeur → ville`

**S₂** :

| ville | Pays |
|-------|------|
| Berlin | Allemagne |
| Londres | GB |

> `ville → Pays`

Cette décomposition préserve les DF :

```
grimpeur → ville → pays
```

Par transitivité on a : `grimpeur → pays`

Et elle est sans perte : `S = S₁ JOIN S₂ ON ville`

> **Résultat important** : Tout schéma relationnel admet une décomposition en 3NF qui préserve les dépendances fonctionnelles.

---

## BCNF — Forme normale de Boyce-Codd

Une relation R est en **forme normale de Boyce-Codd (BCNF)** si pour toute DF non triviale `X → Y`, X est une super-clé (ce qui n'apporte rien de superflu).

C'est la forme idéale mais on n'est pas assuré de l'existence d'une décomposition BCNF qui soit sans perte et qui préserve les DF.

**Exemple :**

`Adresse(rue, ville, CP)`

DF :
- `rue, ville → CP`
- `CP → ville`

Les clés candidates : `{rue, ville}` et `{rue, codePostal}`

→ Il n'y a pas d'attributs non-clé ⟹ 2NF et 3NF.

Elle n'est **pas en BCNF** à cause de `CP → ville` car `CP` à lui seul n'est pas une clé.

**Décomposition :**

- `CP(codePostal, ville)`
- `RC(rue, codePostal)`

On a perdu la DF `rue, ville → codePostal`.
