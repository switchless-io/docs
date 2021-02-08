# Puppeteer 
is a headless chrome browser. We use this withing [[codecept]] for testing. This is also used for automation. 

Notes related to puppeteer
- [[]]

https://pptr.dev/
https://try-puppeteer.appspot.com/
## Set screen size
```javascript
const browser = await puppeteer.launch({
  args: [`--window-size=1440,768`] 
});
```

## Wait for element to disappear
```javascript
await page.waitForSelector('.dimmer-holder', { hidden: true });
```


## Add reusable scripts to window context



ref: https://stackoverflow.com/questions/48476356/is-there-a-way-to-add-script-to-add-new-functions-in-evaluate-context-of-chrom