TODO
- [X] intro : assumptions about gradual / migratory typing,
  see jfp19=X oopsla19=? jfp20=? proposal=X
  - [X] hang on, assumptions must go in extra chapter,
        they're not critical for theory work,
        they only set stage for performance ---- again not critical,
        it's just a gradual essay for why we picked this
        chapter2 = why
        chapter1 = what it's all about
        ... maybe DO want that TS Eliot quote to explain the writing experiment
- [X] performance chapter (2), adapt jfp19
- [X] theory chapter (3)
  ... copy JFP, get building, thats all for now
- [X] transient-racket chapter (4)
  - [X] committee update email
  - [X] TR RFC
  - [X] 2020-07-22 : share chap4 outline, diff with first attempt, intro, committee update
  - [X] blame section
  - [X] blame table
  - [X] future work
- [X] full intro (1)
- [X] "both" chapter
- [X] related
- [X] conclusion ... other chapters?
- [X] HEY write the contributions, separate from thesis
      the CONTRIBUTIONS will survive need to applaud them
- [X] "methods" -> "method" goddammit I am the first with these great METHOD canonical,
      you can improve but you will be second (abstract intro conclusion)
- [X] diss to committee
- [X] GTP case study needs work
- [X] sk > I know it's fashionable to say such things at NU, but I'm not sure I agree that "a compiler cannot use optional types to justify transformations".  It certainly can: it just needs to then generate code that guards against using the transformed code.  It's a bit like saying "a JIT cannot use run-time values to justify specializations" — yet that's exactly what a JIT does every day?
- [X] sk PR talk sounds like shallow replacing TR
- [X] jv fig 58 be clear this is fully-typed, explain why; same for all "ratios" tables
- [X] jv fig65 what is timeout and is it worse than deep? explain
- [-] jv try to be clearer that end is shallow without blame ... in figures?
      no, it's fine, future work makes it clear
- [X] jv ack Like types with the Concrete / Erasure switch
- [-] jv isn't this a challenge to explain two behaviors and modes to programmers (yes, we haven't even explained the first!)
- [X] jv what can Shallow do to approximate blame? (keep 1st only, use srcloc instead of id)
- [-] jv remark that Shallow\blame is mitigated by running Deep
- [X] fh typo TS def, chapter 6, mixing lang L with type X
- [X] st benchmarks, new threat, some benchmarks have boundaries that we wrote to contextual modules!!
         alts = consider this as partial lattice with
         ctx attached (is current really the same??!) use unsafe boundary for context port entire library
- [X] st benchmarks, threat, data / structs all in one file
      arose from snake,tetris,zombie arose because of SCV limitations
      what could results be in a ... synth2 ... without the wall
- [X] st fig 48 unclear, use new example, the point is only check at elim forms and
      upcast changes the elim forms
      lazy-fact is bad because it upcasts the result instead of the value
- [X] st p49 wrappers also cause identity problems, the trouble is not only cost and correctness
- [X] st fig 25 does not blame net/url blames interface! double check, get it right
- [X] st fig 26 be clear its the same error as no types whatsoever
- [X] st snake and tetris are both educational and game
- [X] cd "nearby" clarify 'cannot describe designs'
- [X] st sampling, try the worst-case bounds ... what if picked (N slowest) (N fastest) (N slow, N fast)
      ... what are the odds for that?
      2020-12-15 well it can get quite bad, quadU fills the frame
      2020-12-16 ok theres more
      - take5 tetris synth quadU quadT
      - repeatedly take 10 samples of 10*n
      - get average width of intervals, plot on a histogram
      - show committee tomorrow
