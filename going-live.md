---
layout: default
title: Going live
---

##Custom domain

Serving you site on a custom domain came a lot easier a while ago. Now the custom domain can be added through the Cloud Console, under the App Engine settings page on a "Custom Domains" tab. This is nicely in [documented](https://cloud.google.com/appengine/docs/domain), so read more there.

The App Engine WordPress plugin forces the wp-admin to use https, so if you wan't to access your administration area through <em>yourdomain.com</em>/wp-admin and don't serve the site with SSL, you should either comment the lines from the App Engine plugin (lines 63 and 64 on <code>modules/core.php</code>) or revert the settings elsewhere.

###Naked domain redirect

At some point it wasn't possible to assign the app to a naked domain (a url without www) and even now we suggest that you use the www-subdomain for your app to make things easier, since you can't do both very nicely. But obviously we wan't the naked domain to work too and for SEO purposes we wan't it to redirect to the www-version so we won't have the double content issue.

There are few options how to achieve this. Our own DNS provider has a service for this, so we can handle these redirects like any other DNS records. Under the hood it uses nginx to redirect the requests, and that's an option for you too. But it might be silly to maintain a server just for www-redirects. Luckily there is a free service for this one: [wwwizer](http://wwwizer.com/naked-domain-redirect)! You just point the A record the their IP address and thats it. No registrations or configurations needed, they just forward every request wwwized one.

##Custom domain with SSL

This is currently a bit of a mess. Despite Googles efforts to https the whole internet and the fact that every App Engine app gets a secure appspot.com-subdomain, adding your own domain with your own certificate is too complicated.

The process is a bit loosely documented ([here](https://cloud.google.com/appengine/docs/ssl) and [here](https://support.google.com/a/answer/2644334), but the most important thing to notice: You will need a Google Apps account with the desired domain as the primary domain. So if the domain uses Google Apps already for emails etc, you will need an administrator access to that one.

Why there just can't be a checkbox "Enable SSL, +10$/month" :)