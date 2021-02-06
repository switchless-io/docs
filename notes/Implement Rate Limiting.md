# Rate Limiting

Install express rate limiter:
```console
npm install --save express-rate-limit
```

Add rate limiter to http.js
```javascript
myRateLimiter:require("express-rate-limit")({
  windowMs: 1 * 60 * 1000, // 1 minute
  max: 16*30 // limit each IP to 30 pages per windowMs (each request calls 16 times in this specific app )
}),
order: [
  'myRateLimiter',
]
```