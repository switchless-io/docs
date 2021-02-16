# How to change Favicon
---
- Keywords: #pattern
- author: #alex
---
## What is a favicon?

The little icon that you see in a broswer tab. But default, a switchless project will have the sailjs icon as favicon.

## Create a favicon
Use this service to generate a favicon - [https://favicon.io/favicon-converter/](https://favicon.io/favicon-converter/)

Use this service to make white area transparent - [https://onlinepngtools.com/create-transparent-png](https://onlinepngtools.com/create-transparent-png)

## Update favicon
The default favicon in your switchless project will be at `assets/favicon.ico`. The favicon that you download from favicon.io will contain favicons generated in various sizes. You want the 32x32 pixel version. Copy paste that image into `/assets` and rename it as `favicon.io` to replace the favicon.

After pushing to production, you might experience some catching issues. Try clearing the [cache on cloudflare](How%20to%20clear%20cache%20in%20cloudflare.md) and [cache in your browser](How%20to%20clear%20cache%20in%20your%20browser.md) to see your new favicon.