# Launch.json for 11ty projects
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}/node_modules/@11ty/eleventy/cmd.js"
            // "program": "npx @11ty/eleventy --serve"
            
        }
    ]
}
```
Use this when you want to debug eleventy serve 