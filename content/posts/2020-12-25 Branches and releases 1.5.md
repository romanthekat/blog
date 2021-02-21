---
title: "[14/100] Branches and releases 1.5"
date: 2020-12-25
draft: false
---

One of little details left behind with feature branches - the moment code reaches release.
Popular branching models approach it mainly in two ways:
1) once feature development is finished, and code review passed, one shall merge the feature branch; e.g. merge **before** feature validation 
2) feature branch deployed separately to conduct testing procedures, bugfixes if needed, and only after that you merge the feature branch; e.g. merge **after** feature validation

So it's a tradeoff whether we deploy features faster, or more reliably.

First approach updates codebase rapidly, which can be extra convenient if there are dependent features, or if refactoring happens. But at a cost of possibly unstable code. Last part can be partially mitigated by code freeze and/or starting new release.
This way testing is often conducted on a aggregation of multiple (non-tested) features at the same time.
But the bigger the team - the more features gonna be in such an aggregate, possibly badly interfere with each other. Leaving you with never really stable feature set.

Second approach leads to granular validation: stable code base + 1 feature at a time. 
That means you always have stable release in known state, ready to deploy. Generally it scales better with team size - there are no multiple untested features added simultaneously.

But that requires performing multiple, preferably fast, deploys. Usually having the same amount of environments per features to be tested at the same time.
It's more demanding for configured CI/CD pipelines.

Besides, several features working independently doesn't always work if combined. 
While first approach implies 'immediate' features integration, second requires performing regression testing more often. 

Also, if you have several dependent issues, you usually create separate 'integration' branch, and merge required features there. Which ultimately is the first approach. :)

So it's a tradeoff - you either get codebase updates faster, or more predictable results. 
At the cost of more complex process and somewhat higher testing load.
