### Disable wp-admin/plugins.php Page For All:
	* So that no One can Download My Plugins when I send the wp-admin login for test

### Place the Below Code in wp-config.php

```php

// place this after WP_DEBUG

define('DISALLOW_FILE_MODS', true);

// place this after require_once ABSPATH . 'wp-settings.php';

// ----------------------------------------------------------

// No one can download plugin from plugin page

// ---------------------------------------------------------

function remove_plugins_menu() {
    remove_menu_page('plugins.php');
}
add_action('admin_menu', 'remove_plugins_menu');

function redirect_from_plugins_page() {
    if (is_admin() && strpos($_SERVER['SCRIPT_NAME'], 'wp-admin/plugins.php') !== false) {
        wp_safe_redirect(admin_url()); // Redirect to the admin dashboard
        exit();
    }
}
add_action('admin_init', 'redirect_from_plugins_page');


// ----------------------------------------------------------

// No one can download plugin from plugin page

// ---------------------------------------------------------


```