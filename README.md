# Projet_P5

Projet Probabilités V

L'objectif de ce projet est d'estimer la longueur de câble sous-marin nécessaire pour relier deux côtes $A$ et $B$ en utilisant des simulations conditionnelles.
Le câble reposera sur le fond marin dont la profondeur est inconnue. Le segment $[AB]$ est discrétisé par une séquence de (N+1) points. On pose $x_0=A$ et pour $i=1,\dots,N$, $$x_i=x_0+i\Delta$$ où $$\Delta = \frac{AB}{N}$$ de telle sorte que $x_N=B$. On note $z(x)$ la profondeur du fond marin au point $x$ de telle sorte qu'on pourra estimer la longueur totale de câble nécessaire par la somme des longueurs sur les segments de la discrétisation :
$$l=\sum_{i=1}^N\sqrt{\Delta^2+(z(x_i)-z(x_{i-1}))^2}.$$

Enfin, notons que l'on dispose d'un ensemble de $n$ observations de la profondeur que l'on supposera situées sur des points de discrétisation $z(x_{j_1}),\dots,z(x_{j_n})$.

On adopte un modèle probabiliste pour la profondeur. On suppose que le vecteur des profondeurs sur les points de discrétisation $\mathbf{z}=(z(x_0),\dots,z(x_N))$ est la réalisation d'un vecteur aléatoire gaussien $\mathbf{Z}=(Z(x_0),\dots,Z(x_N))$ dont le vecteur d'espérance ne contient qu'une seule valeur $\mu$ répétée $N+1$ fois et dont la matrice de covariance $\Sigma$ a pour termes $\sigma_{ij}$ définis par $\sigma_{ij}=C(|x_i-x_j|)$ où $C$ est une fonction décroissante, traduisant le fait que deux points géographiquement proches ont tendance à avoir des profondeurs plus similaires que deux points éloignés.

On supposera que la matrice de covariance ainsi générée est définie-positive (en fait, $C$ sera choisie parmi les fonctions qui, appliquées aux termes d'une matrice de distance, produisent des matrices définie-positives).

Si on note $L$ la variable aléatoire donnant la longueur de cable nécessaire : $$L=\sum_{i=1}^N\sqrt{\Delta^2+(Z(x_i)-Z(x_{i-1}))^2},$$ un bon estimateur de $L$ est fourni par l'espérance conditionnelle
$$L^\star=E[L|Z(x_{j_1})=z(x_{j_1}),\dots,Z(x_{j_n})=z(x_{j_n})].$$

Cependant, cette quantité est difficilement accessible par le calcul. On va donc avoir recours à des simulations conditionnelles. C'est-à-dire que l'on va simuler un nombre $K$ de réalités (disons des réalisations du modèle probabiliste choisi), et sur chacune d'entre elle, la quantité de câble nécessaire sera évaluée. On disposera ainsi d'un échantillon $l_{(1)},\dots,l_{(K)}$ de longueures simulées. Puis on approchera l'espérance conditionnelle par $$L^\star=\sum_{k=1}^K l_{(k)}.$$

L'objectif de ce projet est donc d'écrire un code permettant d'effectuer cette simulation conditionnelle, puis de l'appliquer au jeu de données fourni et d'en déduire une estimation de la longueur de câble nécessaire.
