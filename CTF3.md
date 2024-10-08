Week 3

Wordpress version: 5.8.1

### Installed plugins and their versions:
To find the installed plugins, we inspected the source code of the site.
- Woocommerce 5.7.1 (src="http://143.47.40.175:5001/wp-content/plugins/woocommerce/assets/js/frontend/woocommerce.min.js?ver=5.7.1")
- Mstore-api 1.0.0 (src="http://143.47.40.175:5001/wp-content/plugins/mstore-api/assets/js/mstore-inspireui.js?ver=1.0.0")

### Possible users and usernames:
- To discover the user with id=1, we added "/?author=1" to the site URL, where we found that this user was "admin."
- By testing "/?author=2," the site was redirected to the "shop." Thus, we concluded that id 2, although it exists, may be linked to a user with another role, likely related to WooCommerce.
- No additional users were found with the remaining ids we tested.

### Vulnerability research:
#### Woocommerce5.7.1 : CVE-2020-36326
WordPress versions 3.7 to 5.7.1 use a vulnerable version of the PHPMailer library, which has a PHP Object Injection vulnerability due to improper sanitization of user input before it is passed to the unserialize() function. This can allow remote attackers to inject and execute arbitrary code within the affected web server process.

