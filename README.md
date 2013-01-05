Overview
========

These scripts will automatically replace all SVG images on the page (using an img tag with a .svg extension) with a fallback format when SVG is not supported by the browser. If the image has the attribute data-svg-fallback, it replaces the image src with that value. If it doesn't have that attribute it sets the image src to the same filename but with a .png extension. Therefore, if you intended to use .svg images, you should either provide an alternative via the data-svg-fallback attribute or by putting a .png image with the same name in the same directory.

Both versions work the same way and the the only difference is whether or not it uses jQuery.

*Note:* The jQuery version can be placed anywhere in the document as long as jQuery has been defined. It uses DOM-Ready so either the header or bottom of the body tag will work (though JS is always best at the end of the document.) The non-jQuery version *must* be used at the end of the body tag to work properly or adapted to be used in a window.onload or some other DOM-Ready handler.

Examples
========

If you place a .png file will the same name in the same directory as your .svg images, just a normal image tag will do:

    <img src="images/logo.svg" />

becomes

    <img src="images/logo.png" />

If you use a different extension for your fallback images or put them a different directory, use the data-svg-fallback. So

    <img src="images/logo.svg" data-svg-fallback="images/fallback/logo.jpg" />

becomes

    <img src="images/fallback/logo.jpg" />

If your browser supports SVG images the only thing that changes is that the 'svg' class is added to the body element on the page for other CSS/scripts to use.

Using for CSS background images
===============================

The script will add either an svg or no-svg class to the body element, which you can use in your CSS rules to specify which version to use. Here's an example:

    <style>

      h1.logo {
        background: url(logo.svg);
      }

      body.no-svg h1.logo {
        background: url(logo.png);
      }

    </style>

This example will use logo.svg as the background image for h1.logo when SVG is available and logo.png when not. (Other styles removed to simplify the example.)

Note for Ruby on Rails and the Asset Pipeline
=============================================

If you are using Rails and the asset pipeline you should put your images in the page doing something like this:

    <%= image_tag "logo.svg", {:"data-svg-fallback" => "#{image_path('logo.png')}", :alt => "Use an alt value for images!"} %>

Just using the default behavior of automatically using a .png extension for the same file path won't work when the asset pipeline adds the digest to the filename during asset compilation.

Credits
-------

Adapted from Thomas Fuchs' example at https://gist.github.com/3202087