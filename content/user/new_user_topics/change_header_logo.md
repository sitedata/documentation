---
title: How do I change the logo or the logo alt text in the header?
description: Customizing your logo 
category: new_user_topics
weight: 10
aliases: 
    - /user/new_user_topics/change_powered_by/
---

## Storefront Header 

By default, Zen Cart uses `includes/templates/YOURTEMPLATE/images/logo.gif` for the filename of the logo image, but you can use your own filename for the logo.

**NOTE:** If your logo is already available as a .gif image, it's faster to just upload your logo by naming the file as logo.gif and replacing the logo.gif file on the server. Then refresh your browser cache (CTRL+R) to see it on your site. You may still want to update the image dimensions listed in the following instructions.

Using an [image editor](/user/first_steps/useful_tools/#graphics-editors), create your new logo and save it to `includes/templates/YOURTEMPLATE/images/yourname` and upload it to your server.

The name `yourname` will also include a file extension, such as `.png`, `.jpg`, etc. 

After creating your logo you can adjust the alt text, width, height, and image name in `includes/languages/english/YOURTEMPLATE/header.php`

**NOTE:** If you don't have the file `includes/languages/english/YOURTEMPLATE/header.php`, then copy `includes/languages/english/header.php` to `includes/languages/english/YOURTEMPLATE/header.php` before editing.  See [What if I don’t have a file that some instructions mention?](/user/new_user_topics/no_such_file/)

For the purpose of this example, let's assume `yourname` is `newlogo.png`, and that the logo is 200px wide and 80px tall.

```
define('HEADER_ALT_TEXT', 'My new alt text');
define('HEADER_LOGO_WIDTH', '200'); // this is the number of pixels
define('HEADER_LOGO_HEIGHT', '80'); // this is the number of pixels
define('HEADER_LOGO_IMAGE', 'newlogo.png');
```

Save this file and upload it to your server. 

By default, the logo is left aligned. Changing the alignment involves making a modification to your `includes/templates/YOURTEMPLATE/css/stylesheet.css`. 

Open the file and find the following:

```
#logo, .centerBoxContents, .specialsListBoxContents, .categoryListBoxContents, .centerBoxContentsAlsoPurch, .attribImg {float: left;}
```

Since this is a collection of several “selectors” (#logo, .centerBoxContents, etc) and in order not to interfere with the layout of other sections, split this into two separate statements and create a new selector/definition below it, like this:

```
.centerBoxContents, .specialsListBoxContents, .categoryListBoxContents, .centerBoxContentsAlsoPurch, .attribImg {float: left;}

#logo {float: left;}
```

To center the logo use `text-align: center;`

To right align the logo use `float: right;`

## Admin Header 
A similar change should be made in `admin/includes/languages/english.php`, which contains the same four PHP define statements. You might use a different image in your admin. The filename mentioned here refers to a *different* file and location than the one used above for the storefront. See notes below.

```
define('HEADER_ALT_TEXT', 'My new alt text');
define('HEADER_LOGO_WIDTH', '200');
define('HEADER_LOGO_HEIGHT', '80');
define('HEADER_LOGO_IMAGE', 'newlogo.png');
```

The image itself should be placed in the `admin/images/` folder.
See [Using your logo on packing slips and invoices](/user/orders/high_res_logo) for more details.

## Image Caching 

The reason the instructions above recommend using the new name `newlogo.png` is to ensure that the cache isn't used.

If you simply replace `includes/templates/YOURTEMPLATE/images/logo.gif` with your own logo using the same filename, your browser will likely not pick up the change immediately because of [browser caching](/user/new_user_topics/browser caching/).

## Related Articles 
- [Logos in HTML emails](/user/email/logo/) 
- [Using your logo on packing slips and invoices](/user/orders/high_res_logo)
