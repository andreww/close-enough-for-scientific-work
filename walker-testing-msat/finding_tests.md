# Finding tests for the Matlab Seismic Anisotropy Toolkit

Andrew M. Walker <a.walker@leeds.ac.uk> and James Wookey

During 2011 and 2012 we created MSAT, the Matlab Seismic Anisotropy
Toolkit [^1][^2]. We aimed to create a reusable, maintainable and documented
software suite to enable easer modelling of seismic anisotropy. This 
variation of seismic wave speed with direction is a property of many 
Earth materials that offers insight into processes such as the geometry
of cracks (important in hydrocarbon exploration) and the alignment
of crystals (a signature of high temperature deformation in the Earth's
interior). In creating MSAT we brought together existing software
already in use in our lab with new tools. Part of this effort involved
finding suitable tests for the various new and refurbished functions 
within MSAT. It turned out that many of the most useful of these 
functions are re-implementations of software described in published
scientific papers, often from the 1960s, '70s or '80s. We found that 
the example results commonly included in these papers make useful test
cases. Indeed, being able to reproduce these is a key to demonstrating 
scientific reproducibility. In this chapter we discuss some of the choices
we made when designing the test suite for MSAT and point out some of
the pitfalls we discovered during this process. Before discussing the 
tests themselves we provide some background on the scientific problem
the code is designed to solve and why we chose to build and release a 
toolbox to in the first place.

## Building MSAT

Seismologists study the propagation of elastic waves through the Earth (or
sometimes through the Moon or other planets). Analysis of the small surface 
displacement caused by these waves and recorded as seismograms by 
seismometers allows the location and properties of earthquake source 
and the material between the source and the seismometer to be determined.

* Some examples
* But we deal with anisotropy
* seismic waves propagate at different speeds in different directions
* and with three (rather than the familiar two) velocities 
* analysis using seismic anisotropy can give much more information 
about the medium (examples)
* but is more complex

Why build MSAT:

* already had much code
* but versions used by different people were tending to get out of sync
* e.g. two students fixing the same problem
* and the documentation quality was mixed
* so we brought the code together (and added some new features).
* in the process we
** created a predictable API
** put everything under version control
** wrote documentation
** developed an automated test suite
** tried to make the code more robust (asserts etc)

This turned out to be a lot of work, but gave a boost to our productivity and 
(if the citation rate is anything to go by) the productivity of other groups.

During this process we think we learned something about testing

## A first test case

Illustrate with Backus averaging of a stack of isotropic layers.

* Initially we can think about rays going normal to the layers, this is 
implies that the stress in each layer is constant and we have Voigt (check)
avarage of $C_{33}$. This is our first test (and deserves a Figure)
* We also have an argument about symmetry, must be hexagonal. This is our
second test.
* But even together this is not enough - how can we go further?
* Point out that the literature is a good source of tests and these
tests have a special place in confirming scientific reproducibility.
* Argue that "good enough" in this context is sufficiently good to 
reproduce the published work, given the precision of the reported results.

## Building a library of tests 

* Make the point that it is valuable to include tests for all published
examples, not just a subset of them. Note that not doing this has caught
us out. 
* Illustrate this with an example, probably using tensor decomposition 
of Browaeys and Chevrot [3].
* Sometimes test cases are of exactly the same algorithm - e.g. making
MS_phasevels go more quickly
* Here we can be more strict with our tolerances - and we are approaching 
the ream of numerical analysis - which is outside the main thrust of this chapter
* But we should note that these tests should be distinct
* Other times we have analytical solutions of simple cases, but again this is 
outside the main thrust of the argument

## Defensive programming

* Comment on the fact that this is not the only way we test MSAT.
* We need to include tests and other code to help maintain high 
standards of software engineering (e.g. fails gracefully if provided 
with invalid data).
* But these test case are generally ease to think about
* And are (to some extent) orthogonal to the scientific problem

## Lessons

* Being able to reproduce previous results is a key part of science
* Tests can automate the process of checking that our code still does 
this.
* Previous published work is a key source of such tests
* But, often, the precision given in this previous work is limited (this
is especially true for older publications, where computational limitations 
were important). Although this can be all we have.
* When turning this previous work into tests, it is valuable to turn all
published results into test cases.
* Sometimes these tests do not come from the first presentation of the 
approach, but from some later use.
* Always include commentary with the test outlining where it comes from
and what it is for - just like for functions - especially where the source of the 
test and the original method differ
* Remember that these are not the only tests code should have, but we
argue that this sort of test case should have a special place in the scientific
method.


[^1] https://github.com/andreww/MSAT
[^2] http://dx.doi.org/10.1016/j.cageo.2012.05.031
[^3] http://dx.doi.org/10.1111/j.1365-246X.2004.02415.x

