transient-expressive
===

Can transient express new programs?

Well of course. Any code that needed a chaperone at the boundary can be used now.

Is there any wild evidence that this is useful?


### github

Searched for `typed/racket/no-check`, found 900+ results, most are copies of
 the scribble file.

A few looked promising, but no there is nothing here:

- https://github.com/gcrowder/programming-language-classifier
  : Has data files from different PLs

- https://github.com/takikawa/tr-both
  : Experimental language, supposed to have: typed syntax, untyped behavior,
  and optional typed behavior. No-check helps the implementation, don't need
  transient.

- https://github.com/racket/gnats-bugs/blob/7e4bb9a65cd4783bef9936b576c5e06a5da3fb01/all/14821
  : gnats-bug about no-check behavior

- https://github.com/LeifAndersen/experimental-methods-in-pl/
  : goddam another fork of TR


### gitlab

Another search, `typed/racket/no-check`, 0 results.



### mailing list

#### case study, plot

- https://groups.google.com/g/racket-users/c/sRDGG6azTDU/m/-1dE6f85CgAJ
  John Clements, 3d plots unusable after 6.11
  -> plot master  = bit slow, but runs
  -> plot deep    = marginally slower? ... did collapsible help?
     --- defined by swapping `unsafe-provide` with `provide`
  -> plot shallow = gotta convert ENTIRE codebase, but ok
     --- see `transient` branch
  DISCUSSION ... plot3d = from plot-gui-lib,
  = plot3d-frame, returns (Instance Frame%)
    previously hidden via (U (Instance Snip%) Void)
    no contract vs. shape check

[X] TODO try without collapsible, is deep slow?
    ... disable `->-contract-has-collapsible-support?`
    = still quick enough, not fast but not deadly
[ ] try transient-alone again, for minimal number of files
    I really thought this was a wrapper over untyped
    should not need to change entire codebase
[ ] MF suggestion ... try drracket


- https://groups.google.com/g/racket-users/c/ooPDibJC5PM/m/oXB7xYxVBAAJ
  evdubs, sluggish from 7.2 to 7.3
  .... inconclusive whether there is a problem, and no fix committed
  -> plot master  = fine, pretty fast
  -> plot deep    = fine, pretty fast response to mouse actions
     ... if slower, very hard to notice
  -> plot shallow = hey seems faster
    - switching only plot-gui-lib/plot/private/gui/plot3d.rkt is fast too


#### FAIL case study, TR stream

motivation
: https://groups.google.com/g/racket-users/c/1N6bXSQmmHQ/m/m23l2aOvAQAJ

work-around Deep package
: https://github.com/AlexKnauth/typed-racket-stream

can transient avoid the dance between macros and functions?

FAIL, no it cannot, no help. Issue is untyped macro introduces untyped id's
This is a static type-check issue


#### PASS case study, msgpack

https://groups.google.com/g/racket-users/c/6KQxpfMLTn0/m/lil_6qSMDAAJ

"tr lowered my perf."
 narrowed some types from Any
 tanked perf, vector / hash tests slow

type / contract for `pack`
ok, and it's because the input contract wraps mutable data

transient should help!

installed, `make check` ~ 6 minutes
 in particular `raco test test/pack/array.rkt` = 44.34 sec

changed pack types to Any
 `raco test test/pack/array.rkt` = 1.78 sec
 see msgpack/pack-any.diff

changed pack.rkt to Transient
 `raco test test/pack/array.rkt` = 9.48 sec

changed pack.rkt + packable.rkt to Transient
 `raco test test/pack/array.rkt` = 9.60 sec

changed pack.rkt + packable.rkt + ext.rkt to Transient
 `raco test test/pack/array.rkt` = 10.85 sec
 yikes!

changed pack.rkt + packable.rkt + ext.rkt + main.rkt to Transient
 `raco test test/pack/array.rkt` = 9.91 sec

changed ALL to Transient
 `raco test test/pack/array.rkt` = 10.76 sec

changed ALL to Transient + removed cast, weakened types to Any and _Top
 `raco test test/pack/array.rkt` = 2.26 sec
 hmmph guess the cast is the problem

OK TRY AGAIN, is there a case here, keeping the casts?
 yes there is

