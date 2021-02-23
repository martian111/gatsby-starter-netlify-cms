# Gatsby + Netlify CMS Starter

**Note:** This starter uses [Gatsby v2](https://www.gatsbyjs.org/blog/2018-09-17-gatsby-v2/).

This repo contains an example business website that is built with [Gatsby](https://www.gatsbyjs.org/), and [Netlify CMS](https://www.netlifycms.org): **[Demo Link](https://gatsby-netlify-cms.netlify.com/)**.

It follows the [JAMstack architecture](https://jamstack.org) by using Git as a single source of truth, and [Netlify](https://www.netlify.com) for continuous deployment, and CDN distribution.

## Features

- A simple landing page with blog functionality built with Netlify CMS
- Editable Pages: Landing, About, Product, Blog-Collection and Contact page with Netlify Form support
- Create Blog posts from Netlify CMS
- Tags: Separate page for posts under each tag
- Basic directory organization
- Uses Bulma for styling, but size is reduced by `purge-css-plugin`
- Blazing fast loading times thanks to pre-rendered HTML and automatic chunk loading of JS files
- Uses `gatsby-image` with Netlify-CMS preview support
- Separate components for everything
- Netlify deploy configuration
- Netlify function support, see `lambda` folder
- Perfect score on Lighthouse for SEO, Accessibility and Performance (wip:PWA)
- ..and more

## Prerequisites

- macOS or Linux development environment
  - On Windows workstations, use Windows Subsystem for Linux 2 (WSL 2) - see section below for details.
- NodeJS v14.6.0 or higher
- NPM v7.5.6 or higher
- Recommended: Environment management system such as Anaconda and/or NVM

## Getting Started

Note: These instructions are different from the upstream version of this project because this project/branch is intended to run locally only.

```
$ git clone [GIT_REPOSITORY_URL]
$ cd [REPO_NAME]
$ npm install
$ npm start
```

The URLs to access the built website and the Netlify CMS UI are displayed on the console if everything starts up properly.


### Test Build Process

To test the static page build process:
```
$ npm run build
$ npm run serve
```
Once again, the URL to access the built website will be displayed on the console if everything starts up properly.


## Windows Development Environment

This project will not work under Windows with native NodeJS installed.  Instead, install the NodeJS environment under Windows Subsystem for Linux 2 (WSL 2).  

Reference documentation:
*   [Windows Subsystem for Linux Installation Guide for Windows 10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
*   [Set up your Node.js development environment with WSL 2](https://docs.microsoft.com/en-us/windows/nodejs/setup-on-wsl2).

Important:  Make sure to verify that WSL 2 is in fact set on the Linux distribution installed by verifying with the `wsl --list --verbose` command.  For more information, refer to the first reference link above.


## Known Issues and Workarounds

### Dev server fails with "Callback was already called"

The dev server start process would fail due to a "Callback was already called" error.  There doesn't seem to be a clear solution to the issue, but what fixed by:
*   Switching to dart-sass from node-sass
*   Use gatsby-plugin-netlify-cms v4.9.0 instead of using the latest version (v4.10.0 at the time of writing).

These workarounds are already incorporated into the `package.json` and lock files committed in this project and branch.  Do not upgrade these packages unless this issue is resolved.


### Fail to compile after publishing content via Netlify CMS

In this sample Gatsby + Netlify CMS project, there is an issue when the development server is running (using `npm start` command) and an edit to the content is done within Netlify CMS.  Normally, the browser window viewing the rendered content page should refresh with the updated content upon publishing the change via Netlify CMS.  However, due to unknown root causes, that fails with a "failed to compile" error message similar to:
```
Failed to compile
There was an error in your GraphQL query:

      Field "full_image" must not have a selection since type "String" has no subfields.

      This can happen if you e.g. accidentally added { } to the field "full_image". If you didn't expect "full_image" to be of type "String" make sure that your input source and/or plugin is correct.
      However, if you expect "value" to exist, the field might be accessible in another subfield. Please try your query in GraphiQL and use the GraphiQL explorer to see which fields you can query and what shape they have.

      It is recommended to explicitly type your GraphQL schema if you want to use optional fields. This way you don't have to add the mentioned
      "dummy content". Visit our docs to learn how you can define the schema for "undefined":
      https://www.gatsbyjs.org/docs/schema-customization/#creating-type-definitions

File: /Users/martian111/Documents/SurgeMotion/websites/starter-upstream/src/templates/product-page.js
This error occurred during the build time and cannot be dismissed.
```

Workarounds:
*   Make a whitespace edit (add a space, save, delete the space, save) in `gatsby-config.js` to trigger a refresh of the Gatsby development process.
*   OR: Restart the Gatsby development server (`Ctrl-C` and then `npm start`)

References:
*   This issue has been brought up to GatsbyJS team, but remains unsolved for this project/codebase as currently coded ([Issue 27862](https://github.com/gatsbyjs/gatsby/issues/27862)).
*   Contrary to some reports, this problem does happen under macOS:  [Issue 13469](https://github.com/gatsbyjs/gatsby/issues/13469)
*   Others:  [Issue 25307](https://github.com/gatsbyjs/gatsby/issues/25307)


## Purgecss

This plugin uses [gatsby-plugin-purgecss](https://www.gatsbyjs.org/packages/gatsby-plugin-purgecss/) and [bulma](https://bulma.io/). The bulma builds are usually ~170K but reduced 90% by purgecss.

# CONTRIBUTING

See original project at:
https://github.com/netlify-templates/gatsby-starter-netlify-cms
