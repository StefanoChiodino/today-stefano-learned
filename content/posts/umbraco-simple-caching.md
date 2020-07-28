---
template: post
title: Umbraco Simple Caching
slug: umbraco-simple-caching
draft: true
date: 2016-11-24T23:05:23+00:00
category: Programming
tags:
  - Umbraco
  - Cache
  - Programming
---
I once looked into a pretty straightforward, very recent, website that took more than 5 seconds for the [TTFB](https://en.wikipedia.org/wiki/Time_To_First_Byte) from Azure. I created a default controller for Umbraco and set the ASP caching on: TTFB dropped to 25 m!

ince then