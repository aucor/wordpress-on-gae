---
layout: default
title: Plugins
---

This is our plugin stack for Google App Engine. Naturally we use other plugins too, but these are the most relevant ones.

Due to the Google App Engine restrictions (most importantly, writing to a local file system isn't possible) some plugins won't work on Google App Engine. If the plugin requires to write on file system, or if the plugin generates outbound requests, it usually won't work on Google App Engine. 


#Critical

There is really only one critical plugin:

## Google App Engine plugin (official)
[Google App Engine for WordPress](https://wordpress.org/plugins/google-app-engine/) is a must. Plugin handles writing and reading of data to Google Storage bucket automatically, and the plugin handles email requests too.

#Essential

These plugins are essential for using WordPress on a Google App Engine environment.

##WP-Mail-SMTP
You cannot send mail from Google App Engine like you usually could on a normal VM environment. Mail requests are handled by Google. Due to this, it is generally wise to use external mail service. We use [SendGrid](http://sendgrid.com), and use [WP-Mail-SMTP plugin](http://wordpress.org/plugins/wp-mail-smtp/) to handle the mail traffic.


## <a name="gravityforms-gae-file-upload">Gravity Forms 
[Gravity Forms](http://www.gravityforms.com) is an awesome plugin for creating forms on WordPress. However, we noticed that Gravity Forms doesn't support uploading files to Google Storage. We wrote our own plugin for enabling this.

[Download plugin from WordPress.org](http://wordpress.org/plugins/gravityforms-file-upload-for-gae/)

#Will not work on Google App Engine

##Revslider
Revslider is a popular plugin for creating sliders. Revslider requires a way to access slider_settings.xml (and something else too, we are not sure what else), but for some reasons plugin can't read the xml properly. 