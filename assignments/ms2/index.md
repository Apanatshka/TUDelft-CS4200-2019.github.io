---
layout: page
title: "Milestone 2: Semantic Analysis"
excerpt: "Milestone 2: Semantic Analysis"
tags: ["assignment"]
context: assign
subcontext: ms2
---

{% include _toc.html %}

The lab descriptions for this milestone are currently being revised.
**You should not work on these labs until revision is complete**, because
important aspects will change.
{: .notice .notice-warning}

In this milestone, the MiniJava editor from the previous milestone is extended with semantic analyses. The extended editor should be able

* to resolve references in a MiniJava program,
* to calculate types of MiniJava expressions,
* to report semantic errors, warnings, and notes, and
* to provide semantic code completion.

## Initial Projects

We provide you with a fresh MiniJava editor project, which covers the concrete and abstract syntax of MiniJava and desugarings.
For grading purposes, you are required to use this project as a starting point for milestone 2.
You should use `MiniJava-tests-names` for assignment 5 and `MiniJava-tests-types` for assignment 7.

## Resources

You can find the *MiniJava Language Reference Manual* in the appendix of the book
*Modern Compiler Implementation in Java* (2nd edition).
The relevant pages are available on [Google books](http://books.google.com/books?id=JNs6fWkJZbAC&pg=PA484).

The [MiniJava project](http://www.cambridge.org/us/features/052182060X/)
by Joao Cangussu, Jens Palsberg and Vidyut Samanta provides some example programs
and an HTML version of the reference manual.

The following research papers cover relevant topics of this milestone:

1. L. Kats, R. Vermaas, E. Visser: [Integrated Language Definition Testing: Enabling Test-Driven Language Development](http://swerl.tudelft.nl/twiki/pub/Main/TechnicalReports/TUD-SERG-2011-011.pdf), OOPSLA 2011
2. P. Neron, A. Tolmach, E. Visser, G. Wachsmuth: [A Theory of Name Resolution](http://swerl.tudelft.nl/twiki/pub/Main/TechnicalReports/TUD-SERG-2015-001.pdf), ESOP 2015
3. H. van Antwerpen, P. Neron, A. Tolmach, E. Visser, G. Wachsmuth: [A Constraint Language for Static Semantic Analysis based on Scope Graphs](http://swerl.tudelft.nl/twiki/pub/Main/TechnicalReports/TUD-SERG-2015-012.pdf), PEPM 2016
