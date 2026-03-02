# Bases du traitement du signal déterministe

## I/ Transformée de Fourier

### I.1) Premières définitions

On s'intéresse à une fonction de la variable $t$, $x(t)$. $x$ peut être à valeurs complexes, $t$ est une variable pouvant être éventuellement vectorielle. Dans le cadre de ce cours $t$ sera une variable scalaire que l'on considérera comme le temps.

Une fonction $x(t)$ satisfaisant les **conditions de Dirichlet** peut être décomposée sur une base infinie de fonctions sinusoïdales.

$$x(t) = \int_{-\infty}^{+\infty} X(f)\, e^{j2\pi ft}\, df \quad \Rightarrow \text{ décomposition intégrale de Fourier}$$

$$X(f) = \int_{-\infty}^{+\infty} x(t)\, e^{-j2\pi ft}\, dt \quad \Rightarrow \text{ transformée de Fourier}$$

**Conditions de Dirichlet** : suffisantes mais non nécessaires

1. $x(t)$ possède un nombre fini de discontinuités sur tout intervalle fini.
2. $x(t)$ possède un nombre fini d'extrema sur tout intervalle fini.
3. $\displaystyle\int_{-\infty}^{+\infty} |x(t)|\, dt < +\infty$ : absolument sommable.

**Exemple :** $x(t)$ est une impulsion rectangulaire : $x = \text{rect}_T(t)$

$$X(f) = \int_{-\infty}^{+\infty} x(t)\, e^{-j2\pi ft}\, dt = \int_{-T/2}^{T/2} A\, e^{-j2\pi ft}\, dt = A \left[\frac{e^{-j2\pi ft}}{-j2\pi f}\right]_{-T/2}^{T/2}$$

$$= \frac{-A}{j2\pi f}\left(e^{-j\pi fT} - e^{j\pi fT}\right) = \frac{A}{\pi f}\sin(\pi fT) = TA\, \text{sinc}(fT)$$

**Sinus cardinal :**

$$\text{sinc}(x) = \frac{\sin(\pi x)}{\pi x}$$

---

### I.2) Propriétés de la TF

On note $x(t) \rightleftharpoons X(f)$ la paire transformée de Fourier.

① **Linéarité :**

$$x_1(t) \rightleftharpoons X_1(f)$$

$$x_2(t) \rightleftharpoons X_2(f)$$

$$\alpha x_1(t) + \beta x_2(t) \rightleftharpoons \alpha X_1(f) + \beta X_2(f) \quad \forall\, \alpha, \beta \in \mathbb{C}$$

② **Changement d'échelle :**

$$x(t) \rightleftharpoons X(f)$$

$$x(\alpha t) \rightleftharpoons \frac{1}{|\alpha|}\, X\!\left(\frac{f}{\alpha}\right)$$

③ **Retard temporel :**

$$x(t) \rightleftharpoons X(f)$$

$$x(t - \tau) \rightleftharpoons e^{-j2\pi f\tau}\, X(f)$$

④ **Déplacement fréquentiel** *(modulation d'amplitude)* :

$$e^{j2\pi f_0 t}\, x(t) \rightleftharpoons X(f - f_0)$$

⑤ **Moyennes :**

$$X(0) = \int_{-\infty}^{+\infty} x(t)\, dt \quad \leftarrow \text{valeur moyenne de } x(t)$$

$$x(0) = \int_{-\infty}^{+\infty} X(f)\, df$$

⑥ **Différenciation dans le domaine temporel :**

$$x(t) \rightleftharpoons X(f) \qquad \frac{d^n x(t)}{dt^n} \rightleftharpoons (j2\pi f)^n\, X(f)$$

⑦ **Intégration :**

$$\int_{-\infty}^{+\infty} x(t)\, dt \rightleftharpoons \frac{X(f)}{j2\pi f}$$

⑧ **Dualité :**

$$x(t) \rightleftharpoons X(f)$$

$$X(t) \rightleftharpoons x(-f)$$

⑨ **Symétries et conjugaisons :**

$$x(t) \rightleftharpoons X(f)$$

$$\boxed{x^*(t) \rightleftharpoons X^*(-f)}$$

$$\boxed{x(-t) \rightleftharpoons X(-f)}$$

$$\boxed{x^*(-t) \rightleftharpoons X^*(f)}$$

**Cas particulier :** $x(t)$ est réel $\Rightarrow X(f) = X^*(-f)$ — symétrie hermitienne.
