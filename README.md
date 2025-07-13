# AMP-Static-Blog v1

This is a blog customized from eleventy-base-blog v9.

## Steps

1. Save these files to a new folder in your GitHub folder with the blog name you want.

2. Install dependencies

```
npm install
```

3. Run Eleventy

Generate a production-ready build to the `_site` folder:

```
npx @11ty/eleventy
```

Or build and host on a local development server:

```
npx @11ty/eleventy --serve
```

## Features

1. sitemap.xml
2. OG social sharing meta
3. Recommended posts by tag matches
4. Site search
5. Featured text on home page
6. Mobile menu
7. Redirects added
8. Embed Everything
9. Amazon Affiliate built in

## How to use og social sharing meta

Add the below in frontmatter

- image: /images/flirty-text-message-poems.jpeg
- title: your title here
- description: your description here

## How to use recommended posts by tag matches

Add the below in frontmatter

- tags: ["tag1"] or
- tags: ["tag1","tag2"]

More tags matching = higher priority to be recommended.

The code for this is ONLY in the post.njk and is commented.
The styles are located in custom.css

## How to use site search

[This article helps a lot](https://rknight.me/blog/using-pagefind-with-eleventy-for-search/)

What ever has data-pagefind-body gets indexed basically.

example:

<article data-pagefind-body>
    {{ content | safe }}
</article>

Insert this code where you want the search box to show.

<link href="/_pagefind/pagefind-ui.css" rel="stylesheet">
<div id="search" class="search"></div>
<script src="/_pagefind/pagefind-ui.js" onload="new PagefindUI({ element: '#search', showImages: false });"></script>

commands:

npm install --save-dev pagefind
npm uninstall --save-dev pagefind

## How to use featured text on home page

This is loclated in the index.njk

## How to use redirects

added this shortcode in eleventy.config.js already
// This adds a redirects file.
	eleventyConfig.addPassthroughCopy("_redirects");

In the _redirects file you can see how to setu redirects.

## How to use embed everything

npm install eleventy-plugin-embed-everything
npm uninstall eleventy-plugin-embed-everything (to remove)

add this to your eleventy.config.js file

const embeds = require("eleventy-plugin-embed-everything");
module.exports = function(eleventyConfig) {
  
  // (...other Eleventy configuration settings...)

  eleventyConfig.addPlugin(embeds);

};

[Helpful Article](https://gfscott.com/embed-everything/)

## Eleventy Notes

* [Want a more generic/detailed getting started guide?](https://www.11ty.dev/docs/getting-started/)

[Eleventy](https://www.11ty.dev/) site generator (using the [v3.0 release](https://github.com/11ty/eleventy/releases/tag/v3.0.0)).

_Optional:_ Review `eleventy.config.js` and `_data/metadata.js` to configure the site’s options and data.

Demo: [Cloudflare Pages](https://eleventy-base-blog-d2a.pages.dev/)

- `content/about/index.md` is an example of a content page.
- `content/blog/` has the blog posts but really they can live in any directory. They need only the `posts` tag to be included in the blog posts [collection](https://www.11ty.dev/docs/collections/).
- Use the `eleventyNavigation` key (via the [Eleventy Navigation plugin](https://www.11ty.dev/docs/plugins/navigation/)) in your front matter to add a template to the top level site navigation. This is in use on `content/index.njk` and `content/about/index.md`.
- Content can be in _any template format_ (blog posts needn’t exclusively be markdown, for example). Configure your project’s supported templates in `eleventy.config.js` -> `templateFormats`.
- The `public` folder in your input directory will be copied to the output folder (via `addPassthroughCopy` in the `eleventy.config.js` file). This means `./public/css/*` will live at `./_site/css/*` after your build completes.
- This project uses three [Eleventy Layouts](https://www.11ty.dev/docs/layouts/):
	- `_includes/layouts/base.njk`: the top level HTML structure
	- `_includes/layouts/home.njk`: the home page template (wrapped into `base.njk`)
	- `_includes/layouts/post.njk`: the blog post template (wrapped into `base.njk`)
- `_includes/postslist.njk` is a Nunjucks include and is a reusable component used to display a list of all the posts. `content/index.njk` has an example of how to use it.