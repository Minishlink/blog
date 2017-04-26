---
layout: post
title:  "Remove sensitive information from your Git repository"
categories: dev
tags: git
---
# Remove sensitive information from your Git repository
**DISCLAIMER**: This will rewrite your Git history and you won't be able to go back in time if you don't make a backup.

You have removed secret variables from your repo, but they obviously still show up in your Git history.
There are several ways to get rid of them completely, and here's the quickest:

1. Install [BFG](https://rtyley.github.io/bfg-repo-cleaner/)
    * On macOS: `brew install bfg`
2. Clone your repo in a bare repo
    * `git clone --mirror url/to/your/repo.git`
3. Create a file with a new line for each string you want to remove
    * `echo "string" >> secret.txt`
    * `echo "second_string" >> secret.txt`
4. Remove the strings in your repo history
    * `bfg --replace-text secret.txt repo.git`
5. `cd repo.git`
6. Clean your repo
    * `git reflog expire --expire=now --all && git gc --prune=now --aggressive`
7. `git push`
8. Notify your coworkers that they have to clean their branches
    * `git fetch origin/branch`
    * `git checkout -B branch origin/branch`

Note that if your repo is public, the Git history might have been cloned somewhere in the world,
so your sensitive are already compromised. In that case, beware of a "Streisand" effect...
