## Week 3

### Wordpress version: 5.8.1

### Installed plugins and their versions:
To find the installed plugins, we inspected the source code of the site.
- Woocommerce 5.7.1 (src="http://143.47.40.175:5001/wp-content/plugins/woocommerce/assets/js/frontend/woocommerce.min.js?ver=5.7.1")
- Mstore-api 1.0.0 (src="http://143.47.40.175:5001/wp-content/plugins/mstore-api/assets/js/mstore-inspireui.js?ver=1.0.0")

### Possible users and usernames:
- To discover the user with id=1, we added "/?author=1" to the site URL, where we found that this user was "admin."
- By testing "/?author=2," the site was redirected to the "shop." Thus, we concluded that id 2, although it exists, may be linked to a user with another role, likely related to WooCommerce.
- No additional users were found with the remaining ids we tested.

### Vulnerability research:

##### Woocommerce5.7.1 : CVE-2020-36326
WordPress versions 3.7 to 5.7.1 use a vulnerable version of the PHPMailer library, which has a PHP Object Injection vulnerability due to improper sanitization of user input before it is passed to the unserialize() function. This can allow remote attackers to inject and execute arbitrary code within the affected web server process.

#### Mstore-api 1.0.0 : CVE-2023-2732
CVE-2023-2732 is a critical vulnerability in the MStore API plugin for WordPress, allowing unauthenticated attackers to bypass authentication and impersonate users, including administrators. It has a severity score of 9.8/10. The issue is fixed in version 3.9.3​

##### We found the above vulnerability the most relevant to our goal, but we also found the following in Mstore-api 1.0.0: 

- CVE-2024-8269
- CVE-2024-8242
- CVE-2024-7628
- CVE-2024-6328
- CVE-2023-3277
- CVE-2023-3209
- CVE-2023-3203
- CVE-2023-3202
- CVE-2023-3201
- CVE-2023-3200
- CVE-2023-3199
- CVE-2023-3198
- CVE-2023-3197
- CVE-2023-3077
- CVE-2023-3076
- CVE-2023-2734
- CVE-2023-2733
- CVE-2021-24148
- CVE-2020-36713
 
 ### Chosen vulnerability and exploitation
 
 ##### Mstore-api 1.0.0 : CVE-2023-2732
 We found this vulnerability to be the most useful when logging as another user. After researching about it, we found an exploit, by entering "http://143.47.40.175:5001/wp-json/wp/v2/add-listing?id=1" we were able to log as the admin user. After finding the private post, we found the flag: flag{byebye} :)

Sources:
- https://github.com/RandomRobbieBF/CVE-2023-2732?tab=readme-ov-file
- https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=wordpress+mstore

