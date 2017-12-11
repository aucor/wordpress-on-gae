---
layout: default
title: Why we chose Google App Engine
---

On our company we didn't have the afford to use sysadmins to manage our servers. This became a problem, because our hosting abilities didn't match our service level and quality. In addition, we had the typical server-based LAMP structure, which meant that there were multiple sites running on the same server. When PHP or database went kaput due to the high load, our phones started to ring. Not funny.

On summer 2013 we started to scout different solutions. In addition to Google we tested Joyent, Amazon, Rackspace, Digital ocean, Linode (our awesome hosting provider at that time), Heroku and some smaller and national hosting providers. Every one of those had very nice solutions, with different strong points and caveats. In the end, selection was between Amazon and Google. At that time, Amazon had more mature ecosystem, but there were clear signs that Google was coming fast to their turf. And if we would have chosen Amazon, there wouldn't have been any noticable difference on web development. We still would have needed to use constant sysadmin services.

On August 2013 we made the strategic decision to migrate our sites to Google App Engine (and in general, Google Cloud Platform). After we deployed our first pages to Google App Engine, there was some problems, but nothing we couldn't manage. Documentation was (and still is on many accounts) lacking, because PHP has never been high on Google's priorities. After ironing out the worst kinks, we were happily deploying our sites to the Google App Engine.

After the site is up and running on WordPress, it's pretty much fire & forget. We haven't had a single downtime on our applications since 2013, and no latency variations either.
