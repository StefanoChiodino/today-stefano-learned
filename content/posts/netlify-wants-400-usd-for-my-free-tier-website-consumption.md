---
title: Netlify wants 400 USD for my free tier website consumption
slug: ''
draft: true
date: 2021-06-07T00:00:00+01:00
category: programming
tags: []

---
I've been an happy Netlify user for a few years. Personal use, nothing fancy, but I've found their service complement very well static websites. So, in addition to my personal website I've decided to host there a pet project with the rivetting title [https://github.com/StefanoChiodino/analytics-bypassing-adblockers](Analytics bypassing adblockers). This was to show the fundamental weakness of most adblockers, and how a simple reverse proxy can punch straight through most of them. I've now moved this to [github pages](https://stefanochiodino.github.io/analytics-bypassing-adblockers/) for now, but the reverse proxy mechanism is broken.

Just playing around with the reverso proxy concept, I found out Netlify supports this very well, and so I set this up [https://github.com/StefanoChiodino/analytics-bypassing-adblockers/blob/master/netlify.toml](this way).

```toml
# Reverse proxy anything after "/proxy/".
[[redirects]]
from = "/proxy/*"
to = ":splat"
status = 200
headers = {Access-Control-Allow-Origin = "https://analytics-bypassing-adblockers.netlify.com"}
```

Have you noticed it yet? "Reverse proxy **anything**"....no whitelist, no blacklist :(

This was used to reverse proxy Google GTM, load the page, and show that indeed, uBlock and many more would allow GTM to load and manipulate the page. A few people were upset on hacker news, then I forgot about it.

Until I received this email:

![](/uploads/netlify_chages.png)

I soon realised what happened. I only needed GTM, why did I leave it wide open?

What Laura didn't mention is that the day after I would receive another $340 bill, for a total of $400:

![](/uploads/netlify_bill-1.png)

At first I've got quite concerned, but then I realised that I never put my billing details in Netlify, so how is it possible that they charged me?

![](/uploads/netlify_question.png)

![](/uploads/netlify_answer.png)

Oh no, imagine if the BBC published an article about my website with a single 11kb page! That could have ruined my reputation!