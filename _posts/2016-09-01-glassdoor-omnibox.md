---
layout:     post
title:      Add Glassdoor's company search to Chrome's address bar
date:       2016-09-01
summary:    I find myself looking up companies through Glassdoor extremely often.  I added a tab-complete search functionality to Chrome's address bar to speed up my workflow.  Here's how to do it!
categories: Chrome omnibox search Glassdoor jobs
---


Often when I see a job listing, I want to read about the company that posted it.  [Glassdoor](www.glassdoor.com) is the place to do it-- I can read about salaries, work conditions, interviews, etc. from the employees themselves.

I found myself using this specific type of Glassdoor search so often, that I found myself wishing for the ability to `tab` after typing `glassdoor.com` to directly search, just like you can with `youtube.com` and `maps.google.com` in Chrome's address bar (officially, the _omnibox_).  (Note that you can also look up other things on Glassdoor, such as job titles, but almost every search I do is for a company.)

I used Chrome's developer tools to inspect the page, capture network traffic, and identify the request string needed to make this happen.  (If you want to build a similar search, try this out!)  Here's how you add it:

<hr>
In Chrome, open up Settings, and find Search.  Click on `Manage search engines...`.

<center><img src="/assets/img/glassdoor-search/glassdoor0.png"></center>

Scroll to the bottom.  In each field, respectively, type a name for your search engine (e.g. `Glassdoor Companies`), type the base URL which Chrome will use to autocomplete your search (`glassdoor.com`), and finally type the following string:

    https://www.glassdoor.com/Reviews/company-reviews.htm?suggestCount=10&suggestChosen=false&clickSource=searchBtn&typedKeyword=%s&sc.keyword=%s&locT=C&locId=&jobType=

<center><img src="/assets/img/glassdoor-search/glassdoor1.png"></center>

That's all there is to it!  Try it out.  Here I typed `glassdoor.com` followed by a `tab`, and then typed `Facebook`.

<center><img src="/assets/img/glassdoor-search/glassdoor2.png"></center>

Press `enter` and there we go!  Note that this search will automatically jump to the company if the choice is obvious, and if not it will give you multiple results.

<center><img src="/assets/img/glassdoor-search/glassdoor3.png"></center>
