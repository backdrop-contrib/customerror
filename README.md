Custom Error
============

This module allows Backdrop site admins to create custom error pages for HTTP
status codes 403 (access denied) and 404 (not found) without creating nodes, and
custom 404 redirect rules.

Features:

* Configurable page title and descriptions.
* There are no author and date/time headers unlike normal nodes.
* Any HTML formatted text can be be put in the page body.
* The error pages are themeable.
* Users who are not logged in and try to access an area that requires
  login will be redirected to the page they were trying to access after
  they login.
* Allows custom redirects for 404s.

Since the error pages are not real nodes, they do not have a specific content
type, and will not show up in node listings.

At present, the module can be set up to handle 403 and 404 errors, however the
design of the module is flexible and can accommodate future error codes easily.

Installation
------------

- Install this module using the official Backdrop CMS instructions at
  https://backdropcms.org/guide/modules.

- Visit the configuration page under Administration > Configuration > System >
  Custom error (admin/config/system/customerror) and customize as you like. You
  can use any HTML tags to format the text.

- Now, if you go to a non-existent page on your Backdrop site, then you should
  see your custom error page for 404 (not found) page.

Custom redirects for 404 errors
-------------------------------

It is possible to set up custom redirects for status code 404 (not found).

For example, if you had a page called foo and a page called xyz, then you moved
them to a page called bar, and abc respectively, then setup the redirect rules:

  ^foo$ bar
  ^xyz$ abc

The first rule will redirect visitors of example.com/foo to example.com/bar. The
second rule will redirect all requests to example.com/xyz to example.com/abc.

You can have multiple pairs of redirects. Each must be on a line by itself.

Note that the first argument is a regexp, and the second argument is a path. You
have to use one space between them, and enter each pattern on a line by itself.

FAQ
---

Q: I want to prevent robots from indexing my custom error pages by
   setting the robots meta tag in the HTML head to NOINDEX.\
A: There is no need to. CustomError returns the correct HTTP status
   codes (403 and 404). This will prevent robots from indexing the
   error pages.

Q: I want to customize the custom error template output.\
A: In your site's theme, duplicate your page.tpl.php to be
   page--customerror.tpl.php and then make your modifications there.

Q: I want to have a different template for my 404 and 403 pages.\
A: Duplicate your page.tpl.php page to be
   page--customerror--404.tpl.php and
   page--customerror--403.tpl.php. You do not need a
   page--customerror.tpl.php for this to work.

Q: Some 403 errors (e.g. "http://example.org/includes") are served by
   the Apache web server and not by CustomError. Isn't that a bug?\
A: No. CustomError is only designed to provide a custom error page
   when the page is processed by Backdrop.  The .htaccess file that
   comes with Backdrop will catch some attempts to access forbidden
   directories before Backdrop even see the requests.  These access
   attempts will get the default Apache 403 error document, unless you
   use the Apache ErrorDocument directive to override this, e.g:
   ErrorDocument 403 /error/403.html For more information about this,
   see: http://httpd.apache.org/docs/current/custom-error.html

Q: I want to implement a custom page for another error code.\
A: Please contact [AltaGrade](https://www.altagrade.com) for customizations of
   this module as well as Backdrop consulting, installation, development, and customizations.

Issues
------

Bugs and Feature requests should be reported in the Issue Queue:
https://github.com/backdrop-contrib/customerror/issues.

Current Maintainers
-------------------

- [Alan Mels](https://github.com/alanmels).

Credits
-------

- Ported to Backdrop CMS by [Alan Mels](https://github.com/alanmels).
- Originally written for Backdrop by [Khalid Baheyeldin](https://github.com/kbahey).

License
-------

This project is GPL v2 software.
See the LICENSE.txt file in this directory for complete text.
