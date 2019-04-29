# Summary

This repository contains several implementation of the BAC ("Basic Access Control") protocol for passports for the DeepSec prover tool. We introduce an updated model ( `deepsec/british-passport-nondet-choice.dps`), with the following changes compared to the "original" model (`deepsec/british-passport-original.dps`, copied from the original deepsec repository without change):

- The passport and reader roles accept custom names for channels, allowing the option of modelling an attacker who can detect which roles (or possibly agents) are exchanging messages.
- The processes which are being checked for equivalence are changed. Instead of checking 
<p align="center">(A | B) ≈<sub>T</sub>? (A | A),</p>

we check

<p align="center">(A|(A+B)) ≈<sub>T</sub>? (A | A).</p>

Here, | can be interpreted as parallel composition, + as a nondeterministic choice, and ≈<sub>T</sub>? a check for Trace Equivalence of processes.

These changes are performed to demonstrate that varying definitions of equivalence, unlinkability (in terms of this equivalence) and the underlying adversary model can produce different results. As discussed in our paper, this demonstrates the need for thoroughness and consistency in defining a security model.

# Execution

The DeepSec tool can be gotten from the repository: 
` https://github.com/DeepSec-prover/deepsec`
. If DeepSec is already present on your machine you can execute the included model with the command
`deepsec <file>`. Depending on your install method, you may need to include an argument `-deepsec_dir <path to deepsec>` in order to correctly load the HTML file produced as output.

# Results

For the implementation in our model, the DeepSec tool gives a result of "equivalent processes" after almost 24 hours of computation. This is in contrast to the example included in the DeepSec tool, which returns "not equivalent" (usually in less than one second of computation). The trace produced by DeepSec for the original model has been reconstructed in the diagram below.



![Figure demonstrating the counterexample to trace equivalence given by running analysis on the included file](/figs/BAC-british-trace-equivalence.png"Deepsec Counterexample to Trace Equivalence")



This diagram demonstrates that the claim

<p align="center">(A | B) ≈<sub>T</sub>? (A | A),</p>

does not hold (i.e. the two processes are not **trace** equivalent). In particular, gives a trace that exists in the setting (A | B), but not in the setting (A | A) - in this case, it is when we "mix" the keys, which results in an error message in one setting but not in the other. Note that the setting (A | (A+B)) has this trace - its set of traces is clearly a superset of that of (A+B), while DeepSec demonstrates that it is the trivial superset (i.e. they are in fact equal).

We argue (in our paper) that this motivates the need for a stronger verification methodology. Indeed, the scenario given in the included file is closer to one that an adversary may face in the real-world: they must be able to tell the difference between the scenario when only one agent is present, and that where they do not know whether it is one or two agents.

Either way, note that the accepted definition of strong unlinkability is based not on trace equivalence but on **bisimulation**. As such a single trace is not sufficient to (dis)prove strong unlinkability. Both weak and strong unlinkability are generally argued over **infinite** duplication. Therefore while the DeepSec results give an indication of the existence of an attack on weak unlinkability, it is not sufficient to fully prove it.

DeepSec contains the required syntax for both infinite duplication and observational equivalence (which is related to, but not the same as, bisimulation). However, at the time of submission, support for both of these features is either unimplemented or unstable (i.e. leads to nontermination). We argue that the use of a theory built with bisimulation at its core should allow for analysis that is more faithful to the accepted definition of strong unlinkability, and thus more precise analysis of protocols.