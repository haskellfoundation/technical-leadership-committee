# The TLC's shared vision

We believe that Haskell is the best programming language out there and that it
can provide unique value to everyone, because it sits at an interesting
intersection between craftsmanship and radical automation:

* It is good for humans to write by hand: Type safety, powerful abstractions
  and referential transparency have enabled engineers all over the world
  in startups and big tech to deliver and maintain complex systems.
* It is good for responsible AI workflows: review is the new bottleneck in
  modern AI-workflows and Haskell's strengths heavily favor the reviewer.
  Additionally, the ability to quickly design eDSLs and express constraints
  where it matters allows to set up strong guardrails for code generation,
  without losing flexibility.

There may be better languages for formal verification or for vibecoding, but
there's no better language for "human in the loop". Haskell is where we
maintain control of our work, build institutional knowledge and ship responsibly.

## Motivation

What drives the TLC is our motivation to improve Haskell for:

1. Beginners: improving the newcomer experience, because it is *the*
   UX benchmark
2. Experts: fixing long-standing pain-points of the Haskell ecosystem
3. Industry: understanding corporate needs and scaling issues

## Priorities

While there are many parts of the ecosystem that need love our current
priorities have crystallized as follows.

### Security

We believe that security needs a new and more focused approach and cannot be
seen as a given. The lack of major incidents is not an indication that our
libraries, systems and infrastructure are secure.

Supply-chain needs to be trustworthy, security processes need to work seamlessly
and end user awareness of vulnerabilities and mitigations needs to come
without effort.

Haskell needs to provide a strong crypto ecosystem and utilize its language
to allow better strategies to harden applications (e.g. through Information Flow Control
and other techniques).

### Tooling and productivity

While the community has made great efforts with tooling in the past few years,
there's still major gaps we need to tackle.

1. Faster iteration: whether it's compilation speed, improving GHCi or implementing
   better caching for build tools... all of these affect both human and machine
   workflows. Faster CI, faster contribution, faster turnaround times.
2. Debugging: an often neglected art, because it's less fun. The ecosystem
   needs to catch up, polish the tools we have, support new tools and
   write documentation and tutorials that make this less of a frustrating
   experience.
3. Onboarding: most Haskell users are beginners! From installation to
   tooling interaction... everything should fit together nicely and not be
   a jigsaw puzzle.

We are further committed to unix principles, which allows tools to be extensible
and empowers the user to realize complex and sometimes unforeseen workflows,
without having to rewrite large parts of the ecosystem.

These things are important as frustration tolerance is in decline (and maybe
rightly so!) and users are more quickly to abandon languages, ecosystems and
tools if they do not accommodate their needs.

### Stability

Moving fast isn't the only thing that matters, however. We also want to invest
in ways to make the Haskell experience pleasant for users, who maintain
large complex systems, who have to upgrade the compiler every year, catch up
with library updates and have deeply ingrained workflows that our tooling
must not disrupt.

This may entail allowing users to opt-out of breaking changes, maintain longer
backport windows for GHC, coordinate ecosystem upgrades better (which often has
been pushed to stackage maintainers) and generally make the ecosystem more
predictable for corporate users.

## A flourishing open source ecosystem

All of the above is an attempt to support the Haskell open source ecosystem
that we love. We are committed to open source, its values and the social
aspect of it. Collaboration is how we engage with and inspire each other.

We want to enable all the maintainers and volunteers who keep this ecosystem
alive, many of them unknown, doing their part on a Saturday evening
at the other end of the world.

## We need your help

In these turbulent times, we ask you to help us.

Send us:

* ideas
* money :)
* feedback

