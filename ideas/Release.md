Release 0.4
===========

Graphical value pickers for interactively tweaking shape parameters.
* `parametric` constructs a parametric shape, with named parameters
  that are bound to value-picker types.
* HUD (head up display) overlays the value picker GUI on top of the
  shape displayed in the Viewer window.

Contributed features:
* @gsohler: lib.blend
* @tlc123: new keyboard viewer controls
* @s-ol: REPL autocomplete, REPL syntax colouring

Language changes:
* New features used to construct parametric shapes:
  * Parametric records (constructed by `parametric`) remember how they were
    constructed by storing metadata.
  * Picker predicates specify a value picker type & its configuration.
  * Predicate assertion patterns associate a predicate function with a variable.
    Syntax is `name :: predicate`, eg `pi :: is_num = 3.1416`.
    Can be used to associate a "type" with a variable definition or function
    parameter, or to associate a picker predicate with a shape parameter.
* Imperative programming
  * generalized `:=` (assignment statement) works on all local variables
    defined using `let`, `where`, `for`
  * `var` definitions are deprecated
  * generalized `do` works in list/record/string comprehensions
  * generalized `while` works in list/record/string comprehensions
* String literals
  * multi-line string literals
  * new character names: dol, quot, tab
  * string comprehensions using ${...}
  * $. $= ($$ and "" escapes removed)
* predicate assertion patterns and expressions using ::
  * 'pred pat' pattern removed.
* `where` operator is now higher precedence than `,` or `;`.
  `a = b where (bindings)` is now legal syntax, is equivalent to
  `a = (b where (bindings))`.
* Parametric records (constructed by `parametric`) remember how they were
  constructed, by storing metadata (`constructor` and `argument` fields).
  When a record value is called like a function, first try `call` field,
  then try `constructor` field.
* calls to `error` now appear in stack trace

Shape Library:
* lib.blend
* `cylinder` with no argument is `cylinder{d:2,h:2}`.
* `box` with no argument defaults to `box[2,2,2]`.

Geometry Compiler:
* Experimental support for 1D and 2D arrays of numbers and vectors
* polymorphic == and != (works on vectors and bools now)
* a primitive code optimizer
* `-o frag` file format replaced by `-o gpu`.
  This is a human readable data file that contains the output of the
  Geometry Compiler. This feature is for debugging and developing the
  geometry compiler, and the file format is subject to change.
  The `curv` tool can now also read GPU files, display them in the Viewer,
  and you can live edit them.

Other changes:
* Curv now requires OpenGL 3.3
* `curvc` is a new statically linked executable that provides a JSON API for
  running Curv programs. It's for @sebastien's Web GUI work, and may be
  replaced in the future by a webassembly executable.
* fix bug in `-o json` (escaping of control characters in string literals)
* can export empty/infinite 2D shapes as PNG (defaults to Viewer behaviour)
* use `make uninstall` to uninstall Curv
* all Curv library files are now stored under /usr/local/lib/curv