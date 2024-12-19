---
title: Replacing Substack with Astro and Buttondown in 12 easy steps
slug: replacing-substack-with-astro-and-buttondown-in-12-easy-steps
link: /newsletter/replacing-substack-with-astro-and-buttondown-in-12-easy-steps
isoDate: 2024-01-07T01:41:47.508Z
contentSnippet: Replacing Substack with Astro and Buttondown in 12 easy steps
content: Replacing Substack with Astro and Buttondown in 12 easy steps
thumbnail: https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/4e39af8e-45d7-4efc-8b95-9d5097d30f00/width=1200,format=auto
pubDate: "Sun, Jan 7, 2024, 1:41:47 AM UTC"
---

![title](https://abouthalf.com/cdn-cgi/imagedelivery/oZs0WTb3giZ46YUUQdHDjQ/4e39af8e-45d7-4efc-8b95-9d5097d30f00/width=1200,format=auto)

_A bit of a warning up front - this is more than a little bit technical and nerdy. I'm posting this here for the purposes of shring knowledge and helping others who have similar plans and schemes. Fee free to skip it if it's not for you._

---

I recently left Substack behind [(for reasons I wrote about here)](https://abouthalf.com/newsletter/you-cant-un-know-something). I chose to repatriate all of my written content back to my own website, not just spin up another newsletter service.

I wanted to share some details about how I did this. Hopefully it’s useful.

# Recommendations for normal humans

If you’re a Substack user, and you want to leave, I’d recommend [Buttdown](https://buttondown.email/) as an easy alternative. Buttondown imports from Substack and a variety of other sources. It has many of the same features for newsletter authors, but isn’t attempting to become a social network. The free tier is generous and the paid plans are priced fairly.

If you want a more robust website experience, perhaps look into [Wordpress.com](https://wordpress.com). They support newsletters and membership options as well.

I’m a developer, and what I’m about to describe is for other developers.

# What to expect when you export

Substack allows you to export your content. In the account settings area you can schedule an export. You receive an email when it’s complete.

The export file - a zip archive - is retained and downloadable from account settings.

The zip archive contains:

-   Posts (HTML format)
-   Subscriber list (CSV format)
-   Analytical data about posts (CSV format)

The zip archive does not contain:

-   Post images
-   Social media images (thumbnails) for posts

## Posts

The posts archive contains every post, including drafts in HTML format. Each HTML file is a fragment. That is, it contains only the content in HTML format, but is lacking the HTML header, styles, metadata, etc. This makes it easy to import into another blogging tool.

The HTML itself is the same HTML used on your Substack website. This means it includes links to larger images, little SVG icons for enlarging images, and so on, but does not include the styling or scripting to make those things work.

If you are importing these things into your own site, you’ll need to either fix the HTML or create new CSS rules to display this to match your new site. I chose to programmatically fix the HTML, which I’ll describe below.

## Images

As a I mentioned above, no images are included in the export file. All images are linked and are hosted on Substack’s servers. Substack appears to be hosting images on Amazon’s S3 service, but proxying those URLs through an image service which resizes and converts the image to a desirable format like WebP.

It is unclear what Substack will do with those images over time. Are they committing to perpetual image hosting? Who knows?

This motivated me to download all of my images.

Buttondown and Wordpress.com (Wordpress the commercial product, not the free version) will both import those images for you.

# Choices

## Site

This site is built with [Astro](https://astro.build). I’ve been happy with Astro. It’s a good HTML-first tool for building custom websites.

Astro has good support for working with content collections in Markdown, JSON, and other data formats.

I already use these features for my portfolio. Incorporating newsletter content works the same way.

Astro has some built in image processing tools. At build time, Astro will reformat and resize images for use on the web. This means I didn’t have to pay for my own image hosting service, nor roll my own.

## Email

The newsletter “format” of sending my writing out via email to people who want it works well. It shows up in your inbox. You can read it now, or read it later. Once downloaded, it lives on your device. I didn’t want to give up sending email newsletter, so I looked into a couple of options:

-   [Mailjet](https://www.mailjet.com)
-   [Buttondown](http://buttondown.email/)

Mailjet is a professional tool. I’ve used it at work as a system to bulk send emails to testing platforms (ask me if an emoji works in a particular email client, I can tell you).

Mailjet will absolutely support newsletters, but also requires I configure a special email sending sub-domain (like email.abouthalf.com or something similar).

I’m not ready for that level of commitment. I ended up choosing Buttondown. It’s very similar to Substack, but not problematic.

One of the best features of Buttondown, is that I can choose my own “read on web” URL - so I can publish a blog post, copy it into a newsletter, and direct readers to my website instead of Substack.

# Process

After reviewing Substack’s anemic export, I realized I wanted all those thumbnail images I carefully chose over the past 2 years.

The RSS feed provided by Substack included the thumbnail image, but doesn’t include every post, only the last several.

The archive page which Substack generates includes thumbnails, but it’s a dynamic web application. All of the content is generated by a JavaScript application, so there’s nothing “in” the HTML. Unclear if this is just lazy or a deliberate mechanism to prevent writers from getting organic traffic outside of the Substack ecosystem.

The archive page is an “infinite scroller” - that is when you get to the bottom of the page it loads in the next block of posts. I scrolled all the way to the bottom to load in all the posts, then used my browser’s developer tools to extract the generated HTML. I saved this to a file and wrote a script to find all the images, and then download them.

I used `cheerio` to process the HTML. [Cheerio](https://www.npmjs.com/package/cheerio) is a NodeJS package which replicates the [jQuery](https://api.jquery.com) API, but in server-side JavaScript. The basically means I can load up an HTML file and pass in a query like:

```javascript
const linkedImages = $(“a.classname img”).attr(“src”)
```

Then iterate over the results and create a list of images to download.

My script collected image URLs and extracted the URL slug of each post. That way I could map slug-to-image and create a look up map for my posts later.

Next I needed to work on the posts.

The same downloading technique I used for thumbnails worked for post images as well. I was able to download 700-ish megabytes of images (several times actually, it took a few tries). I stored all of these locally in my project. That’s not small but I’m not rebuilding my site every 5 minutes. so I can live with it.

As I mentioned above Substack is hosting their images using S3 behind some image hosting service. This created a challenge in that many of these URLs are missing file extensions. In order to name the files properly, I checked the mime-type of each image on download, and renamed the file with the corresponding file extension.

The HTML provided in Substack’s export has a lot of stuff I don’t want. Using Cheerio again I was able to restructure markup I didn’t want - in this case I was mostly fixing image URLs and removing links to images. Basically I’d find all the links to images, wrapped around `<picture>` elements and replace those links with a simple image element.

I also wanted something a little more versatile than clumps of HTML. I used `turndown` - a [tool](https://www.npmjs.com/package/turndown) which converts HTML into [Markdown](https://www.markdownguide.org) to strip out all the unwanted formatting and cruft from the HTML leaving me with minimally formatted text.

Astro works directly with standard Markdown files, but if you want to include thumbnails or metadata like a title, publication date, and so forth, you need to add `frontmatter` to the Markdown file. [Frontmatter](https://markdoc.dev/docs/frontmatter) is just a set of variables, in [YAML](https://yaml.org) format, at the top of a Markdown file, demarcated by three dashes before and after the data. Like so:

```markdown
---
title: A title in frontmatter
date: 2024-01-10
etc: stuff
---

# A heading

some text in a paragraph.
```

I updated my thumbnail extraction script to include publication dates, titles, and other metadata. Then was able to marry the thumbnails and metadata to each converted HTML file. I used the [markdown processing library](https://www.npmjs.com/package/gray-matter) `gray-matter` to prepend frontmatter to each Markdown file.

With all of this complete, I had a giant collection of blog posts in a folder in my website project. I updated my content configuration in Astro and created a page template for blog posts, and an index page to display links to all the posts.

With 700MB of images, this takes about 10 minutes to build (converting all the images is slow in NodeJS) but my build tool caches images between builds, so subsequent builds are faster.

The only thing left to do was to make blogging easier. I created a small script which accepts a title, then creates a new Markdown file with metadata, including publication date. This saves me a lot of manual work. I can just copy / paste from my writing software (Byword or Day One) into the new file, preview in dev mode, then push my changes up to GitHub.

This is all very manual, and I’m not going to lie, I miss the convenience of using a tool like Substack. But now, at least, I own all of my content and I can migrate any and all of it anywhere else.

# Examples

## Create a new newsletter with easy metadata

Below is my "make a new blog" script. I run it like so:

```bash
node ./scripts/blog.mjs -t "a blog post title"
```

It's a pretty simple little script.

-   `commander` provides command line parameters
-   `gray-matter` generates frontmatter in a markdown file
-   `slug` generates URL-friendly slugs from my title
-   `fs` is the standard NodeJS file system module, which lets me write out the file

```javascript
import { program } from "commander";
import matter from "gray-matter";
import fs from "fs";
import sluggo from "slug";

function main() {
    program
        .version("0.0.1")
        .option("-t, --title <input>", "Title of the post", "Untitled");
    program.parse();

    const { title } = program.opts();
    const now = new Date();
    const isoDate = now.toISOString();
    const [year, month, day] = isoDate.split("T")[0].split("-");
    const content = `# ${title}`;
    const slug = sluggo(title);
    const markdown = matter.stringify(content, {
        title,
        slug,
        link: `/newsletter/${slug}`,
        isoDate: new Date(isoDate), // prefer date object to string
        contentSnippet: title,
        content: title, // derp. crufties.
        thumbnail: null,
        // for RSS…
        pubDate: now.toLocaleString("en-US", {
            weekday: "short",
            day: "numeric",
            month: "short",
            year: "numeric",
            hour: "numeric",
            minute: "numeric",
            second: "numeric",
            timeZoneName: "short",
            timeZone: "GMT",
        }),
    });

    fs.writeFileSync(
        `src/content/newsletter/${year}-${month}-${day}-${slug}.md`,
        markdown,
        "utf8",
    );
}

main();
```

# Image downloader with renaming

This image downloader uses the ubiquitous Fetch API to grab the image.

I grab the mime-type from the response headers an duse the `mime-types` library to look up the proper file extension. If the provided url has no file part (a lot of S3 URLs are just a long ID) I can append a proper file extension and make Astro and everyone else happy.

The `finished` API from the standard `stream/promises` NodeJS package allows me to await asynchronously downloading data and know when it's completed writing to a file. From there I return the new file name to stash where needed.

```javascript
import fs from "fs";
import path from "path";
import { Readable } from "stream";
import { finished } from "stream/promises";
import mime from "mime-types";

/**
 *
 * @param {string} url URL of download
 * @param {string} filePath path to save file to
 * @returns {string} file name of saved file
 */
export default async function download(url, filePath) {
    const response = await fetch(url);
    if (!response.ok) {
        console.log(`unexpected response ${response.statusText}`);
        console.log("Could not download file", filePath);
        return;
    }
    const contentType = response.headers.get("content-type");
    const extension = mime.extension(contentType);
    const extname = `.${extension}`;
    const originalExtanme = path.extname(filePath);
    if (!originalExtanme) {
        filePath += extname;
    } else if (originalExtanme && originalExtanme !== extname) {
        filePath = filePath.replace(/\.[^.]+$/, extname);
    }
    const stream = fs.createWriteStream(filePath);
    await finished(Readable.fromWeb(response.body).pipe(stream));
    console.log({ url, contentType, extension, filePath, originalExtanme });
    return path.basename(filePath);
}
```
