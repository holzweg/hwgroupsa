Holzweg Group Site Access Extension
=======

What is the Group Site Access Extnsion?
----------------------------------------------------------
This extension enables you to use subdirectories inside your siteaccess settings directories to create additional overrides to siteaccess settings (e.g. for different languages)

&rarr; This extension is for those of you using multi site implementations (e.g. 3 different websites with 5 different languages each)

How does it work?
----------------------------------------------------------
hwgroupsa overrides two kernel files (ezsiteaccess.php and ezini.php) to push the subdirectory's settings (further referred to as "sub-siteaccess settings" to the settings override array.

Additionaly, it provides a custom language switcher to allow switching between sub-siteaccesses, while not leaving the main siteaccess.

A new MatchOrder Setting was introduced in the site.ini settings, to allow an easy setup for multi-site-multi-language installations (see in the configuration section)

Installation:
----------------------------------------------------------

1. Clone this repository into your extension directory

2. Activate kernel overrides in your {ezpublish-root}/config.php (this file eventually needs to be created)

        <?php
        define( 'EZP_AUTOLOAD_ALLOW_KERNEL_OVERRIDE', true );
        ?>

3. Activate the extension from the ezpublish backend (or override/site.ini.append.php)

4. Regenerate your autoload array (don't forget the "-o" flag to override kernel and lib classes)

        $ bin/php/ezpgenerateautoloads.php -o

Configuration:
----------------------------------------------------------

1. Update your settings/override/site.ini.append.php

        MatchOrder=host_uri_group
        HostUriGroupMatchMapItems[]
        HostUriGroupMatchMapItems[]=www.website1.com;de|en|it;website1
        HostUriGroupMatchMapItems[]=www.website2.com;de|en|it;website2
        HostUriGroupMatchMapItems[]=www.website3.com;de|en|it;website3

        The Syntax for each HostUriGroupMatchMapItems is:
        [hostname];[sub-siteaccess1]|[sub-siteaccess2]|[...];[main-siteaccess]

2. Create the directory structure

        settings/siteaccess/website1
        settings/siteaccess/website1/de
        settings/siteaccess/website1/en
        settings/siteaccess/website1/it
        settings/siteaccess/website2
        settings/siteaccess/website2/de
        settings/siteaccess/website2/en
        settings/siteaccess/website2/it
        settings/siteaccess/website3
        settings/siteaccess/website3/de
        settings/siteaccess/website3/en
        settings/siteaccess/website3/it

3. Setup site.ini.append.php

        in each main siteaccess, create a site.ini.append.php just like you normally would

        in each sub-siteaccess, only create those settings files that need to override the main siteaccess:

        settings/siteaccess/website1/de/site.ini.append.php:

        [RegionalSettings]
        Locale=ger-DE
        ContentObjectLocale=ger-DE
        SiteLanguageList[]
        SiteLanguageList[]=ger-DE
        SiteLanguageList[]=eng-US
        SiteLanguageList[]=ita-IT

5. Kick back, clear the cache and enjoy! (:

### Feedback and Feature Requests
We're happy to receive your feedback at technik[at]holzweg.com

Please feel to contribute by contacting us or simply sending us a pull request.

### Initially brought to you by Holzweg e-commerce Solutions, with love. ###
Note: No kernel files were harmed during the development of this extension.

### Contributions by ###
(this could be you!)

(For more document and questions please visit http://github.com/holzweg/hwgroupsa)

Tak!