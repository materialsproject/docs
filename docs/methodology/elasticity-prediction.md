# Elasticity Predictions

## Introduction

The Materials Project (MP) provides a growing collection of elastic
constants calculated from first principles Density Functional Theory
(DFT). Please see [Elasticity calculations](/methodology/elasticity)
for details regarding the MP elasticity workflow [^1].

For compounds that have not yet been processed with the elasticity
workflow, the MP offers statistical learning (SL) predictions of the
Voigt-Reuss-Hill [^2] average bulk and shear moduli ($K_{VRH}$ and $G_{VRH}$,
respectively). The SL models were trained with a diverse set of 1,940
k-nary compounds, using the $K_{VRH}$ and $G_{VRH}$ moduli calculated by the
elasticity workflow.

## Formalism

Ensemble statistical learning techniques construct a predictor from a
collection or ensemble of weak learners. Each weak learner is either a
single descriptor or a function of just a few descriptors, which limits
the level of interaction between descriptors. Gradient boosting (GB) is
a very flexible ensemble technique, which makes few assumptions
regarding the form of the solution and iteratively builds a predictor
from a series of weak learners while minimizing the residual of a loss
function [^3]. GB implementations use regularization techniques to
reduce the risk of over-fitting, which typically include limiting the
level of interaction between descriptors, limiting the number of
iterations per some risk criteria, and employing shrinkage [^3]. At
each iteration, the weak learner that causes the greatest reduction in
the loss function’s residual is selected and added to the model,
however, when shrinkage is employed, each new term is attenuated by the
learning rate.

## Descriptors

The successful application of SL requires a set of descriptor candidates
that sufficiently explain the diversity of the phenomenon being learned.
We distinguish between composition and structural descriptors.
Composition descriptors are calculated from elemental properties and
only require knowledge of a compound’s composition. Structural
descriptors require knowledge of a compound’s specific structure and are
calculated using DFT.

## Citations

To cite elastic constant predictions within the Materials Project,
please reference the following works:

1.  "de Jong M, Chen W, Notestine R, Persson K, Ceder G, Jain A, Asta M,
    and Gamst A (2016) A Statistical Learning Framework for Materials
    Science: Application to Elastic Moduli of k-nary Inorganic
    Polycrystalline Compounds, Scientific Reports 6: 34256."
    [doi:10.1038/srep34256](http://dx.doi.org/10.1038/srep34256)
2.  "de Jong M, Chen W, Angsten T, Jain A, Notestine R, Gamst A, Sluiter
    M, Ande CK, van der Zwaag S, Plata JJ, Toher C, Curtarolo S, Ceder
    G, Persson KA, Asta M (2015) Charting the complete elastic
    properties of inorganic crystalline compounds. Scientific Data 2:
    150009."
    [doi:10.1038/sdata.2015.9](http://dx.doi.org/10.1038/sdata.2015.9)

## Authors

1.  Randy Notestine
2.  Maarten de Jong

## References

[^1]: de Jong M, Chen W, Angsten T, Jain A, Notestine R, Gamst A,
Sluiter M, Ande CK, van der Zwaag S, Plata JJ, Toher C, Curtarolo S,
Ceder G, Persson KA, Asta M (2015) Charting the complete elastic
properties of inorganic crystalline compounds. Scientific Data 2:
150009.

[^2]: Hill, R. The elastic behaviour of a crystalline aggregate.
Proceedings of the Physical Society. Section A 65, 349 (1952).

[^3]: Hastie, T., Tibshirani, R. & Friedman, J. The elements of
statistical learning: data mining, inference, and prediction. (Springer,
2011), second edn.

