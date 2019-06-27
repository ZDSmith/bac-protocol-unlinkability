# Summary

This repository is presented as part of a submission for ESORICS 2019. In particular, in the `deepsec` folder, we provide a new implementation of the passport BAC protocol, making use of the nondeterministic choice operator (+) in order to more faithfully model weak unlinkability

An in-depth `README.md` file that can be found in the `deepsec` folder, or a short summary follows.

As part of our experiment we also created a custom implementation of the passport role in the BAC protocol that can be run on an android smartphone. This implementation will be released at a later date.



## DeepSec Implementation

The `deepsec` folder contains two implementations of the BAC protocol. One is copied faithfully from the original deepsec repository (located at [https://github.com/DeepSec-prover/deepsec](https://github.com/DeepSec-prover/deepsec) ). The other is one we have prepared for this submission.

The key observation of these two code files is that a change in the modelling parameters leads to DeepSec confirming an attack on trace equivalence in one setting, and showing that no attack exists in another. We make the following arguments:

* The model that we present (using the (+) operator) gives a closer approximation to the definition of weak unlinkability that is accepted in the literature
* Precision in the definitions used is absolutely required to ensure that we, as a community, have a consistent understanding of our security definitions. Many abstractions or simplifications that are made to aid analysis can incidentally affect the outcome
