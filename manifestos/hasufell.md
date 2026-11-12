# Julian's TLC Manifesto

## Vision

My vision of Haskell is a community and an ecosystem that:

1. allows newcomers to get into Haskell quickly while enjoying its tools and easily finding support
2. is mindful about changes: stability and progress is a delicate balance
3. cares deeply about the craft of software engineering

### 1. The newcomer experience is the benchmark

When trying to understand developer experience and usability we have to first
look at experience reports from newcomers. Seasoned developers and community members
often get used to workarounds and quirks and may become somewhat oblivious to
recurring issues.

If a newcomer can set up the haskell toolchain easily, find resources to learn the
language, join forums and channels to deepen their understanding of concepts and
share their progress to inspire others... then we have succeeded.

Anything that improves the life of a newcomer also improves the life of seasoned
developers: the newcomer experience is the benchmark.

### 2. Balancing stability and progress is our main challenge

Historically, Haskell has been an academic laboratory: a language where
we explore functional programming, laziness, Hindley-Milner, etc.

These roots are incredibly important to the language and the community. It
is why we all ended up here, one way or another.

At the same time Haskell has accidentially become "successful". Companies are using
it for immense codebases and are running into problems we could not have
foreseen (e.g. requiring an entire person year of work to update a GHC version).

These users care about predictability, upgrade cost, support and other things
that maybe did not come naturally with Haskell's roots.

This doesn't simply affect GHC, but also the larger library ecosystem.

We need to continue this work of balancing these concerns in a way that doesn't stack one ad-hoc decision on top of another, but evaluates the impact of each decision
on the ecosystem as a whole.

### 3. Programming is an art and Haskell is beautiful

Haskell was created for humans to express their ideas and thoughts, explore
things as they type and inspire each other.

[Programming is fundamentally an art](https://blog.glyph.im/2026/10/programming-isnt-special.html),
even if it's mostly mundane art (rather than fine art).

I want to work on an ecosystem where it is still fun to write
things by hand and exercise programming as a craft and an art.

As automation is increasing and industry demands are changing I believe that
a core principle that benefits everyone regardless of their workflow is:
"if it's easy to understand and write for a human, it will also be easy for a machine to process".

I see this as an opportunity to bring opposing views together.

Engineering still matters, understanding still matters. And there's
a lot of work to do to build solid engineering foundations for Haskell
that will allow us to express our thoughts more easily and reason about
systems more precisely.

## Priorities

My own priorities are the following, in exactly that order:

1. security
2. Haskell tooling
3. library ecosystem

### Security is going to be a discerning factor

I believe that current changes in the software engineering landscape will cause
massive negative effects for practical security, hosting public facing services
and maintaining a trustworthy supply chain.

For Haskell to stay relevant and be a feasible choice for industry, we need to invest
heavily in security hardening, processes and crypto libraries.

### Haskell tooling

It may be no surprise that this is in my top 3 priorities. GHC, cabal, HLS, stack, ghcup
and new upcoming tools like the haskell debugger have the highest exposure surface. They're
used by newcomers, industry users, CI systems and other automated systems around the clock.

They need to be robust, extensible and follow unix principles, so that new and unforeseen
workflows can be realized without much effort.

Continuing investment in this area is essential as workflows are starting to become more
complex and more automated.

### Library ecosystem

While Haskell has seen an enormous amount of new and exciting libraries, our ecosystem
sometimes struggles with long-term maintenance and robust libraries for boring use cases.

Such efforts need to be supported financially where possible. Our volunteers are precious
and we can't have them burn out.

## Strategy

I believe the right strategy for the TLC is to be:

1. proactive: focus on finding contractors that can do diverse pieces of work and show a track record of success
2. inviting: make it easy for anyone to submit a proposal and ask for funding without much fuss
3. transparent: communicate our vision, goals and capacity clearly to the community and provide progress reports on all proposals

The biggest challenge appears to be our budget. We need to find a way to get small or incremental proposals going
in order to show proof of progress, which then may facilitate further funding. Possible solutions
may involve small bounty programs (to drive long-standing issues forward) or co-sponsoring proposals
with industry.
