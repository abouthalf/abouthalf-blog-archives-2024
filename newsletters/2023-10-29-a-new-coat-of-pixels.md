---
title: A new coat of pixels
slug: a-new-coat-of-pixels
link: /newsletter/a-new-coat-of-pixels
isoDate: 2023-10-29T18:30:10.458Z
contentSnippet: "Thinking technically, minimally"
content: "Thinking technically, minimally"
thumbnail: >-
    https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/520fff19-3b3e-4775-f216-e0bf1f014600/width=1200,format=auto
pubDate: "Sun, Oct 29, 2023, 6:30:10 PM UTC"
---

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/cdf41679-f7a4-46e4-0213-18df1cbf4400/width=1200,format=auto)

[Check it out](https://www.abouthalf.com)

I was interested in learning more about the up-and-coming web framework [Astro](https://astro.build). I decided to rebuild my [personal website](https://www.abouthalf.com) using the framework. This proved to be a good method for learning. My website is pretty lean and simple, so it wasn’t a daunting task to rewrite. Since I chose not to change anything (beyond some clean up and refinements) I had a very clear goal: Make it work and look like the live site. This also gave me the opportunity to do direct comparisons between NextJS and Astro.

I worked on this tiny project about an hour a day for a week, converting one small chunk of the site at a time each morning before breakfast.

Astro builds upon conventions established by other front-end web development frameworks making it quick to understand core concepts.

My previous web framework choice, [NextJS](https://nextjs.org), is a so-called ‘meta-framework’ in that it is a framework which enhances another framework called [React](https://react.dev).

React’s job is to create a user interface system which _reacts_ to user input. React was originally written for Facebook. The Facebook web app is a deluge of rapidly updating newsfeeds, reactions on posts, alerts, messages, and whatnot. The page needs to _react_ quickly to a rapidly changing data.

NextJS bundles React up with a web server, a renderer (which generates HTML on demand), and a router (which connects pages together on the site). NextJS makes React a “full stack” tool - allowing you to build search-engine-friendly websites that are also highly interactive. It’s a good compromise between traditional server generated websites and single-page applications. Years ago, at a previous job, I selected NextJS as a replacement for ASP.Net. We were able to quickly replace large portions of a giant site with small NextJS sites that could run and scale independently. It worked well.

I started learning about React about 10 years ago. At that time web browsers were still a _mess_. Google’s Chrome had become the dominant browser on the desktop, but Apple’s Safari had a giant share of mobile web traffic. In corporate settings Microsoft’s Internet Explorer was still king. At this time these three browsers worked _differently_ - Safari and Chrome were pretty much in sync (though not always). However, Internet Explorer had _different ideas_ about how a web browser should work. A lot of my expertise and my habits toward [defensive programming](https://en.wikipedia.org/wiki/Defensive_programming) was built from wrestling with browser inconsistencies.

This meant that one of the critical jobs React performed was to wallpaper over all the inconsistencies between these different browsers and create a normalized, reliable, and reasonably fast abstraction layer atop the browser.

React was so successful at this, that it went on to create other systems for building native applications on mobile and desktop, emails, command line applications, and even programmatically create video.

10 years is a long time on the web. Since that time, Internet Explorer was finally, officially, killed and other browser authors have standardized very well. Automatically self-updating browsers now adopt new web features multiple times a year, instead of waiting for a major operating system update. Web development is no longer a compromise between compromised platforms. It’s reasonably consistent, stable, and reliable.

Beyond making it easier to work across broken browsers, React also helped usher in the modern, modular, component driven method of building websites. Instead of creating big, long, flowing page templates (maybe with a reusable header and footer), React encourages breaking sites down into small reusable parts which can be Lego-bricked together into a functioning web site.

This has led to different design thinking as well. Designers create design systems (which specify the modular parts) instead of designing each web page like a poster. (If your designers aren’t doing this, get new designers.)

This approach and thinking has grown beyond React and has become more or less the standard way of thinking about web development.

---

I’ve been thinking a lot recently about what comes next, after React.

React (and Vue, and other major web frameworks) all include a “runtime” - a software application written in JavaScript which is loaded atop your website and enables all of your interactivity, animations, effects, and features. The runtime sometimes enhances but mostly replaces built-in browser functionality. The runtime is included along with any custom code that you write.

For a site written with NextJS, that means that the site must include React, ReactDOM (for manipulating the web page), and NextJS (router and other features).

For a very interactive web application, this is an acceptable trade-off. For my very simple site, it feels heavy-handed. I think this may be true for many websites.

Astro takes a different approach. Astro has a component model like React and others, and allows you to integrate and bundle interactive features, but it only bundles in the JavaScript features you explicitly include.

There’s no router, no runtime, none of these things, unless you need or want them.

I was able to recreate the modular construction of my site while cutting the HTML download size in half[1](#footnote-1). I have some minimal interactivity on my site (click around on random things) but Astro delivered only my custom code and the one utility library I needed. This means my site once had about 350kb of JavaScript and now it has 30kb. So my site loads very very quickly on desktop and mobile. It is _instantaneous_.

---

This rebuild had the sort of strange result of getting more done while doing a lot less. By relying upon the browser platform more, I can rely on my frameworks less. My site is minimal as a _product_ - but that’s a matter of choice and taste. I’m excited about minimalism in _process_ and _tools_.

Here the framework made _building_ things easier, and then _got out of the way_. It has me rethinking my approach to lots of things.

[1](#footnote-anchor-1)

NextJS appends a lot of data to each web page. This data is tucked away and invisible, and is used to enable interactivity in the browser. This inclusion is optimistic, assuming that you’ll want to work with that data in some interactive way. On my site, I’m simply displaying information, so the embedded data wasn’t needed. Swapping NextJS for Astro made my HTML payload lighter, because it didn’t include a duplicate of the data already displayed on the page.
