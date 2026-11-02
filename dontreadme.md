# TD/TP 2 – Cryptologie avancée (ENSTA Alger, 4e année SS)
Binôme : Nom1 Prénom1 / Nom2 Prénom2

## Contenu du dossier
- `exercice1.py` : exponentiation rapide en Python (6 versions).
- `exercice2.py` : `fusion` et `karatsuba`.
- `exercice3.py` : nombre d'inversions d'une permutation (tri fusion modifié).

Exécution : `python3 exercice1.py` (idem pour 2 et 3). Chaque fichier contient des tests.

## Exercice 1
Les programmes OCaml sont réécrits tels quels. Complexités (multiplication = opération fondamentale) :
| Version | Équation | Complexité |
|---|---|---|
| itérative / récursive naïve | C(n) = n | O(n) |
| rapide, 2 appels récursifs | C(n) = 2C(n/2)+2, q=2, γ=0 | O(n) |
| rapide, 1 appel récursif | C(n) = C(n/2)+2, q=1, γ=0 | O(log n) |
| récursive terminale / itérative | (p+1) itérations, p=⌊log2 n⌋ | O(log n) |

## Exercice 2 – Karatsuba
1. `fusion(A,B,C,n)` calcule A + X^(n/2)·B + X^n·C par simples décalages : O(n).
2. `karatsuba(a,b)` : on écrit A = A1 + X^(n/2)A2, B = B1 + X^(n/2)B2, puis
   - P1 = A1·B1, P2 = A2·B2, P3 = (A1+A2)(B1+B2)
   - A1·B2 + A2·B1 = P3 − P1 − P2
   - résultat = fusion(P1, P3−P1−P2, P2).

   Équation : C(n) = 3C(n/2) + O(n). Théorème 1 avec q=3, γ=1 : log2(3) ≈ 1,585 > 1, donc
   **C(n) = O(n^1,585)**, mieux que O(n²) du produit naïf.
   Les tests aléatoires comparent le résultat au produit naïf.

## Exercice 3 – Inversions
Idée : tri fusion. On compte les inversions de la moitié gauche, de la moitié droite, puis celles
« croisées » pendant la fusion : quand un élément d[j] de droite est placé avant les éléments
restants g[i:], il forme une inversion avec chacun d'eux, soit len(g) − i inversions.
Équation : C(n) = 2C(n/2) + O(n), q=2, γ=1, log2(q)=γ donc **C(n) = O(n log n)**.
Exemple : σ = (2 1 3 5 7 4 6) → inversions (2,1), (5,4), (7,4), (7,6) = **4**.
