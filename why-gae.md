---
layout: default
title: Why GAE?
---

If you want to know why we chose WordPress, read [this](http://aucor.github.io/wordpress-on-gae/why-we-chose-google-app-engine.html).

#Why Google App Engine

## Costs
Google App Engine is not cheap, but it has a very competitive cost structure considering the scalability and ease of use. 


## Scalability
This is where the Google App Engine + WordPress shines. On our experience, we haven't had any problems with Google App Engine and WordPress scalability. Site can take easily 70 000 queries per second, without any performance issues. 

## Security

## Easy and fast development

## This is the future

Time of server tweaking is over. On our client segment (WordPress) there is no actual need to own/rent servers. Using a PaaS like Google App Engine is the best way to create robust and reliable solutions for the modern world.


# Caveats

Google App Engine is no silverbullet to any particular problem. It is a good platform that can be used to build robust and highly scalable applications with low effort and relatively cheaply. Using WordPress there is bound to be some problems, and on this site we try solve them as best we can. 

##No writing to a local filesystem

##Database latency
This isn't just a Google App Engine problem. One might say it is a feature. ;) When using highly scalable systems, part of the whole idea is that databases and instances can (and most likely, will) be on different geographic locations. This means that there will be latency, no matter what you do. 

# Conclusion

## When to use Google App Engine + WordPress

## When NOT to use Google App Engine + WordPress
* If you need a WordPress solution that has plenty of database queries and no way to optimize them, you may have better results using some framework or some other platform/hosting solution.
* If you need a WordPress multisite with domain mapping. It's a no go.
* If you need to preprocess images using WordPress media gallery (only square blocks, sorry).



