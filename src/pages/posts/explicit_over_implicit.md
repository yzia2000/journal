---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
  import Cool from '../../components/Author.astro'
title: Explicit behaviour over implicit
publishDate: 3 July 2022
name: Mohammad Yousuf Minhaj Zia
value: 128
description: Abstractions that cost less in the long term
---

<Cool name={frontmatter.name} href="https://github.com/yzia2000" client:load />

I often see myself being at cross-roads with how much implicit behaviour
I should pack into a function, service, module and product. If you are working
with anything related to developer experience or creating core libraries
for devs in your company, I am sure you can relate to this conundrum.

To share an example, this code was written in a Storage service whose first
usecase was to handle profile pic file uploads in a social media application:
```javascript
class StorageService {
    upload(user: User, picture: Picture) {
        // upload above file to s3
        ...
        this.shareWithNetwork(user, 'PICTURE_UPDATED');
    }

}
```

This code served its purpose well but most people can quickly identify that
there is an issue with separation of concerns here. A Storage service
performing social media updates will prevent it from handling other types of
uploads that are unrelated. Later down the line, this code will have to be
rewritten and the concerns will have to be separated. A naive approach to
improving this could be:

```javascript
class StorageService {
    upload(file: File, key: string) {
        ...
    }
}

class ShareService {
    sharePictureUpdated(user: User, picture: Picture) {
        storageService.upload(picture.file, picture.name);
        this.shareWithNetwork(user, 'PICTURE_UPDATED');
    }
}
```

The thing that improved in the above code is that now the StorageService
doesn't implicitly share with network. You have stripped away more implicit
behaviour from the above the code and now it can be reused in more places.

I believe everyone knows about this through different forms of software
engineering priciples like Separation of Concerns, DRY, cohesion, coupling but
I feel these words overcomplicate such a fundamental discussion of implicit
and explicit behaviour. As a random caller of a function, service or product
would you want more things to happen without you knowing or would you rather
dictate the individual pieces?

Believe it or not, I have seen a bunch of people in support of implicit
behaviour and rightly so. For them, it is much better to have sane defaults and
you don't have to worry about recreating things in iterations. A lot of times
people don't even notice that they are violating SoC, cohesion, coupling and
the rest. Yet they create good business value.

However, more than often, I see there being a sudden need that pops up where
all things come crashing down and you do need to rewrite. You realize
those sane defaults and implicit behaviours are not configurable and now
the effort of changing things becomes greater than creating them.

If you were to choose a strategy randomly without much insight into future
requirements, minimize implicit behaviour. Break things down and separate
them. Make sure that things need to be done explicitly. Because the cost
of migration to more implicit behaviour is merely cutting code while
cost of migrating to more explicit behaviour is much higher on average.

The above decisions are easy and seem obvious. But I often see myself and
others not checking if the libraries we are using are built to support explicit
behaviour. Now that is a tough place to be in because you cannot change
libraries and good luck meeting your OKRs while forking, updating and deploying
your version of the library (not to mention the newly incurred cost of
maintainance and being in-sync with upstream).

Another area is product. Now decisions have become a notch harder because
upstream business folks, VPs, product owners, product managers and, most
importantly, customers often want or need that implicit behaviour. The biggest
selling points are automation, unification, taking the complexity away and
handling things end to end. Windows/Mac is more popular than Linux and it will
always be to an end user (not a server). Packing all these things in will incur
a ton of implicit behaviour and customer will enjoy it while things are meeting
there needs. Different companies have different implicit behaviours and there
are different customers with different needs. If your implicit behaviour makes
sense, there will be a customer out there to try your unique solution because
they have a unique need. The name of the game is ensuring the implicit
behaviour, workflows and more broadly UX can meet more customers than just a
selective few. Because there will be a competitor out there whose implicit
behaviour will supercede yours and the rest of the solutions in their kit will
shadow over yours. Though niche markets and solutions are a thing and strategy.

A bonus is to support both implicit and explicit behaviour. A great example for
us devs is Jira. You can drag cards along. Or you can have complicated pieces
of logic and filters to support more custom workflows.

There are no absolutes. Everything here is relative to situation and
requirements but I always keep explicit over implicit in my head than SE jargons.
It is much easier to remain consistent.
