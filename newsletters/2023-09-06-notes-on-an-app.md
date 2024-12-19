---
title: Notes on an app
slug: notes-on-an-app
link: /newsletter/notes-on-an-app
isoDate: 2023-09-06T16:00:17.418Z
contentSnippet: Software is made of compromises
content: Software is made of compromises
thumbnail: >-
  https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/27002875-5944-4b20-c38e-721eb3112600/width=1200,format=auto
pubDate: "Wed, Sep 6, 2023, 4:00:17 PM UTC"
---

![Graffiti reading "RIP Mover" spray painted on an alley wall.](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/02273490-dcb5-44cb-091f-14cd71466e00/width=1200,format=auto "Graffiti reading “RIP Mover” spray painted on an alley wall.")

RIP my weekend

The client wants a native mobile app. They have creative, content, and a budget.

We have a team of web developers, not native app developers. What’s the difference? Web developers are (often) affordable generalists. Native app developers are (often) expensive specialists. You have to be building and maintaining a lot of apps to justify the salary of a decent native app developer[1](#footnote-1).

A web developer can do a little email development, they can patch up that API, and they can maybe help to figure out how to automate that process you hate. The code may be less elegant, but it will work and you’ll be happy. Many shops prefer to hire general-purpose web developers who can do lots of things pretty OK. I know I do.

To solve this problem of too few app developers but plenty of web developers, teams of smart people invented toolkits and frameworks which transform your web developer code into native application code. These are _metaframeworks_ - software development frameworks which manage other software development frameworks.

These metaframeworks promise to let your web developers write code they are familiar with and then deliver a native mobile application in the end. It’s fast. It’s easy. We _promise._ We choose a metaframework[2](#footnote-2).

A brilliant developer builds the majority of the app. The app has complex needs. The code the developer have written is complex…and inscrutable.

The app ships, the client is happy.

The new guy takes over (hi!). He pores over the inscrutable code, taking notes, adding comments, making the unknowable known, but confusing. A qualified improvement.

The client wants another app. This new app has the same job as the previous app, but for a different audience.

We carve common code out of the old app and share it as a library. We build the new app with the common code. We add new features. We enhance old features. We ship. The client is happy. Time passes.

There is no budget for maintenance. We cannot assign a developer to tend to the app like a garden. We get the app into a stable state. We cross our fingers.

Time passes. The apps work. The client is happy. Google is not. Google is upset. Google is upset that’s we are not using version 33 or higher of their software development kit. Remember that we are using a software development kit _which_ _uses_ Google’s software development kit, a metaframework.

Google is sending us angry emails telling us that we need to upgrade or else bad things might happen. You’ve got a nice app here, it’d be a shame if something happened to it.

We try to upgrade the apps to use the latest version of the metaframework, so that we are in turn, using Google’s minimum preferred framework.

It goes poorly.

Sometimes you can just update the various software libraries you use, tweak a few things, turn a few knobs, and you’re good to go. This time, though, the authors of the metaframework have made _decisions._ They no longer want to it _that_ way, but instead _this_ way. The metaframework uses an another framework behind the scenes. That framework’s authors have also _made decisions_. They used to think _one way_, now they think _another_.

Nothing works.

Decisions that the original brilliant developer made are now harshly scrutinized. Choices they made are no longer viable. Some code must be replaced, some must be rewritten. One library is dead and no longer maintained. The code is exhumed from the ashes, brushed off, and turned into a local dependency. _Risky_. But there is no time for a rewrite.

The original promise of this metaframework: “Use our tool. It’s faster and easier to build an app.” This is true.  However, it is not easier to _own and maintain_ an app.

During this upgrade process it became apparent that the only way forward was to start over with a fresh build from a newer version of the framework and slowly copy over old code, replacing bits as needed. Upgrade became _rebuild_.

This happens…not every time, but almost.

This is the compromise we unknowingly made. We chose fast execution in exchange for a higher total cost of ownership. Easy to make, hard to keep.

[1](#footnote-anchor-1)

Or perhaps one very big app.

[2](#footnote-anchor-2)

It rhymes with “redact frustrative”
