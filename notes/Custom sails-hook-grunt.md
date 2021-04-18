---
-au
---
# Custom sails-hook-grunt

Previous version of `less` that is used by `grunt-contrib-less` has dependancy on `request` which is now deprecated. This results in deployments to AWS linux 2 fail.

Upgrading the packages solves the problem.


relevant github repo - https://github.com/matkappert/sails-hook-grunt