master
 `raco test test/pack/array.rkt` = 44.68 sec

changed pack.rkt to transient
 `raco test test/pack/array.rkt` = 10.57 sec

changed pack.rkt + main.rkt to transient
 `raco test test/pack/array.rkt` =  9.90 sec

HOW ABOUT ALL TESTS

master ; make setup ; time make check
 make check  319.89s user 6.75s system 94% cpu 5:44.25 total

pack.rkt transient ;  make setup ; time make check
 make check  204.33s user 6.52s system 96% cpu 3:37.97 total
 wow, better but NOT BY MUCH!

ALL transient ;  make setup ; time make check
 make check  202.33s user 8.22s system 81% cpu 4:18.76 total
 hah

ok what if we take sam's fix, no casts? (all Deep)
 make check  117.10s user 5.58s system 96% cpu 2:07.08 total
 I see, well ... is it just a lot of tests in here?

sam's fix, no casts? (all Shallow)
 make check  66.57s user 4.16s system 98% cpu 1:12.03 total)

no casts, only pack.rkt Shallow rest Deep
 make check  101.15s user 4.42s system 97% cpu 1:47.94 total

what about untyped
 make check  24.13s user 3.43s system 97% cpu 28.332 total
 holy crow!


#### FAIL case study, JSON

https://groups.google.com/g/racket-users/c/8YS0vxj4ZBc/m/l1mbb3NnBwAJ

can transient avoid the O(n)? well yes. but is it better after?
too small for a case study, nothing here


#### FAIL case study, quad

https://github.com/mbutterick/quad

oh dear, quad is untyped now .... don't know natural break point


#### case study, prl-website

#### case study, grift

#### case study, phil json validator

https://github.com/philnguyen/json-type-provider

... find data thats expensive
(even with ignored fields?)
... conclude that library better off typed,
    spot-checks for S U,
    usable in T not too slow

- currently unusable in S right? YES, untyped macro used in typed code
- hmph, tried a few configurations and no luck
  transient client
   - t-read t-main s-client = cannot run
   - t-read t-main (unsafe) s-client = ~386 sec
   - t-read s-main s-client = ~290 sec
   - s-read s-main s-client = ~345 sec
   - t-read t-main t-client = ~280 sec
  untyped client
   - t t t u ~ 350 336 334 324 337
   - s s s u ~ 385 380 378 378 383
   - t s s u ~ 353 352 365 340 353
   - t t s u ~ 278 253 276 252 272
  untyped client, bigger data
   - t t o u ~ 2200
   - t s s u ~ 2500
   - s s s u ~ 2600
   - t t t u ~ 2190

fully-typed seems fastest! I think because the parser goes datum-at-a-time,
 so transient ends up double-checking everything

... this library is too good

after parsing there's a boundary, but both shallow and untyped have to deal with it

ok, "custom.rkt" shows a difference for end-to-end parsing using 'json' as-is.



#### 2020-08-18 -- 2017-11-28

150 messages so far,
6 winners

- https://groups.google.com/g/racket-users/c/IKTFoqwQ6yQ/m/vBGhck4TAgAJ
  X : static error, can't occurrence a set! var
- https://groups.google.com/g/racket-users/c/jtmVDFCGL28/m/jwl4hsjtBQAJ
  O : cannot protect opaque value, FIXED by transient
- https://groups.google.com/g/racket-users/c/2X5olKMV3C4/m/mJhsp9ZWBgAJ
  O : inference gets precise type, cast does not forget it, FIXED by transient b/c old type forgotten
- https://groups.google.com/g/racket-users/c/8xkpjpNntRo/m/mexP1a6OBgAJ
  X : need to require/typed vector-sort, suggestion (Vectorof Any) fails even with transient for the particular code
- https://groups.google.com/g/racket-users/c/UD20HadJ9Ec/m/Lmuw0U8mBwAJ
  O : set! has no apparent effect, b/c Deep puts a contract around and that makes a copy! transient = no copy
- https://groups.google.com/g/racket-users/c/JEEuTQc1YjE/m/dobsO63XBwAJ
  X : type cannot contract, contains free variables
