# Gravity Forms Worpdress Plugin - enhanced UI dropdown fix for mobile

Gravity Forms (https://www.gravityforms.com/) is an awesome plugin to create forms. It is easy to create fields and use custom configurations.

But it has a problem nowadays for mobile devices. Gravity Forms still uses `Chosen` jQuery script to enhance dropdown fields (if you check this option in the dropdown options, in form editor).

Chosen was a great script in the past, to make enhanced dropdown fields. I was a big fan of this jquery plugin in the past! But nowadats there is no sense to continue with it, since Chosen **does not work with Mobile devices**. There is a good options to use intead, but this is another thing to discuss.

Luckyly, [@swentel](https://github.com/swentel) faced this problem too and blogged about a fix for that https://realize.be/blog/mobile-support-chosen. I just adapted it to make it work ok with Gravity Forms.

## Instructions

You just need to put the `.js` to your theme's folder and add the following function into `functions.php` (just paste it at end of file or in another place of your preference).

```php
/**
 * Fix for chose not working on mobile devices.
 */
function [themes name]_fix_gform_chosen_mobile() {
	wp_deregister_script('gform_chosen');
	wp_register_script('gform_chosen', path_join(get_stylesheet_directory_uri(), 'js/chosen.jquery.fix.min.js'), ['jquery'], '1.10.0-fix');
}

add_action('init', '[themes name]_fix_gform_chosen_mobile', 11); 
```

 * In the case above, I put the Javascript file in `[themes folder]/js` folder.
 * I choose to use priority `11` since Gravity Forms source code adds at default Wordpress position `10`. 

## Notes

* The Chosen plugin version used is `1.10.0`. The lasted version so far (Jan 2019) is `1.8.7`. Feel free to add the fix and pull request me the updated version.
* It is a simple fix, I didn't want to make a complex fix. In my case it was not necessary, because the site I faced the problem was a simple one.
* The Chosen author is not interested to make a mobile version, for a series of reasons. Don't blame him, every dev has his own reasons for that.
* This is a shared solution, feel free to fork and contribute! :D
