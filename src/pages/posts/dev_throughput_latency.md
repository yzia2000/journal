---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
  import Cool from '../../components/Author.astro'
title: Throughput vs Latency applied to Engineers
publishDate: 28 July 2022
name: Mohammad Yousuf Minhaj Zia
value: 128
description: How can devs maximize impact?
---

<Cool name={frontmatter.name} href="https://github.com/yzia2000" client:load />

The data and compute argument for throughput and latency is well known. You
optimize throughput if your SLAs are flexible enough to sacrifice latency at
the benefit of greater overall volume of work down. You optimize latency if you
are willing to sacrifice volume of work done but at the benefit of near
real-time processing of each individual request which is especially apparent in
low traffic jobs. I have heard countless say that throughput is more valuable
in most scenarios as most people do not need that latency and the perills of
scaling a low latency low throughput system is no joke. Regardless, this debate
is usually the first example people give in the technology domain for tradeoffs
especially around performance. But this post is not about performance of
compute or data systems. These days I have been thinking about the relevance
of this argument but when optimizing our performance/impact as devs instead.

The thing that sparked this internal discussion was scope creeping and how great
of a planning strategy it is. Let's say I have a bunch of feature work, technical debt and bug fixes
planned this quarter which would equate to 10 units of work. I could create 1 Jira
card for each of these units of work to follow the policy of equitable breakdown. An
interesting discussion can be formed over how I deal with these cards. Do I deal with
them 1 at a time, creating a single pull request for each of them? Do I combine
all the coherent feature work into 1 PR? Is there any scope of combining tasks which
do not appear coherent on the surface at all?

Let's look at the cost factor here. Creating 1 PR for each unit of work is a
strategy. But you incur the latency cost of context switching as well as the CI/CD,
code review request-response. What I have tried very frequently is
combining coherent feature work together in a PR, combining coherent technical
debt together in another PR and fixing as many coherent bugs as possible in
another PR. This proved to be a great experience because I often observed
myself and those who do it this way push out an entire feature consisting
of multiple units of work together almost immediately. Just like in caching,
locality plays a great role here when doing bug fixing and making design
changes as only a single PR will need to change and no downstream dependencies/PRs
will be impacted. I can send this PR for code review and I am getting more
LoC code reviewed in a batch without the reviewer having to context switch
multiple times. As a reviewer myself, I find commit-wise breakdown to be much
more valuable that PR-wise breakdown anyway. All in all, compared to the
previous approach of 1 MR per unit of work, there is certainly potential
for greater impact and quicker deployments. There is another side
to this argument which is that you could possibly distribute the task
amongst more devs such that more devs are working on the same feature. However,
I have more than often seen there being dependencies, blockers and just chaos
in general when using this strategy. You could try your best to distribute
work such that the coupling between tasks that your team is working
on is not high but you are bound to make mistakes and the benefits of
this perceived parallelism will sometimes outweigh the costs (just like
parallelism in computing). I am almost convinced that maximizing throughput
here and combining more tasks (batching) is often better than finely
splitting in most scenarios. However, doing too much batching incurs
a separate cost here too. There is the discussion about bus factor and also when you
deploy too much work together, you are opening
your system to entropy. Too much change coupled together means that an issue
in one commit cannot be rolled back (you can split commits finely but you
are bound to fail at some point).

The above conversation is not very eye opening and often implicit. The
meat of the argument is how to batch and how much to batch. After
entering a team that works on core infrastructure services, the volume
of tech debts and refactors has increased drastically. What I am now
going to start experimenting with is aggressively combining
tech debts and bug fixes with feature work, drawing and catching as
many similarities and patterns as possible. I have also heard
many senior engineers talk about not creating any tech debt Jira cards
in the first place which I find incredibly amusing. If you are working
in a team that always tries to optimize for impact with every task
they are taking, fixing the most debts, implementing the most features
while making sure the issues of coherence and coupling don't kick in;
imagine the impact this team will create. Instead of implicitly batching
tasks together without deeply internalizing things, I will strive to explicitly
scope creep efficiently and observe the increase/decrease in impact I am
producing to the business. I strongly feel leads and managers can find space in
this conversation to provide and derive greater insights for team growth.

Previously, I would enjoy the thrill of context switching between
several incoherent tasks and working on several small tasks during a sprint. Pretty
much optimizing latency over throughput. The high of closing different small
Jira cards is incomparable and I feel its easy to get addicted to quick wins,
more PRs, more cards amongst others but at the end of the day, am I truly that
much more impactful? Do my managers feel that I am more impact if I do things
this way? Is it important for me to show that I am doing more work when in
actuality my overall impact to the business could be much higher if I optimized
things differently?

At the end of it all, I find how humans can themselves fall under
circumstances of the systems they create fascinating. Am I right in thinking
that throughput will usually win, eventhough I might sacrifice the time
it takes to get a unit of work out there?
