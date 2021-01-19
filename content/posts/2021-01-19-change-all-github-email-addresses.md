---
template: post
title: Change all Github email addresses
slug: change-all-github-email-addresses
draft: true
date: 2021-01-19T17:47:05.782Z
category: programming
tags:
  - programming
---
I have found out that recruiters have hunted me down using the email address I have inadvertedly used to commit in Github. Unfortunatley it's not straightforward to replace this, but here is what I've done:

From an **empty folder** clone all your public repos using github API. Replace `YOUR-GITHUB-USERNAME`.
```
for SSH_URL in $(curl -s https://api.github.com/users/YOUR-GITHUB-USERNAME/repos | grep ssh_url | cut -d'"' -f 4)
do
    git clone $SSH_URL
done
```
This is a good time to  **BACKUP THIS ENTIRE FOLDER**.

For every repo just cloned, run `git filter-branch` and check the committer and author email (they are two different things).

I had multiple emails, and each needs to be checked for each case. This looks crazy syntactically, but still easier than an `in` operator in bash...
You'll need one line to test for each case you may have used like "EmailOne", "emailone", "emailTwo", etc, depending on how you tend to type this.

Force push after this is done. I have commented out this line because you'll probably want to check what happened (use `git log`).


```
for dir in ./*/
do
    cd $dir || exit
    pwd
    FILTER_BRANCH_SQUELCH_WARNING=1 git filter-branch -f --commit-filter '
    if [ "$GIT_COMMITTER_EMAIL" = "ONE.OF@YOUR.EMAILS" ] \
      || [ "$GIT_COMMITTER_EMAIL" = "ANOTHER.ONE.OF@YOUR.EMAILS" ] \
      || [ "GIT_AUTHOR_EMAIL" = "ONE.OF@YOUR.EMAILS" ] \
      || [ "GIT_AUTHOR_EMAIL" = "ANOTHER.ONE.OF@YOUR.EMAILS" ];
    then
        GIT_COMMITTER_EMAIL="i-dont-want@to-be-recuited.thank-you-very-much";
        GIT_AUTHOR_EMAIL="i-dont-want@to-be-recuited.thank-you-very-much";
        git commit-tree "$@";
    else
         git commit-tree "$@";
    fi' HEAD
    #git push -f
    cd ..
done

```

If you are trying to dodge recruiters maybe you should check out this project that will allow you to filter their emails in Gmail: [I don't want to be recruited, thank you very much on Github](https://github.com/StefanoChiodino/i-dont-want-to-be-recruited-thank-you-very-much). 