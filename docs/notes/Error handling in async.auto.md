# Error handling in async.auto
---
- Keywords:#pattern
- author: #alex
---
- Suppress error, not acting on it or just console.logging has lot's of unknow consequences.  
- We won't able to identify any errors that is genuinely effecting the business/product functionalities. examples:
        - we assumed a function created an user but it threw a unique email id error. Due to suppression we showed a wrong message to the customer that he account is activated  
        - Any validation error the function threw
- Our monitoring systems won't able to capture if we don't capture error 

```
// AwesomeController.js
module.exports = {
    listAwesomeness: function (req, res) {
        async.auto({
            getTheCoolThing: function (cb) {
                Cool.find({ id: req.params.id }).exec(function (err, c) {
                    // **always pass the unknown error passed from the function**
                    if (err) return cb(err);
                    // **always create a Error object to pass a custom error**
                    if (!c) return cb(new Error("COOL_NOT_FOUND")); 
                    return cb(null, c);
                });
            },
            getTheHotThing: ['getTheCoolThing', function (results, cb) {
                Hot.find({ id: req.params.id }).exec(function (err, h) {
                    if (err) return cb(err);
                    if (!c) return cb(new Error("HOT_NOT_FOUND"));
                    return cb(null, h);
                });
            }]
        }, function (err, results) {
            if (err) {
                //**always use the switch case to handle error.**
                switch (err.message) {
                    case 'COOL_NOT_FOUND': 
                    case 'HOT_NOT_FOUND':
                        return res.status(404).view('not_found_view', { error: 'NOT_FOUND' })
                        break; // **always use a break to exit out of the loop**
                    default: // **alway throw the error for unknown case. **
                        throw err;
                        break;
                }
            }
            var locals = {
                cool: results.getTheCoolThing,
                hot: results.getTheHotThing
            }
            return res.view('list_awesome_view', locals)
        });
    }

}
```