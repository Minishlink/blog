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

1. Make sure you have Java installed
2. Install [BFG](https://rtyley.github.io/bfg-repo-cleaner/)
    * On macOS: `brew install bfg`
3. Clone your repo in its entirety (every refs) inside a bare repo
    * `git clone --mirror url/to/your/repo.git`
4. Create a file with a new line for each string you want to remove (each string will be rewritten as `***REMOVED***` by default)
    * `echo "my_secret_API_key" >> secret.txt`
    * `echo "glob:SECRET_*" >> secret.txt` (search by glob pattern)
    * `echo "regex:password=\w+==>password=" >> secret.txt` (search by regex pattern and change default rewritten text)
5. Remove the strings in your repo history
    * `bfg --replace-text secret.txt repo.git`
6. `cd repo.git`
7. Now is the time to verify in your history that everything's fine
8. Clean your repo from dirty data
    * `git reflog expire --expire=now --all && git gc --prune=now --aggressive`
9. Push your changes (forcing is not necessary because you updated every refs)
    * `git push`
10. Notify your coworkers that they have to clean their branches
    * `git fetch origin/branch`
    * `git checkout -B branch origin/branch`

Note that if your repo is public, the Git history might have been cloned somewhere in the world,
so your sensitive are already compromised. In that case, beware of a "Streisand" effect...

In the future, try not to commit sensitive information in the first place ;) Here's some tips:
- Use `git diff --cached` to verify the content that you're going to commit
- Put sensitive information in `*.secret` files that are ignored in your `.gitignore`

I narrowed this article to removing sensitive information from files, but you can do much more with BFG, including
removing secret files entirely. Check out all the [BFG features](https://rtyley.github.io/bfg-repo-cleaner/#examples)!

*This article is also available on [BAM's Tech blog](https://blog.bam.tech/developper-news/remove-sensitive-information-git-repository).*
