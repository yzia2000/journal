---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
  import Cool from '../../components/Author.astro'
title: Chasing glamorous tech
publishDate: 2 July 2022
name: Mohammad Yousuf Minhaj Zia
value: 128
description: I wish I didn't make these mistakes...
---

<Cool name={frontmatter.name} href="https://github.com/yzia2000" client:load />

One mistake that I often regret making is chasing glamorous solutions to simple
problems. I have a ton of these at work or in personal/education projects. Its
not the fact that I chose those solutions because I wanted to experience
working on that piece of technology, purposely make my life harder or boast
about how complicated it is to my peers. It was the planning that went into it
and the execution that was lacking.

Often times with complex solutioning, I often see myself missing corner cases
due to gaps in understanding. If there is a shred of business incentive that is
attached to these projects, you need to take them very seriously. Aim to have a
running implementation or a precedent that would verify your claim before
confirming the solution and proposing it to your product owners. If you are
working with an existing or legacy system have a migration strategy in place
which is doable. Never overpromise or underpromise. I have shown negligence in
these areas on numerous occasions. Quarters are short and you need to really
squeeze as much impact out of them as possible.

Even when you run head-first into these projects and realize that things will
not work out, you will force it and spend more time trying to make things pull
through. This is sunk cost fallacy. If there is incentive in exiting from a
strategy, cut your losses. I have seen myself trying to optimize something
for months, trying to give myself hope and making it a living hell for people
around me.

Another fallacy I see myself often falling into is thinking that complex
projects will be appreciated more than otherwise. This has no basis to it.
The code that I have written and reviewed that has been marked as technical
debt has created the most value over time. It is appreciated by people
because they understand. If you are the only one who knows how a subsystem
works, you best believe that you know it in and out because it is going
to be a lonely hell with many challenging the idea.

Make sure that complexity of the solution match the complexity of the
problem.

Let's look at the bright side though. You learn a lot from this experience.
At the very least, you gain insight into what you should and should not do.
