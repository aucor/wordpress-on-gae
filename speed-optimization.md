---
layout: default
title: Speed optimization
---

On our production sites we have noticed that speed isn't Google App Engine's strong suite. Sure you can (and should) tweak the application and SQL settings for your needs, but we prefer to have even more "umpf". There are many ways to speed up Google App Engine sites, here are some of them.

# Google App Engine settings

## Google Page Speed

# Google SQL settings

# Asynchronous vs. Synchronous

#Theme layer and WordPress optimization

#External solutions
Our production stack includes external reverse proxy (Varnish) server for caching static content. This way we get the scalability of Google App Engine and lightning fast response times. Of course, we have a robust DNS-management stack for overriding the Varnish-server if there are huge amounts of traffic. After this happens, Google App Engine takes the hit and scales instances accordingly.
