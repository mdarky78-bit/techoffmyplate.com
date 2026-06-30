# Tech Off My Plate — Website

This is now a proper small static site built with Eleventy (11ty), instead of a single HTML file. It deploys to Netlify automatically every time you push to GitHub.

## How it's structured

```
src/
  _includes/
    base.njk          <- the shared header, nav, footer, and SEO tags used on every page
    blog-post.njk      <- the layout each blog post uses
  index.njk            <- the homepage content
  blog/
    index.njk           <- the blog listing page
    posts/*.md           <- one markdown file per blog post
  css/style.css          <- all the site's styling, in one place
  images/                <- site images
  admin/                  <- the Decap CMS editor (see below)
  robots.txt
  sitemap.njk             <- sitemap.xml, builds itself from your pages and posts automatically
.eleventy.js              <- site build configuration
netlify.toml                <- tells Netlify how to build the site
```

## Editing the homepage

Open `src/index.njk`. It's the same HTML you've seen before (pricing, FAQ, about, etc.), just with the header and footer moved out into `base.njk` so you don't repeat them. Edit the text directly, or send sections back to Claude to update.

## Writing blog posts (the easy way)

You asked for a simple editor, so this is set up with **Decap CMS**, a free, open-source content editor that writes plain files to your GitHub repo. You do not touch code to write a post.

**One-time setup (you'll need to do this in your Netlify dashboard):**
1. Site settings → Identity → Enable Identity
2. Identity → Services → Enable Git Gateway
3. Identity → Invite users → invite your own email
4. Accept the invite email, set a password

**Writing a post after that:**
1. Go to `https://www.techoffmyplate.com/admin`
2. Log in
3. Click "New Blog Posts", fill in title, date, description, optional cover image, and write the post
4. Click Publish

That's it. It commits a new file to `src/blog/posts/`, Netlify rebuilds the site automatically, and the post appears on `/blog/`, gets added to the sitemap, and gets its own SEO tags and structured data, all without you touching HTML.

## Local preview (optional, for Claude or a developer to use)

```
npm install
npx @11ty/eleventy --serve
```

## Deploying

Push this whole folder to a GitHub repository and connect that repo to Netlify (or update your existing connected repo). Netlify will read `netlify.toml`, run `npx @11ty/eleventy`, and publish the `_site` folder automatically on every push. You no longer drag-and-drop a single `index.html`.
