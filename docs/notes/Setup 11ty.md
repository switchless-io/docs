---
author: #alex
---
# Setup 11ty


```bash
# initialise npm
npm init 
	
# install eleventy 
npm install --save @11ty/eleventy

# install markdown-it-obsidian - to convert obsidian wiki links to md links
npm install markdown-it-obsidian --save

# generate html
npx @11ty/eleventy

# run 11ty service with hot reloading
npx @11ty/eleventy --serve
```


## Modify .eleventy.js
```javascript
module.exports = function(eleventyConfig) {
  eleventyConfig.addPassthroughCopy("files");
  let markdownIt = require("markdown-it");
  let markdownItObsidian = require("markdown-it-obsidian")();
  let markdownItOptions = {
    html: true,
  };
  let markdownLib = markdownIt(markdownItOptions)
    .use(markdownItObsidian)
  eleventyConfig.setLibrary("md", markdownLib);
  eleventyConfig.setEjsOptions({
    // use <? ?> instead of <% %>
    delimiter: "?"
  });
  eleventyConfig.addPassthroughCopy("assets");
  return {
    templateFormats: [
      "md",
      // "njk",
      "html",
      // "liquid"
    ],
    // templateFormats: ["html", "njk", "md", "11ty.js"],
    markdownTemplateEngine: false,
    htmlTemplateEngine: false,
    dataTemplateEngine: false,
    dir: {
      input: ".",
      includes: "_includes",
      data: "_data",
      output: "_site"
    }
  };
};
```

## Add includes folder

## Add assets folder


## create gitignore
```
.obsidian/workspace
.obsidian/publish.json
.obsidian/graph.json

_site
node_modules
```
Ref: https://www.11ty.dev/docs/getting-started/