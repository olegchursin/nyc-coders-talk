# Deploy Your Site Securely and Easily with Netlify and Browser Headers

Simple blog starter based fully on the official GatsbyJS one: [gatsby-starter-blog](https://github.com/gatsbyjs/gatsby-starter-blog)

[![Netlify Status](https://api.netlify.com/api/v1/badges/6f2a6346-e7e0-496b-9dbf-0b20dfb97481/deploy-status)](https://app.netlify.com/sites/deploy-and-secure/deploys)

## Intro

*Our goals:*

* create a simple website (blog)
* add a new blog post
* publish our website to Netlify
* secure it with browser security headers

*Your takeaways:*

* step-by-step guide on how to publish a website with Netlify
* Netlify config file with working config for basic browser security headers

## Let’s go

### Step 1. Create a simple website (blog).

Question 0 - which tech stack to use. We will be working with GatsbyJS ([GatsbyJS](https://www.gatsbyjs.org/)) which is an amazing static site generator allowing to create blazing fast websites at almost no time. I will not waste time enumerating all of the Gatsby features, but do make sure that you play with it. And if you happen to like the result, feel free to join GatsbyNYC Meetup ([Gatsby NYC (New York, NY) | Meetup](https://www.meetup.com/Gatsby-NYC/)) that I have an honor to co-host.

Make sure you have `gatsby-cli` installed by running `gatsby -v`. If not install Gatsby globally with:

```shell
npm install -g gatsby-cli
```

GatsbyJS has a concept they call starters.

## 🚀 Quick start

1.  **Create a Gatsby site.**

    Use the Gatsby CLI to create a new site, specifying the blog starter.

    ```shell
    # create a new Gatsby site using the blog starter
    gatsby new deploy-and-secure https://github.com/olegchursin/nyc-coders-talk
    ```

2.  **Start developing.**

    Navigate into your new site’s directory and start it up.

    ```shell
    cd deploy-and-secure/
    gatsby develop
    ```

3.  **Open the source code and start editing!**

    Your site is now running at `http://localhost:8000`!

    _Note: You'll also see a second link: _`http://localhost:8000/___graphql`_. This is a tool you can use to experiment with querying your data. Learn more about using this tool in the [Gatsby tutorial](https://www.gatsbyjs.org/tutorial/part-five/#introducing-graphiql)._

    Open the `my-blog-starter` directory in your code editor of choice and edit `src/pages/index.js`. Save your changes and the browser will update in real time!

## 🧐 What's inside?

A quick look at the top-level files and directories you'll see in a Gatsby project.

    .
    ├── node_modules
    ├── src
    ├── .gitignore
    ├── .prettierrc
    ├── gatsby-browser.js
    ├── gatsby-config.js
    ├── gatsby-node.js
    ├── gatsby-ssr.js
    ├── LICENSE
    ├── package-lock.json
    ├── package.json
    └── README.md

1.  **`/node_modules`**: This directory contains all of the modules of code that your project depends on (npm packages) are automatically installed.

2.  **`/src`**: This directory will contain all of the code related to what you will see on the front-end of your site (what you see in the browser) such as your site header or a page template. `src` is a convention for “source code”.

3.  **`.gitignore`**: This file tells git which files it should not track / not maintain a version history for.

4.  **`.prettierrc`**: This is a configuration file for [Prettier](https://prettier.io/). Prettier is a tool to help keep the formatting of your code consistent.

5.  **`gatsby-browser.js`**: This file is where Gatsby expects to find any usage of the [Gatsby browser APIs](https://www.gatsbyjs.org/docs/browser-apis/) (if any). These allow customization/extension of default Gatsby settings affecting the browser.

6.  **`gatsby-config.js`**: This is the main configuration file for a Gatsby site. This is where you can specify information about your site (metadata) like the site title and description, which Gatsby plugins you’d like to include, etc. (Check out the [config docs](https://www.gatsbyjs.org/docs/gatsby-config/) for more detail).

7.  **`gatsby-node.js`**: This file is where Gatsby expects to find any usage of the [Gatsby Node APIs](https://www.gatsbyjs.org/docs/node-apis/) (if any). These allow customization/extension of default Gatsby settings affecting pieces of the site build process.

8.  **`gatsby-ssr.js`**: This file is where Gatsby expects to find any usage of the [Gatsby server-side rendering APIs](https://www.gatsbyjs.org/docs/ssr-apis/) (if any). These allow customization of default Gatsby settings affecting server-side rendering.

9.  **`LICENSE`**: Gatsby is licensed under the MIT license.

10. **`package-lock.json`** (See `package.json` below, first). This is an automatically generated file based on the exact versions of your npm dependencies that were installed for your project. **(You won’t change this file directly).**

11. **`package.json`**: A manifest file for Node.js projects, which includes things like metadata (the project’s name, author, etc). This manifest is how npm knows which packages to install for your project.

12. **`README.md`**: A text file containing useful reference information about your project.

## 🎓 Learning Gatsby

Looking for more guidance? Full documentation for Gatsby lives [on the website](https://www.gatsbyjs.org/). Here are some places to start:

- **For most developers, we recommend starting with our [in-depth tutorial for creating a site with Gatsby](https://www.gatsbyjs.org/tutorial/).** It starts with zero assumptions about your level of ability and walks through every step of the process.

- **To dive straight into code samples, head [to our documentation](https://www.gatsbyjs.org/docs/).** In particular, check out the _Guides_, _API Reference_, and _Advanced Tutorials_ sections in the sidebar.

### Step 2. Add a new blog post

The folder that is of interest to us is `content` - that’s where our blog posts live in the for of markdown files. And that’s where we will be adding our new blog post.

It’s high time to see something in the browser. Fire up your newly created blog with  `npm start` or `yarn start`. This will run `gatsby develop` command under the hood which will do it’s magic and make your blog available at `http://localhost:8000/` by default. 

You may have noticed that Gatsby gives you some magic to play with. Folders (folder-names) in `content > blog` automagically become routes. The same thing happens with folders in `pages`.

Therefore, we will create a new folder in `blog`. Let’s name it `deploy-and-secure`. Inside the newly created folder we will touch `index.md`file with the following content:

```MD
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

Blog post content goes here...
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

> ### Continuous Deployment
> Choose the Git provider where your site’s source code is hosted. When you push to Git, we run your build tool of choice on our servers and deploy the result.

We chose GitHub, search for the needed repo and select it.

Then we specify `branch to deploy`. In our case let’s stick to default `master`, and Netlify already knows that we have a Gatsby site, so in **Basic build settings** section it gives us all the needed defaults for `build command` and `publish directory`.

Hit **Deploy site** now. Wait… and wait again. Once it’s done you site is available under netlify-generated url. Let’s change that. 

Click on **Domain settings** and under Custom domains click on **Options** and **Edit this name**. Save your changes and voila you have your site on https://your-site-name.netlify.com

### Step 4. Secure your website with browser security headers

Always start with definition:
Browser security headers - HTTP response headers that your application can use to increase the security of your application. Once set, these HTTP response headers can restrict modern browsers from running into easily preventable vulnerabilities.

#### More information on headers:
**OWASP Secure Headers Project** [Link](bit.ly/owasp-security-headers)

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

RTFM. 

Netlify docs on custom headers: [Custom headers | Netlify Docs](https://docs.netlify.com/routing/headers/)

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