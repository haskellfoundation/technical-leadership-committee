# Josh's TLC Manifesto

Haskell presents itself as a strong general-purpose language, suitable for expressing constraints and invariants in syntax that other languages must supplement with rigorous external testing. When human authors are guided by algebraic reasoning and supported by an ecosystem that respects algebraic laws, Haskell programs can come close to being correct by construction. Do these properties still matter in an era where humans are moving more and more out of the loop?

I think this is one of the most pertinent questions we face right now. GHC's own [contribution guidelines](https://gitlab.haskell.org/ghc/ghc/-/wikis/contributing/AI) already accept LLM-assisted patches, with the proviso that humans remain in the loop _and_ understand their output. What core tenets should we adopt to ensure that Haskell remains accessible to human practitioners while also improving the feedback loop between humans and their coding agents?

Here are five tenets that I think the TLC can support with its unified voice and its ability to fund work on proposals. They're aimed at human Haskellers first, but I think each of them helps coding agents too.

## 1. Push the philosophy of Haskell as a host language for embedded DSLs

Newcomers to Haskell will no doubt be overwhelmed by the sheer freedom of expression, and LLMs will push them towards code that is not idiomatic (e.g. rote translations of imperative algorithms vs. building an intuition through equational reasoning).

We can promote humans as the authors of their own mini-languages, explicating the techniques and Haskell folklore that allow us to build embedded languages that come closer to being correct by construction.

I'd support proposals that make this side of Haskell easier to learn and use. One example is a curated eDSL guide: the techniques for building embedded languages, paired with libraries that use them well. It would help human users write their own eDSLs, retaining some autonomy and moving toward more advanced Haskell techniques, and it would give coding agents better patterns to follow than generic code. It doesn't need new technology, but it does need expert input - today this knowledge is scattered across the internet on blogs, mailing lists, forums, etc.

We should also encourage GHC features that further empower this approach. But I think the main issue here isn't a lack of features but a lack of discoverability.

## 2. Fill gaps in the ecosystem

Haskell will fall out of favor quickly if it cannot be used to write secure software. We need to continue to fund work to integrate security into tooling and to build modern cryptographic libraries. We should encourage new library proposals, even ambitious and broad ones, as long as they start as a fundable prototype rather than a multi-year commitment. We should also find funding to continue current endeavors such as the [Botan bindings](https://github.com/haskell-cryptography/botan). My own work on the Arbiter job queue framework is a small step toward filling these gaps. Haskell has several job queue libraries, but none has the feature set we find in other languages (Hatchet, River, Oban, Hangfire, Sidekiq, the list goes on and on...).

Honorable mentions to Ian Duncan's work on [wireform](https://github.com/iand675/wireform-) and [hs-opentelemetry](https://github.com/iand675/hs-opentelemetry), the latter of which many industrial users now rely on. Even a native durable execution framework in Haskell could bring more industrial users into the fold. Suffice it to say, we still need good, safe libraries. Agents benefit from them as well.

## 3. Supply-chain trust and reproducibility

Many people take Stackage for granted, but its absence would be felt immediately. A common misconception is that Stackage is just a curated set of package versions. But snapshots pin every package by content hash, so a build against a snapshot resolves to the same sources everywhere. That is a strong mitigation against supply-chain attacks, and cabal/Hackage users should be able to get the same guarantees without much effort. Today, Stackage's `cabal.config` export only carries version constraints, not the hashes, so cabal users get the curated set without the pinning. We should fix that, instead of telling everyone who wants reproducible builds to use Nix.

Stackage's model could also lead to an audit-driven trust registry: a curated set of packages vetted by humans and marked safe, instead of relying on package authors alone. See [`cargo vet`](https://mozilla.github.io/cargo-vet/index.html) for an example from the Rust community. A vetted package set would also be a sensible boundary for coding agents to work within.

## 4. Production tooling

Production tooling has come a long way in the last decade, but much of what exists comes from Well-Typed's tools and write-ups, and the knowledge is scattered. Sanctioning and/or building tools for monitoring live GHC programs is crucial. It helps the feedback loop too, since humans and agents both need to see what a program is doing in production. If GHC needs features to accommodate this then we should fund that work. I would love it if we could finish what was started with the [Haskell Optimization Handbook](https://haskell.foundation/hs-opt-handbook.github.io/).

## 5. Faster builds

Slow builds hurt the feedback loop more directly than anything else, whether it's a human waiting on CI or an agent that iterates by compiling. The TLC can't fund a rewrite of GHC's pipeline, but it can fund the practical work: finding out where build time actually goes in real codebases, improving recompilation avoidance, and making the fast options the defaults. Longer term, I'd like to see a public, signed binary cache for Haskell libraries, so a fresh machine or CI runner doesn't have to rebuild its entire dependency tree.

## Where I stand

My main focus is on community and ecosystem. Everyone depends on GHC, and I'll support the work needed to keep it healthy, but in my experience its feature set has been more than sufficient to build long-term, stable software systems. I am less interested in pushing state-of-the-art PLT into Haskell. Haskell's unofficial motto is to "avoid (success at all costs)", and I agree we shouldn't compromise what makes Haskell good. But I'd like us to lean into success, and I believe we can find the solutions to support the added weight of its increasing popularity.
