---
layout: default
title: Building the site
---

## Image styles

Since we can't write to the disk on GAE, uploads are stored in Google Cloud Storage (GCS). The App Engine plugin takes care of uploading the images into the bucket and generating the public urls for them. Every image gets a default url in form of <code>http://<em>bucketname</em>.storage.googleapis.com/<em>filename.jpg</em></code>. But when embedded into a post or displayed through <code>post_thumbnail</code> functions the plugin fetches the gibberish and unpronounceable CDN powered public serving url based on the image style.

Unlike in "regular" WordPress installations the different image style files are not generated when the image is uploaded. Instead only the original file is stored in the bucket and the different sized are generated (and cached until eternity) on the first request somewhere in the GCS internals. And at this point we sometimes reach the limits of the image handling capabilities of the GCS. The following might not affect your site at all, especially if your editing the images to right dimensions before uploading, but sometimes we have found these a bit confusing and disturbing.

### Resizing

In GCS the images can be [resized or cropped](https://cloud.google.com/appengine/docs/php/refdocs/files/google.appengine.api.cloud_storage.CloudStorageTools#\google\appengine\api\cloud_storage\CloudStorageTools::getImageServingUrl()), but only with one dimensional argument. So when resizing only the longer dimension of the image style is used as the argument. e.g. with image style specified as 600px wide and 400px tall (with no force crop), you'll normally get an image that in its original aspect ratio fits inside a 600&times;400 box, but in GCS it will be fitted into a 600&times;600 box. See the following image for a couple more problematic examples.

![Resizing images on GCS](/wordpress-on-gae/assets/img/resizing-images-on-gcs.png)

<small>Photo credit: Anssi Koskinen / Aucor Oy</small>

### Force crop and a workaround using intrinsic ratios

Cropping is even worse. GCS can only crop images into a square using the longer dimension of the image style as the size argument. The result is far from expected behaviour of WordPress' image styles. See the image below for examples.

![Cropping images on GCS](/wordpress-on-gae/assets/img/cropping-images-on-gcs.png)

<small>Photo credit: Anssi Koskinen / Aucor Oy</small>

Since force cropped image styles are usually used as featured images, avatars, image galleries or in some other special places we can mitigate the issue of cropping in our theme. This is done by using an extra wrapper div around the image and the concept of [intrinsic ratios](http://alistapart.com/article/creating-intrinsic-ratios-for-video). So we'll force the wrapper div to dimensionally behave as we want the correctly sized image behave and handle the possibly wrong sized image inside this container.

As an example we have a featured image spot that is 500px wide and 200px tall. Normally we would specify the image style to this size with force crop option. But in GAE it is better to leave the force crop off since otherwise we would always get 500&times;500 sized images. Not good. Without force crop we get image that is 500px wide and less than 500px tall. Or at least until some dumbass uploads a portrait image to be used in landscape spot, so please leave some instructions for the admins.

<div data-height="268" data-theme-id="11064" data-slug-hash="NPbRJa" data-default-tab="css" data-user="underdude" class='codepen'><pre><code>.main-container {
  // You also need a parent container to limit the width
  max-width: 500px;
  margin: 1em auto;
}
.intrinsic-image-wrapper {
  width: 100%;
  height: 0;
  padding-bottom: percentage(200/500); // Alter this to match the desired aspect ratio
  position: relative;
  overflow: hidden;

  img {
    // The absolute center everything trick: http://www.smashingmagazine.com/2013/08/09/absolute-horizontal-vertical-centering-css/
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
    width: 100%;
  }
}</code></pre>
<p>See the Pen <a href='http://codepen.io/underdude/pen/NPbRJa/'>Force an image to specific size using intrinsic ratio</a> by Janne Ala-Äijälä (<a href='http://codepen.io/underdude'>@underdude</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
</div><script async src="//assets.codepen.io/assets/embed/ei.js"></script>

### Conclusions

And as a bonus the GCS generated image sizes are limited to 1600px. This probably won't affect unless your having huge full size background image sliders with superb retina resolution images that are managed from the WordPress admin. And that might be a bad idea anyway.

So when setting up image styles (or when some plugin sets up its own ones) know the limits of GCS.

### And one more thing: The devserver issue

It's important to notice that in local development environment, the plugin always returns the url of the original image. This means that the image isn't resized nor cropped accordingly to the desired image style. This may cause some unexpected situations when developing or deploying so be careful.
