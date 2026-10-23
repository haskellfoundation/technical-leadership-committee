At a high level, consider two angles: 1. How to make Haskell good for
humans, and 2. How to make it good for AI. Look for areas where we can
improve both.

# 1. Good for humans

My thinking here is influenced mainly by my experience with using
Haskell at a large tech company, which was successful in the sense
that we built a large system that was in production for 10 years,
handled a critical business use case using millions of lines of
Haskell, and was modified by hundreds of engineers. On the other hand,
the system was eventually replaced and Haskell was dropped for various
reasons.

The good parts (that we should lean into):
  * Type safety was key - we deployed code immediately to prod, only
    type safety (and some deploy-time checks) prevented problems.
  * The ability to build flexible & powerful abstractions
  * Runtime performance of Haskell was not the bottleneck, although GC
    was a bit of a headache (see later).

The parts that didn't help:
  * Complexity and unfamiliarity in the language. Engineers who just
    wanted to dive in and make a small change found it hard. Nowadays AI
    will help a lot with this use case, but I found myself constantly
    apologising for unnecessary complexity all over the place.
  * Complexity and unfamiliarity of the compiler and tools. The cost
    of maintaining a compiler toolchain and build system integration
    was proportionally too high.
  * GC performance and latency: this was a constant battle. The
    non-moving GC came later and we never had the chance to try it,
    but the runtime cost would maybe have been too much. Scaling well on
    machines with dozens of cores was quite a challenge, and often the
    GC was the culprit. I have a suggestion for something we could
    work on to address this below.
  * Difficulty of debugging: production problems were very difficult
    to debug and required deep expertise. GHC not working well with
    common tooling (e.g. perf) made it harder.

## What I would like the TLC to do:
  * **Simplify tooling and workflows**
    * decide on a **paved path** and polish that. `ghcup` is wonderful; a
      lot of our other tooling has rough edges though.

  * **Move complexity off the paved path**
    * `GHC20xx` is a good example of the direction I'm keen on: set good
      defaults that cover most use cases and steer users onto the
      paved path. Flexibility still exists for advanced users, but
      there's an easy on-ramp that takes you somewhere useful by
      default.

  * **Streamline/unify documentation**
    * Having the language documentation spread over two places
      (Haskell Report and GHC User's Guide) is a huge problem that
      many of us have forgotten about. I love David Binder's effort to
      produce a new Haskell Report incorporating GHC extensions.

  * **Improve productivity**
    * **Build speed**. There isn't much to be had in optimising GHC, but
      there is a lot of wiggle room in the surrounding build infra:
      less unnecessary work, more parallelism, and more caching.

      My personal view is that throwing more build system stuff into
      Cabal is a losing strategy, instead we should focus on making
      Cabal the front end to a proper build system (e.g. Buck2) and
      use this to build GHC too. Solve multiple problems in one go:
      * GHC builds are too slow and Hadrian is too complex. GHC's CI
        is slow and flaky. Using a build cache would speed up CI a lot.
      * Cabal is too slow, lacks many features and is not a
        general-purpose build system. Hooks are complex and ugly.
      * Cabal and GHC should have the same build system.

    * **Debugging**.
      * I'd support doing anything that improves call stack support so
        we can move away from `HasCallStack`.

    * **Tooling**.
      * HIE files `-fwrite-ide-info` don't support as many use cases
        as they could. For instance, Haddock should be able to consume
        HIE files and be decoupled from the GHC API, but it still has
        to be a GHC front end because HIE lacks the full source code
        AST, at least in a form that can be easily reconstructed by a
        consumer. Another example is [Glean](https://glean.software):
        we can't produce a full source code index in Glean from HIE
        (we use it but it's missing lots of features we'd like to
        have). I would redesign HIE files so that
        1. Haddock can consume them and be independent of GHC
        2. Glean can consume them and produce a rich index
        3. More things can be HIE consumers instead of GHC API
           clients. Something something AI something.

  * **Reduce friction**
    * Upgrades breaking things. GHC upgrades shouldn't need a base bump.
    * Fix bugs that hit common use cases
      * HLS is good but buggy (but is HLS a good investment given that
        a lot of development is moving to AI agents?)

  * **Improve performance**
    * I'd love to have a way to run a thread with its own local heap;
      this could solve many performance problems and is a simple model
      to explain. Several people have explored these ideas, there's
      some discussion in
      https://gitlab.haskell.org/ghc/ghc/-/work_items/21578

  * **Work nicely with other tools and ecosystems**
    * e.g. GHC binaries should work with perf, and you should be able
      to easily get stack traces and flame graphs using standard
      tools.

# 2. Good for AI

I have much less well-formed ideas here and the space is moving really
fast so it's both hard to know what to do now and hard to know what
will be valuable in the future. There's a real danger that we solve
some problem now that turns out not to be a problem in a couple of
month's time. Thoughts:

  * Safety could be super important. It's a shame that Safe Haskell
    didn't achieve critical mass, because AI is precisely the scenario
    where Safe Haskell would be able to help: an untrusted actor
    writing code that we want to run with a controlled set of
    permissions. Should we revive Safe Haskell for this use case?

  * Improving build speed will likely help both AI and humans, so that
    seems like a no brainer.
