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


## <a name="gravityforms-gae-file-upload"></a>Gravity Forms
[Gravity Forms](http://www.gravityforms.com) is an awesome plugin for creating forms on WordPress. However, we noticed that Gravity Forms doesn't support uploading files to Google Storage. We wrote our own plugin for enabling this.

[Download plugin from WordPress.org](http://wordpress.org/plugins/gravityforms-file-upload-for-gae/)

#Test & tried
August 2014 it became possible to use Cloud SQL replicas. This means that it is now possible for read-intensive applications to distribute load to multiple databases. 

[HyperdDB](https://wordpress.org/plugins/hyperdb/) is a nice and mature plugin for managing multiple MySQL-databases for WordPress. Using HyperDB you can distribute database load to master/slave-combinations. For example, you could use master for writing and multiple slaves for reading. In addition, you can distribute reads/writes to database table level, too. 

It seems to work properly based on a short test. Use same Google Cloud SQL settings on db-config.php as you would normally use (and remember, user is 'root' and no password). 

#Will not work on Google App Engine
Not sure if this section is necessary. As a rule of thumb, most plugins that need to write to a local filesystem will not work on Google App Engine, unless they are modified to use Google Cloud Storage instead. And even then, it might not work. ;)

##Revslider
Revslider is a popular plugin for creating sliders. Revslider requires a way to access slider_settings.xml (and something else too, we are not sure what else), but for some reasons plugin can't read the xml properly. 