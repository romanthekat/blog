---
title: "[2/100] Branches, releases, and how to live with that?"
date: 2020-11-06 
draft: false
---

That's gonna be some thoughts on different git branching models, and how to handle multiple supported versions of an app.


There is a great git branching model: [GitFlow](https://nvie.com/posts/a-successful-git-branching-model/).
It serves well, works nice for tons of different cases.

For some scenarios it can be too complex, thus things like [GitHub Flow](https://guides.github.com/introduction/flow/) or [GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html) were created.
But if always moving forward and frequent deploys are not exactly your case - then git flow works nice.


Let's assume one needs to support and develop several releases, available outside, at the same time.
For example, we can have 2 releases to support: soon to release 1.0, and 1.1 with more features, but later to deliver.

Interesting things happen once there is a desire to work on stabilizing release 1.0 and next features _at the same time_.


Release 1.0 could be started as a branch from develop, accumulating all the things prepared so far.
Assuming we already preparing release 1.1 - we also create release 1.1 branch from develop (or previous release).

As a result we end up with following branches composition:
- develop: most recent, 'integration' branch, must have *all* features/commits ever added to the system
- release/1.0
- release/1.1

Features to implement can be done via short living [feature branches](https://nvie.com/posts/a-successful-git-branching-model/#feature-branches).

#+begin_example TO REMOVE?
It can be good practice to prepare special branches, representing environments solution was deployed to:
- staging: branch for your staging environments, quite the same with production; you can conduct extensive end-to-end checks and demo sessions here
- prod/main: production branch
#+end_example

The problem I don't like - when you add something in release 1.0, how to propagate it to release 1.1?


I see two main approaches for that:
1) Merge immediately in multiple places
Once you create your feature branch `feat-1.0`, and ready to merge it - create several merge/pull requests:
feat-1.0 -> release/1.0
feat-1.0 -> release/1.1 (cherry pick)
...
feat-1.0 -> develop (cherry pick)

The good about it - all changes immediately propagated, none will be lost.

The bad about it - you need to do it. Actually create X merge/pull requests.
You also usually want to remove obsolete feature branch, so you also should do it after last request merged.

Most of the tools atm won't do it automatically (there is an open [issue](https://gitlab.com/gitlab-org/gitlab/-/issues/11648) in GitLab for example).

So you either do it manually, with a risk of making mistakes, or do your own automatization tool for that.


2) Backport releases from time to time
Once you create your feature branch `feat-1.0`, and ready to merge it - merge it. And that's it. The flow for developer working on the feature is simple.

But someone had to backport 1.0 to 1.1, 1.1 to next release, up until develop branch.
You can do it daily, as morning routine for instance.

It's somewhat convenient, simple workflow, but temporary your branches are not in sync.
Extra ~8 hours between propagation can cause you extra merge conflicts, especially if there is a refactoring of any kind happens.


I personally don't enjoy both ways. If it's not automated - it is prone to fail, be forgotten, dependent on manual actions to perform.


First approach can be enhanced with automated pull/merge requests creation, using API for correspondent tool of yours.
Or you can use plain git, and backport in timely manner.


Probably I should write a tool for either option, and give it a proper try
