# Basic git branching workflow
      


  

**Permitted branches:**

-   **master** anything that goes to production goes via this
-   **develop** – contains code for whatever there is in master + new feature pending release into master
-   **_feature/<feature\_name>_**: for a new feature that you are working on. You will create this branch from _develop_.
-   **_hotfix/<bug\_name>_**: There is a bug in production. You will create the branch from the _master__._

**What is a hotfix?**

If your production system is facing a breaking issue. There is a 500 error. The customer is not able to make payment. The customer is not able to place an order. The hotfix is called hotfix because you are making small quick changes in the production environment. One needs to pay attention to what constitutes (to)- Delete a hotfix:

-   It should be very a critical issue

-   some very critical error
-   500 error

-   It should be something that can be fixed in a short duration of time

-   the fix should be solved in minutes(max a few hours)..- Delete one full stop

-   It should be a small change

-   Most errors are some silly mistakes that require a character change or line change. At max, a few lines change.

When creating a hotfix, create your local branch from **master**.

  

**What is a feature?**

Any other change other than a hotfix is considered a feature. A feature can consist of:

-   new feature development
-   addressing new corner cases
-   code refactor

When creating a feature branch, create your local branch from **develop**.

**FAQs:**

**I am done with a feature development in feature/<feature\_name>. What shall I do now?**

-   Once you are done with the feature testing you need to merge the branch with **develop**.
-   The problem with merging with **develop** branch is that the code in **develop** is supposed to contain code that is supposed to go into **master** soon.
-   So you should merge code to **develop** when you are sure that your feature is ready to go to production.
-   If not, complete your work and park the feature for a while.
-   If your feature has a specific release date, do all the necessary testing in the feature branch itself and try and not block the production pipeline by merging too early. After testing merge into **develop** closer to release date.
-   follow the merge request checklist for the feature branch

**I have merged my feature branch into develop, but I encountered a bug while testing in develop?**

-   If the code is not in production yet, you don't need to create a new branch to fix the bug in **develop**. Solve the bug in develop itself.

  

**Can I create multiple feature branches?**

Yes. If you are working on a feature that got de-prioritized and wants to work on a new feature, you can park the feature and create a new **feature/<feature\_name>** branch from **develop** branch.

  

**Checklists:**

**Creating a new branch checklist:**

-   name it properly –

-   **feature/<feature\_name>** for a feature branch
-   **hotfix/<bug\_name>** for hotfix

-   make sure your local **develop** and **master** branches are up to date. Run **git pull** on both these branches. Remember, others are contributing code too.
-   Create a branch from the right branch

-   from **develop** for the feature branch
-   from **master** for the master branch

**Merge checklist – feature/<feature\_name> branch:**

-   pull the code from a remote **feature** branch into your local **feature/<feature\_name>** branch.

-   While you were working on your feature in the silo, someone else could have an updated feature branch. Your merge is accepted faster if you resolve any merge conflicts arising from race conditions.

-   push code to the remote server
-   Create a merge request on **a feature** branch on Gitlab/Github via the UI.

**Merge checklist – hotfix/<bug\_name> branch:**

-   pull the code from the remote **master** branch into your local **hotfix/<bug\_name>** branch

-   While you were working on your feature in the silo, someone else could have an updated master branch. Your merge is accepted faster if you resolve any merge conflicts arising from race conditions.

-   push code to the remote server
-   Create a merge request to **master** and **develop** branch on Gitlab/Github via the UI

**Notes:**

-   You can avoid making mistakes in remembering the details. Install git-flow to take care of these cases. [https://github.com/nvie/gitflow](https://github.com/nvie/gitflow).
-   We use a subset of the git-flow branching strategy. For details [https://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)