- [X] st zombie needs more analysis ... what know? what learned?
      our TR data led to simple fixes ... late-neg, struct pred
       but vector contracts = no broad lessons
      call for better tool? (don't say tool, ask about size / number ... cite Grace "almost free")
- [X] st "big" blame, clearer about conclusions,
      (a) basic transient works as expected for TR
      (b) mixing optimal sometimes
      (c) blame bad, useless?
      anyway, the section lesson is NOT how to implement blame for your lang.
- [X] st "big" the lambda-dom checks are a serious model weakness,
      say how to fix ... new language with sequencing , prove simulation
       add to sec 7
- [X] st "big" some intuition for CM ... yes the labels are right but why
      do we care? maybe copy from chap 4
- [X] aa see pdf
- [X] cd fig 46 unclear why checks must be there ... add example?
      also perhaps discuss casts vs checks
- [X] st sec 2 whats the idea here, what inference systems in bounds?
      be clear the goal (stepping stones) ... why else discuss set-based analysis
- [X] st more lisp .... SPCL does typechecking for -> too, but undocumented
      Typed Lisp, by Cartwright 1976 ... copy Sam's dissertation for comments
- [X] st StrongTalk unrelated to lisp, don't remove their history credit
      also they'll use types to optimize when safe
      Hack, similar, has given up
- [X] st remove Pycket from languages picture, it's not a PL, ditto for JFP
- [X] st double-check Strongscript TS* SafeTS for gradual/migratory
      SS = non gradual b/c no implicit coercions to any
           non migratory b/c concrete types
      TS* , SafeTS = ditto
- [X] st double-check ActionScript too, add a version number
- [X] st Monotonic is implemented in Grift and probably TS*
- [X] st Castagna close to Natural, acknowledge it, same for forgetful ... at this point in the paper they're alike
- [X] st canonical forms ... mention in sec 4.3 supports optimization
         put lemmas into 4.6.X ... what do they look like? ditto JFP
- [X] st2 (next page) "ensure ... get-field / send succeed" HEY its not
      succeed , be clear about object members check
- [X] st2 remove (Syntaxof Symbol) too weird
- [X] st2 explain why (All (A) (Box A)) is sound, or give simpler example
- [X] st2 121 say that occurrence types are a general problem, not new to transient
- [X] st2 fig57 are all PR's merged? say so
- [X] st2 5.4 more about experimental conditions ... sw versions, commits (at top)
- [X] st2 fig59 copy to appendix that goes beyond 20x to the worst
- [X] st2 \Gamma_0 -> \Gamma
- [X] st2 sum -> plus
- [X] st2 c6 fig68 put all typing rules in appendix, or here
- [X] st2 rename "Completion" section to "Compilation" be clear that the completing step is an essential part of compiling
- [X] st2 (nearby) bad figures, too far from text
- [X] st2 fig76 add E defenition, we are compatible with respect to E
- [X] st2 (TS def) avoid type U lang U pun .... maybe just say "language" more
- [X] st2 TS add sentence about how to articulate errors (finer context / InvariantErr)
- [X] st2 6.2.1 cite stepping-stones ... You Want When, Advanced Mac., Lang as Lib
- [X] st2 6.2.2 unclear call_f explanation, rewrite
- [X] st2 6.2.3 tu-utils from Neil Toronto, give credit
- [X] st2 fig81 change 42 to symbol, thats what we'd like to allow but overapproximately reject
- [X] st2 xx cite Findler Blume about Any ... least restrictive contract ... any/c vs none/c
- [X] st2 (No Missing Wrappers) cite wrapper-eq papers ... Thiemann, Miller ... search for more
- [X] st2 (External Data) "Deep is eager" major simplification ... refer to TR choices instead
- [X] st2 7.2 vitousek is not whole-program, be clear about their boundary assumption
- [X] st2 7.2 vitousek reports no-jit results, already answers the "jit essential" question
      the wonder is whether non-jit can do so well
- [X] st2 7.3 cite Allende Garcia Tanter about ooplsa ... fortified types ... 
- [X] st2 8 say where quote came from, if anon. survey then fine
- [X] cite Gray etal
- [X] st2 6.3.1 move emails to citations, add title date author, give credit
      "people actually wrote them" instead of simple links
- [X] st2 sec 5.3 fig 51? tr-pipeline, draw forks for transient

- [-] st fig5 colors, pick new ones
- [-] st2 fig65 remove decimals from big numbers (dungeon) try a color scale
          or at least bold for bad ones
- [-] st add Sorbet to figure, gotta check the implementation for parts

- [-] fh review mcallester, kaist, rehof ... think semantic again

- [ ] blame-trail: matthias asked for a handmade bug in acquire that goes 6-7 hops away

- [ ] push MF edits up to JFP

Style
- [X] goddammit typed-color too dark in oopsla-2019/pict
- [X] chapter or section for references? no
- [ ] fig 62+, bad titles for deep vs shallow exact plots
- [ ] shallow/CACHE too big, why are files so huge?
      could zip them
- [ ] hyperlinks broken because scribble labels
- [-] paragraph style looks bad with subsections
- [ ] why not scribble/text ???
- [ ] color-code ideas:
  - sec 2 typed=black, untyped=white
  - sec 3 typed=grey, untyped=white ... moving beyond black/white but not sure yet
  - beyond : multi-color for typed components, depends on semantics
  - apply to figures in BOTH chapter
- [X] print "x" after overheads
- [X] too many exercises, looks like everything has holes, save those for end
- [X] freeze body for exact plots ,,, also they are too wide! reduce max-width by 1 or 2?
- [X] careful about common lisp characterization ... free to ignore, opt non-mand
- [X] start every chapter with acks, papers, people
- [-] MF has boxes around hyperlinks why
- [X] soft typing, remove bullet points
- [X] 2.2.2 still awkward
- [ ] 2.2.3 very awkward ... when do I have time to fix?!

MF edits, leftover
- [ ] (p3) 1 compare sim / dif. in the "two properties" paragraph ... make it stronger
- [ ] (p13) 3 novel configurations in between
- [X] (p14) 3 experience with TR section
- [X] (p45) 3 cache?
- [ ] (p53) 4 think about solid vs dashed arrows
- [ ] (p54) 4 specify error, in fig?
- [X] (p63) 4 how to add dynamic type, orthogonal
- [X] (p64) 4 fix codeblock colors, use "a --" style with label on left at least
- [ ] bring Deep and Shallow into chap 4
- [ ] (p111) 4 conclusion, wrappers vs lambda
- [ ] (p117) 5 move note to end? perf
- [ ] (p119) 5 insert theorem completion correctness ... and a few others
- [X] (p120) 5 better road map .... move integrate blame/Perf explanation
- [X] (p124) 5 how many actions?
- [ ] (p125) 5 correctness, careful
- [X] (p125) 5 Along the way
- [ ] (p129) 5 function clones ... N entry points
- [ ] (p130) 5 "protecting functions ..." gone, is it graceful?
- [X] Q (p132) 5 remove bonus fixes?
- [ ] Q (p148) 6 "not readable" ?
- [X] (p150) 6 redex model
- [ ] (p156) 6 matrix, not rules
- [X] (p157) 6 labeled semantics ... but comes about in CM proof YES really need the labeled semantics
- [X] (p161) 6 labeled red, what symbol?
- [X] (p163) 6 lemmas, explain where needed
- [ ] (p167) 6 why can shallow be aware of deep? articulate benefits
- [ ] 4 move error preorder to bottom row in table 2 --- just like table 1

#### dependencies

racket 7.7 +
python 3.4+
sloccount


#### dear diary

2020-06-18 : need to get moving, spend 2 hours/day or more cmon now
2020-07-09 : we are rolling now, but still way slow progress/hour is pitiful
2020-07-20 : performance and design chapters are imported, need to get serious about transient / data
2020-08-06 : transient data is coming in ... all bugs fixed?
2020-08-12 : transient, waiting on quad, some untypeds way too slow (fsm*)

#### oddball future work

(Q = wrote up as `futurework` question)

- [Q] graduality => errors theorem (icfp 18)
- [Q] natural is a nat. trans.

#### outlines

2020-02-03 :
 Matthias says, the two journal papers will be approx. two chapters so we can
 work those in whenever ready.

2020-05-22 :
 outline attempt
  (why not chronological?)

 0. honest + lying can coexist, thesis ... quest for practical GT
 1. different semantics, which is best? lacking theory + eval landscape
 2. perf eval, applied to TR + Retic (ignore ICFP)
 3. theory eval, for Guarded + Transient + Erasure + compromises
 4. Guarded + Transient
    - why this pair
    - model
    - evaluation
    - other benefits
 5. threats, other concerns (survey)
 6. related work
 7. 

Ben's dissertation outline (2020-05-29):

1. intro, up to thesis,
   contributions that led to thesis
   - perf. evaluation method
     sampling,
     apply to TR, Retic
   - theory analysis
     compromise semantics (TS not enough)
     CM distinguishes honest vs lying
     blame soundness + completeness
   - transient racket (without TR)
     generalize to richer type system (unions, subtyping, ...)
     remove type dynamic
     ... generalize what's needed to insert check?
   - integrating transient + TR
     generalizes smoothly, no surprises
   [[ chapter outline:
      begin with thesis statement (<=1.5 pages),
      short intro to GT, assumptions (migratory vs "gradual"),
      contributions that led to thesis, see above, co-influences,
      chapters outline ]]
2. performance analysis method (goal: fair relative perf, ....)
   - systematic, data collection
     - sampling,
   - visualization
   - apply to TR & retic, validate method
     - suggestion: order of mag. difference, intrinsic!, different shape/curve
     - question: can port transient to racket & reproduce?
3. design analysis method
   - thesis: use standard theory + some new theory to organize design space,
   - tools:
     - parameterized TS
     - complete monitoring
     - blame S + C
   - apply to TR, Retic, Amnesic, Erasure, ....
4. transient racket, implementation (transient + untyped Racket, that's all, can be standalone paper)
   (inherit types + checker from TR but nothing more)
   scale transient to real language, richer type system, 10x gone,
   - theory generalization, to racket types
   - eng. adaptation, to racket lang
   - perf. properties
   - blame, more accessors + manipulators, compromises, huge allocation,
     circularity type at runtime
5. natural + transient + untyped
   (meaning: what are we giving to programmers)
   - simple model
     - no worries, properties still hold
     - failed attempts at natural/transient cooperation to reduce checks,
       possible futures (forgetful)
   - expressiveness
     - (Syntaxof (-> Int Int)) ... new mixed programs that TR doesn't allow
   - implementation
     - require/untyped-contract
     - define-typed/untyped-id
     - ....
   - evaluation
     - ?? 2-way lattice? 3-way
     - ?? programs where mix is better than natural-only or transient-only
     - threats: no blame in transient, 
6. related work soup
   chap 2 - evaluation method
   chap 3 - GTT, KafKa, gradual guarantee?, other analysis
   chap 4 - other impls of transient
   chap 5 - (new)
7. new questions
  - transient + JIT, really fast!? on Pycket, apples-to-apples AOT Racket vs JIT
  - static analysis for transient checks, minimize ala Henglein?
  - transient + blame, practical alternative?
  - need wrappers? forgetful/amnesic instead of transient
8. conclusion
  - summarize chapters, what did
  - revisited fundamental questions (TS, what do types mean at runtime)



