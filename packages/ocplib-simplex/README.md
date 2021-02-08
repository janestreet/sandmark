# ocplib-simplex

A library implementing a simplex algorithm, in a functional style, for
solving systems of linear inequalities and optimizing linear objective
functions


## Overview

`ocplib-simplex` is a (fully) functional OCaml implementation of the
simplex algorithm for solving systems of linear inequalities. The
implementation is incremental and backtrackable. It is able to extract
unsat-cores for unsatisfiable problems. Versions `> 0.1` also support
linear optimization


## Dependencies

`ocplib-simplex` requires `4.01.0` or higher and `ocamlfind`.
You can use `make opam-deps` to install dependencies in the current switch.


## Build and Install Instructions

The easiest way to install ocplib-simplex is to use OPAM:

    $ opam install ocplib-simplex

If you want to install ocplib-simplex from sources, use the following
instructions:

    $ autoconf (if configure is not present)
    $ ./configure
    $ make opam-deps (if you are using OPAM and some deps are missing)
    $ make
    $ make install

to compile and install `ocplib-simplex` on your system. You can
uninstall the library with `make uninstall`.


## Minimal Examples

Solving a system of linear inequalities: see the file `tests/standalone_minimal.ml`

Linear optimization: see the file `tests/standalone_minimal_maximization.ml`


## Contributing

Don't hesitate to report encountered bugs on this Git repo's issues
tracker.

## TODO

- the code is not (well) documented,

- some parts of the code need factorization/simplification,

- some invariants (check unsat-core, linear optimization) are missing.


## Licensing

`ocplib-simplex` is Copyright (C) --- OCamlPro.  it is distributed
under the terms of the GNU Lesser General Public License (LGPL)
version 2.1 (see LICENSE file for more details).