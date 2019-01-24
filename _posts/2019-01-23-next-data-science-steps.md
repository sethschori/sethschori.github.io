---
layout: post
title:  "Next Data Science Steps and What I've Been Up To Recently"
date:   2019-01-23 23:25:00 -0500
categories: data-science
tags:
- meta data science
---
I haven't blogged in about two weeks. Here's what I've been up to with 
data science and programming recently.

- I had a small but interesting consulting project with a client I've 
previously worked with. It involved a proof of concept to read and write 
records via the APIs of a proprietary CRM system. It was an opportunity for 
me to work with OAuth (OAuth2, actually) for the first time. I was 
pleasantly surprised by how the
[requests library](http://docs.python-requests.org/en/master/)
(which I've used before and liked) has built-in OAuth2 support via the
[requests-oauthlib package](https://github.com/requests/requests-oauthlib) 
and this made it much easier to work with OAuth2 than I expected. 

  - Here are the [details on requests' support for Web Application 
Flow](https://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html#web-application-flow)
(which is the flow I needed to use for this project).
  - And here is an article 
from Digital Ocean [about the different types of OAuth2 flows](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)
which was recommended to me by someone with more OAuth2 experience than I 
have.

  This was also a chance for me to work directly with the API, 
  as there isn't a library available that I'm aware of. In contrast, when 
  I've previously worked with Salesforce's APIs I used the 
  `simple_salesforce` Python package, which worked well and which I was 
  grateful for, but it did introduce a layer of abstraction that led to a 
  slightly more superficial understanding.
 
- I had another helpful informational interview with a data scientist doing 
machine learning. From this, I realized that I want to test whether I'm
interested in machine learning, because that will influence my learning path.
He recommended Andrew's Ng's [Machine Learning Coursera course](https://www.coursera.org/learn/machine-learning).
I respect this person's recommendation because he has many years of 
programming experience, completed a data science masters degree at a 
prestigious university, and is working in the industry. Although the course 
material is fairly old, he thinks that Andrew explains the material really 
well. It's a 55-hour course (free!) and I've recently gotten started on it.

- Finally, another client I've been assisting with work that's tangentially 
related to programming has more directly involved me in programming. 
I've been getting my toes wet with Ruby on Rails and it's my first time 
working 
with a production web app. It's been interesting trying to wrap my brain 
around all the parts of a web app (still more to learn!) and to see how 
things are set up at a startup where the founders are all accomplished 
developers.