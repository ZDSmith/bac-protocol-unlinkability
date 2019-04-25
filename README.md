# Summary

This repository contains an implementation of the BAC ("Basic Access Control") protocol for passports for the DeepSec prover tool. It differs from the 'stock' implementation given in the examples folder of the DeepSec tool in two key ways:

- The passport and reader roles accept custom names for channels, allowing the option of modelling an attacker who can detect which roles (or possibly agents) are exchanging messages.
- The processes which are being checked for equivalence are changed. Instead of checking 
<p align="center">(A | B) ≈? (A | A),</p>

we check

<p align="center">(A|(A+B)) ≈? (A | A).</p>

Here, | can be interpreted as parallel composition, + as a nondeterministic choice, and ≈? a check for Trace Equivalence of processes.

These changes are performed to demonstrate that varying definitions of equivalence, unlinkability (in terms of this equivalence) and the underlying adversary model can produce different results. As discussed in our paper, this demonstrates the need for thoroughness and consistency in defining our security model.

# Execution

The DeepSec tool can be gotten from the repository: 
` https://github.com/DeepSec-prover/deepsec`
. If DeepSec is already present on your machine you can execute the included model with the command
`deepsec <file>`. Depending on your install method, you may need to include an argument `-deepsec_dir <path to deepsec>` in order to correctly load the HTML file produced as output.

# Results

For the implementation as given here, the DeepSec tool gives a result of "equivalent processes" after almost 24 hours of computation. This is in contrast to the example included in the DeepSec tool, which returns "not equivalent" (usually in less than one second of computation).

We argue (in our paper) that this motivates the need for a stronger verification methodology. Indeed, the scenario given in the included file is closer to one that an adversary may face in the real-world: they must be able to tell the difference between the scenario when only one agent is present, and that where they do not know whether it is one or two agents.