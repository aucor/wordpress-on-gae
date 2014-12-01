---
layout: default
title: Speed optimization
---

On our production sites we have noticed that speed isn't Google App Engine's strong suite. Sure you can (and should) tweak the application and SQL settings for your needs, but we prefer to have even more "umpf". There are many ways to speed up Google App Engine sites, here are some of them.

## Google App Engine settings

### Google Page Speed

## Google SQL settings

### Asynchronous vs. Synchronous

##Theme layer and WordPress optimization

### Caching

"Cache all the things" is a key rule when developing fast websites. WordPress has few different levels for caching and you should use all of them. App Engine provides us [Memcached](https://cloud.google.com/appengine/docs/adminconsole/memcache), a superfast caching backend. Memcache is a separate service that is accessible from all the App Engine instances. So when a new instance of our site spins up it can immediately access previously cached data.

The starter project includes [Batcache](https://wordpress.org/plugins/batcache/) (advanced-cache.php) and simple [Memcached object cache](https://github.com/jeremyfelt/Memcached-Object-Cache) (object-cache.php) together with Batcache manager plugin. Batcache caches full html pages, so the response is quite immediate. The Batcache Manager helps invalidating the cache, but can only handle simple cases. So we can't use lifetime long cache times. We've been using times from 30 minutes to 2 hours depending the site contents and activity.

Object cache stores - wait for it - objects! So instead of hitting the database we get the details of an object from cache. But we've noticed that complex pages can hit the memcache up to few thousand times and even the cache is fast, we end up having quite a lot of network latency. So we need something more clever.

Wordpress has a nice API for for ones own caching called [transients](http://codex.wordpress.org/Transients_API). WP uses transients internally but they're very easy to use when developing sites. Using transients we can cache bigger parts of the site that stay same from page to page and change infrequently. (TODO: Add code examples)

#### Caching plugins

[Voce Connect](http://afterburner.voceplatforms.com/back-end.html) has developed a bunch of performance related plugins. These two are our favourites:

[Voce Cached Nav](https://wordpress.org/plugins/voce-cached-nav/) caches (not so surprisingly) navigation menus. It's very easy to use, just replace the calls for wp_nav_menu with the plugin's alternative. Plugin handles the active and parent item classes, so we're good. Just faster. And that is awesome, since WordPress' menus are a pain in the performance ass.

Another epic surpise: [Voce Widget Cache](https://wordpress.org/plugins/voce-widget-cache/) caches widgets. The usage requires a bit work but also allows quite sophisticated invalidation mechanisms. If you need some page specific visibility rules, at least the JP Widget Visibility plugin works fine together with Voce Widget Cache.

##External solutions
Our production stack includes external reverse proxy (Varnish) server for caching static content. This way we get the scalability of Google App Engine and lightning fast response times. Of course, we have a robust DNS-management stack for overriding the Varnish-server if there are huge amounts of traffic. After this happens, Google App Engine takes the hit and scales instances accordingly.
