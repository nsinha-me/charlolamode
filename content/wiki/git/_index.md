---
Title: Git
type: list
---


Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency that tracks changes in any set of computer files, usually used for coordinating work among programmers collaboratively developing source code during software development.

### Git Basics -

``` bash
    git init

    git add README.md

    git add .

    git commit -m "first commit"

    git branch -M main
 
    git remote add origin [git repo link here]

    git push -u origin main
```

### Fix Git always asking for user credentials -

1. Make Git store the username and password and it will never ask for them.
    ```
    git config --global credential.helper store
    ```
1. Save the username and password for a session (cache it);
    ```
    git config --global credential.helper cache
    ```
1. You can also set a timeout for the above setting
    ```
    git config --global credential.helper 'cache --timeout=600'
    ```
