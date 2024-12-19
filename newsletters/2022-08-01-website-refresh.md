---
title: Website refresh
slug: website-refresh
link: /newsletter/website-refresh
isoDate: 2022-08-01T16:00:22.368Z
contentSnippet: What is it you say you do here?
content: What is it you say you do here?
thumbnail: >-
  https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/3383a269-ff46-4981-ffd3-6320a2385000/width=1200,format=auto
pubDate: "Mon, Aug 1, 2022, 4:00:22 PM UTC"
---

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/168ed6c1-b7d0-43d2-6ab9-1427bc46e000/width=1200,format=auto)

Refreshed abouthalf.com for 2022

The previous version of my website was a running 4-year archive of an art experiment I was running on Instagram. Instead of just posting pictures like a normal person, I cut up very large images into small squares, and posted each one individually. A single post might come across like a detail, might be an interesting abstraction, or might not make any sense at all. But viewed together, my Instagram profile was one long continuous stream of images, each bleeding into the next.

Below is a sample from the website:

![](https://imagedelivery.net/oZs0WTb3giZ46YUUQdHDjQ/6b6e860e-c430-42a0-a902-080b6a740300/public)

Long site is long

Instagram only lets you post pictures and videos, but on the website, I would mix in some interactive features. Clicking on an image “tile” would “depress” the image into the screen. Some of the images had draggable components. Each “section” had a title, date, and description and could be viewed on a stand-alone page.

This was fun and creatively engaging for a time, but I grew tired of the project and more tired of futzing with Instagram.

Instagram used to be a fun place to share photos and short videos with your friends. Today it’s Meta’s desperate attempt to chase whatever social media trend seems to be popular with the youths. It’s stories! It’s shopping! It’s video! It’s more algorithmic content!

The result is that Instagram is basically awful and I don’t really like using it much any more. I also decided I didn’t like “feeding” the beast much anymore. These days I’ll still post a new painting, but otherwise I’m focusing on my newsletters.

The other problem my old website was that it didn’t _do_ anything. It was an art project but it wasn’t doing the job of communicating who I am or what I do. How do you shove a portfolio into another art project?

It seemed like a good time to start fresh. I am old-fashioned web designer. I started with a sketch.

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/980f1bdd-073e-4b19-f5c1-ab0874f9a300/width=1200,format=auto)

This collection of scrawled blocks represented the major hierarchies of information I wanted to communicate.

- Who am I?
- What do I make?
- What do I think?
- What’s my background?

From here I moved into Sketch.app to figure out my visual language.

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/0471d997-ee40-4d24-3779-0a8d84f88900/width=1200,format=auto)

I wanted artwork and writing to be the focus, so I spent most of my time thinking about typography. I looked hard at using Helvetica and Noto but settled back into using [IBM Plex](https://www.ibm.com/plex/) as my typeface. I used the serif version of IBM Plex for titles and small bits of copy on the previous version of the site. The sans-serif felt right for me here. It’s distinctive with small flourishes on lowercase “l” and “t” which help readability but also soften the overall visual effect of the type.

I chose one simple visual effect to start - the opening title of the site would mask a photograph, in this case poppies, so a hint of my snapshot-aesthetic would come through the type, but not be overwhelming.

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/b7d4d9f5-c0c3-4a05-a010-7abbd2667c00/width=1200,format=auto)

Later I realized I could have some more fun with it by adding several photos and many silly little quips which change at random.

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/246679f4-a7e9-4de6-d5c1-77468f871f00/width=1200,format=auto)

The portfolio is a simple carousel showing art works in reverse chronological order. Some day I will need to limit the number of recent works, and follow with a “see all” link to show the rest. But for now, this works great.

The content of the portfolio is powered by an [AirTable](https://airtable.com) integration. AirTable is, basically, a web-based database platform - though this is an oversimplification. It’s a very powerful tool.

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/8a7b8216-9999-4621-3e71-89a6ba314d00/width=1200,format=auto)

I created the above database to keep track of my finished art work. I have photos, date complete, title, media, who has it, where is it, etc. AirTable has great developer API. I wrote a small script to pull down all my portfolio content, including images, and format into a simple JSON file for integration into the site.

![](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/50cbc4cb-f20d-454a-3373-9e5773ea9900/width=1200,format=auto)

In order to showcase my writing wrote a small script to read the latest entries from my [Substack](https://abouthalf.substack.com) RSS feed, download the thumbnail images, and display the last 10 on the page.

With that, I could follow up with a simple update of my “about” page with cleaned up copy, a little self-portrait, and links out to social media networks.

This revision feels fresher and feels like it can do a better job of answering the question “who is this guy?”.

The site is written with [ReactJS](https://reactjs.org) and [NextJS](https://nextjs.org) for server-side rendering and hosted at [Netlify](https://www.netlify.com).

[Visit abouthalf.com](https://abouthalf.com)

What to do with the old site? I still _like_ that project. I think it was fun. I archived the original on GitHub. I think I should spend a little time cleaning up the code, making sure things are up to date, and hosting it as a stand-alone art project. Then I can add it to my portfolio.
