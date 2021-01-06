# Asset pipeline done right
---
- Keywords:#pattern
- author: #alex
---
Sails out of the box supports a framework to handle assets. It comes with a folder structure and pipeline configuration that loads those files from assets folders to sails runtime for browser consumption.

The top level folder should **not contain anything more than** these folders and files.
![structure](/files/assets_structure.png)

## fonts
- Its a folder  
- will contain all my fonts.  
![structure](/files/assets_fonts.png)
## images
- Its a folder 
- will contain all my images
- I can also make subfolders to organise.  
![structure](/files/assets_images.png)
## js
- its a folder
- its has subfolder called dependencies where i can put all my external dependencies.
- Any thing custom that is specific to my app i will put under the root folder.
- I can also make subfolders to organise.  
![structure](/files/assets_js.png)
## styles
- its a folder
- All css files goes here.
- I can also make subfolders to organise.  

![structure](/files/assets_styles.png)

## So why we are enforcing this structure?
- This helps sails understand where to pick an asset and in what order. This is a sample configuration snippet from tasks/pipeline.js.  
![structure](/files/assets_pipeline.png)
- Sails also takes care of automatically linking those assets in ejs files via custom code blocks. Example  
- That means i need not add js or css file location manually.  
![structure](/files/assets_layout_section.png)
## Browser caches asset files, how do I inform the browser that there's new stuff in the asset file without changing the filename?
- Sails helps you achieve this with minute tweak into the asset pipeline configuration, given that I have followed  the folder and file structure recommended by sails.  
- Tweak is to add a version number as a query parameter to the asset path.   
- With a version number in the asset url, Browser considers as it a new resource that need to be fetched.  
- This happens in tasks/config/sails-linker.js.  

```
// we add a timestamp to the query param named v when the pipeline runs.

<script src="%s?v='+new Date().getTime()+'"></script>
```

![structure](/files/assets_sails_linker.png)

- And in the ejs file I can see the query param v getting added to the js/css asset path.  
![structure](/files/assets_date.png)
