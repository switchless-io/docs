# Install private gitrepo as dependancy
---
- tags: #how_to, #npm, #gitlab
- author: #alex

---

This works specifically for gitlab


Use this to create a private access token - https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html

Package.json will look like this

```javascript
"mralbert_helper": "git+https://x-oauth-basic:<gitlab_token>@github.com/<user>/<repo>.git",
```

to install
```shell
npm install --save git+https://x-oauth-basic:<gitlab_token>@gitlab.com/<user>/<repo>.git
```


Install from local file instead - [[Install NPM packages from local directory]]