- https://groups.google.com/g/racket-users/c/oiFYAxK48Yc/m/Y2mjC-m2AQAJ
  X : trouble expressing polymorphic class, static-only problem
- https://groups.google.com/g/racket-users/c/6lo-duvGX5E/m/c2RDJdKXAQAJ
  X : mutable data, confused about supertypes
- https://groups.google.com/g/racket-users/c/Y7bVyl8sBuc/m/cRu5bufzAAAJ
  X : for macros and immutable vectors
- https://groups.google.com/g/racket-users/c/o8uqVXGFIQ0/m/WDGYFp2NAwAJ
  X : require/typed #:struct, but the library does not export struct
- https://groups.google.com/g/racket-users/c/ZbYRQCy93dY/m/kF_Ek0VvAQAJ
  O : parametric contract changes result, transient avoids
- https://groups.google.com/g/racket-users/c/ZO4tNKOYv74/m/otfia-S7DQAJ
  X : type error, `apply` on function that requires 2 args
- https://groups.google.com/g/racket-users/c/i9jVuzfDGt4/m/Nhk71Z1WBwAJ
  X : syntax error in Racket v6.0 (vs 6.1 and later)
- https://groups.google.com/g/racket-users/c/8YS0vxj4ZBc/m/l1mbb3NnBwAJ
  O : help getting (Listof String) out of a JSExpr union, why O(n) cost, transient does avoid the O(N) up-front cost
- https://groups.google.com/g/racket-users/c/plrpS2ZCWNA/m/trGDdbi-BAAJ
  X : low-level segfault, fixed for 7.4 release
- https://groups.google.com/g/racket-users/c/ozT9sVpfPZE/m/lXm9jkTuCQAJ
  X : about how to use annotations / inst
- https://groups.google.com/g/racket-users/c/BDrrgW0axGQ/m/P31NxeGHAAAJ
  O : require/typed case-> with 2 arity-1 cases, ok for transient
- https://groups.google.com/g/racket-users/c/0tOGWZ9O57c/m/jRXJYkUdAQAJ
  X : for loop, not enough types / unsupported
- https://groups.google.com/g/racket-users/c/79Cm-nyceXE/m/U78Eey0RDwAJ
  X : curry, needs type annotation
- https://groups.google.com/g/racket-users/c/TuHMHdZKhgI/m/x3jAwKtRDgAJ
  X : TR does not do type dispatch
- https://groups.google.com/g/racket-users/c/fSLxP8YW7Mw/m/FV8_UsKdAgAJ
  X : for/fold #:result expansion trouble
- https://groups.google.com/g/racket-users/c/mUOiv9zop70/m/5QT8Fo6pAQAJ
  X : 3 troubles with random, runs ok, usually TR faster than transient,
      orig program : transient < tr, ~30sec
      use positive? : transient > tr, ~30sec
      positive? and c-p-r-g once : transient > tr, ~10sec
      (wow)
- https://groups.google.com/g/racket-users/c/Ma9Fh72gfQg/m/F5v_kdvVBAAJ
  X : typecheck error, poly structs
- https://groups.google.com/g/racket-users/c/tMy9lma7W18/m/iJimGR_OBQAJ
  X : contract for prefab, fixed in later version
- https://groups.google.com/g/racket-users/c/8THiLChLlQg/m/UkwMzqLaCwAJ
  X : type-check succeeds, surprising, but nothing for transient to change
- https://groups.google.com/g/racket-users/c/7hL-zpOdaT0/m/OxQhnGTMBgAJ
  X : type-check surprises
- https://groups.google.com/g/racket-users/c/cCQ6dRNybDg/m/CKXgX1PyBgAJ
  O : any to proc, no "higher order value" problems anymore
- https://groups.google.com/g/racket-users/c/5QKSeAF9ddU/m/P74JrMZVCwAJ
  X : how to make a sequence, resolved on list
- https://groups.google.com/g/racket-users/c/TS-a1XA4_qc/m/5Vd6Ukd7EAAJ
  X : for loop problem, for*/or unsupported?
- https://groups.google.com/g/racket-users/c/Sl7_eoHZFeI/m/KN0WhoVLDAAJ
  X : type check, cannot polymorphic struct at boundary


