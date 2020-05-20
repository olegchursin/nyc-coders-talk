---
title: Deploy Your Site Securely and Easily with Netlify and Browser Headers
date: "2020-05-20T22:12:03.284Z"
description: "Deploy Your Site Securely and Easily with Netlify and Browser Headers"
---

*Our goals:*
* create a simple website (blog)
* add a new blog post
* push it to GitHub
* publish our website to Netlify
* secure it with browser security headers

*Your takeaways:*
* step-by-step guide on how to publish a website with Netlify
* Netlify config file with working config for basic browser security headers

## Let’s go
### Step 1. Create a simple website (blog). 
Question 0 - which tech stack to use. We will be working with GatsbyJS ([GatsbyJS](https://www.gatsbyjs.org/)) which is an amazing static site generator allowing to create blazing fast websites at almost no time. I will not waste time enumerating all of the Gatsby features, but do make sure that you play with it. And if you happen to like the result, feel free to join GatsbyNYC Meetup ([Gatsby NYC (New York, NY) | Meetup](https://www.meetup.com/Gatsby-NYC/)) that I have an honor to co-host.

Make sure you have `gatsby-cli` installed by running `gatsby —v`. If not install Gatsby globally with:
```shell
npm install -g gatsby-cli
```

GatsbyJS has a concept they call starters. And for our needs we will chose *gatsby-starter-blog* ([gatsby-starter-blog: Gatsby Starter | GatsbyJS](https://www.gatsbyjs.org/starters/gatsbyjs/gatsby-starter-blog/)) that will leave us with a simple setup to jump-start a blog. By the way, this starter was inspired by Dan Abramov’s blog - Overreacted, which in it’s own turn is a Gatsby website ([Overreacted — A blog by Dan Abramov](https://overreacted.io/)).

Let’s create a new project with the following command:
```shell
gatsby new our-blog-name https://github.com/gatsbyjs/gatsby-starter-blog
```

And open it in your favorite text-editor.  You will get the following structure:
```
> content
> node_modules
> src
> static
  .gitignore
  .prettierignore
  .prettierrc
  gatsby-browser.js
  gatsby-config.js
  gatsby-node.js
  LICENSE
  package-lock.json
  package.json
  README.md
```

The folder that is of interest to us is `content` - that’s where our blog posts live in the for of markdown files. And that’s where we will be adding our new blog post.

It’s high time to see something in the browser. Fire up your newly created blog with  `npm start` or `yarn start`. This will run `gatsby develop` command under the hood which will do it’s magic and make your blog available at `http://localhost:8000/` by default. 

### Step 2. Add a new blog post
You may have noticed that Gatsby gives you some magic to play with. Folders (folder-names) in `content > blog` automagically become routes. The same thing happens with folders in `pages`. 

Therefore, we will create a new folder in `blog`. Let’s name it `deploy-and-secure`. Inside the newly created folder we will touch `index.md`file with the following content: 
```MD
---
title: Deploy Your Site Securely and Easily with Netlify and Browser Headers
date: “2020-05-20T22:12:03.284Z”
description: “Deploy Your Site Securely and Easily with Netlify and Browser Headers”
---

*Our goals:*
* create a simple website (blog)
* add a new blog post
* push it to GitHub
* publish our website to Netlify
* secure it with browser security headers
```

The part in between `---` is called the front matter.  You may have come across it if you have a blog on DEV.to. The rest is a good old markdown file. Just add your content and publish.

### Step 3. Publish our blog with Netlify.
There are numerous ways to publish your static site these days, but Netlify is probably one of the coolest.

Things we need to be successful:
* a website
* GitHub repo
* Netlify account

We already have our new and shiny website. You don’t need my help to push it to a GitHub repo. Let’s do the Netlify part. 

Next steps are taken under assumption that you created a Netlify account and connected it to your GitHub account. Easy.

So, within Netlify we click on `New site from Git` to setup our CD flow. Netlify will prompt us with the following:

> ## Continuous Deployment
> Choose the Git provider where your site’s source code is hosted. When you push to Git, we run your build tool of choice on our servers and deploy the result.

We chose GitHub, search for the needed repo and select it.

Then we specify `branch to deploy`. In our case let’s stick to default `master` , although for most of my personal projects I prefer to have a separate `prod` branch. Netlify is crazy smart so it already knows that we have a Gatsby site, so in **Basic build settings** section it gives us all the needed defaults for `build command` and `publish directory`.

Hit **Deploy site** now. Wait… and wait again. Once it’s done you site is available under netlify-generated url. Let’s change that. 

Click on **Domain settings** and under Custom domains click on **Options** and **Edit this name**. Save your changes and voila you have your site on https://your-site-name.netlify.com

### Step 4. Secure your website with browser security headers

Always start with definition:
Browser security headers - HTTP response headers that your application can use to increase the security of your application. Once set, these HTTP response headers can restrict modern browsers from running into easily preventable vulnerabilities.

#### More information on headers:
*OWASP Secure Headers Project*
bit.ly/owasp-security-headers

**MDN docs**
* Strict-Transport-Security // [Strict-Transport-Security - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)
* Content Security Policy (CSP) // [Content Security Policy (CSP) - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
* X-Frame-Options // [X-Frame-Options - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)
* X-Content-Type-Options // [X-Content-Type-Options - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Content-Type-Options)
* Referrer-Policy // [Referrer-Policy - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)
* Feature-Policy // [Feature-Policy - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Feature-Policy)

**Course on Pluralsight**
Introduction to Browser Security Headers by Troy Hunt
* Source: [Introduction to Browser Security Headers | Pluralsight](https://www.pluralsight.com/courses/browser-security-headers)

#### How to add headers in Netlify
RTFM. Netlify docs on custom headers: [Custom headers | Netlify Docs](https://docs.netlify.com/routing/headers/)

Straightforward, right? Let’s do it.

**TL;DR**

Add `netlify.toml` to the root.
```toml
[[headers]]
  for = "/*"
  [headers.values]
    Strict-Transport-Security = "max-age=63072000; includeSubDomains; preload"
    Content-Security-Policy = "default-src data: 'unsafe-inline' 'unsafe-eval' https:; script-src data: 'unsafe-inline' 'unsafe-eval' https: blob:; style-src data: 'unsafe-inline' https:; img-src data: https: blob:; font-src data: https:; connect-src https: wss: blob:; media-src https: blob:; object-src https:; child-src https: data: blob:; form-action https:; block-all-mixed-content"
    X-Frame-Options = "DENY"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "no-referrer"
    Feature-Policy = "microphone 'none'; geolocation 'none'"
```

Be extra careful with `Content-Security-Policy` header. You may end up breaking your site by blocking your end-users from being able to load your content. You may find this tool helpful in generating CSP for you: [Report URI: Generate your Content Security Policy](https://report-uri.com/home/generate)

#### Take you HSTS setup step further with Chromium project

The HSTS value needs to be:
`Strict-Transport-Security: max-age=31536000; includeSubdomains; preload`

You can make sure that your site is preloaded into Chromium browsers as the one that is always served over `https`. Use this tool to do it: [HSTS Preload List Submission](https://hstspreload.org/)

This is it. We’ve gone through all the steps and have successfully created, deployed, and secured our website with browser security headers on Netlify.

