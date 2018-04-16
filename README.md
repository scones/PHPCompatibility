PHP Compatibility Coding Standard for PHP CodeSniffer
=====================================================
[![Latest Stable Version](https://poser.pugx.org/wimg/php-compatibility/v/stable.png)](https://packagist.org/packages/wimg/php-compatibility)
[![Latest Unstable Version](https://poser.pugx.org/wimg/php-compatibility/v/unstable.png)](https://packagist.org/packages/wimg/php-compatibility)
![Awesome](https://img.shields.io/badge/awesome%3F-yes!-brightgreen.svg)
[![License](https://poser.pugx.org/wimg/php-compatibility/license.png)](https://github.com/wimg/PHPCompatibility/blob/master/LICENSE)
[![Flattr this git repo](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=wimg&url=https://github.com/wimg/PHPCompatibility&title=PHPCompatibility&language=&tags=github&category=software)

[![Build Status](https://travis-ci.org/wimg/PHPCompatibility.png?branch=master)](https://travis-ci.org/wimg/PHPCompatibility)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/wimg/PHPCompatibility/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/wimg/PHPCompatibility/)
[![Coverage Status](https://coveralls.io/repos/github/wimg/PHPCompatibility/badge.svg?branch=master)](https://coveralls.io/github/wimg/PHPCompatibility?branch=master)

[![Tested Runtime Badge](http://php-eye.com/badge/wimg/php-compatibility/tested.svg?branch=dev-master)](http://php-eye.com/package/wimg/php-compatibility)


This is a set of sniffs for [PHP CodeSniffer](http://pear.php.net/PHP_CodeSniffer) that checks for PHP version compatibility.
It will allow you to analyse your code for compatibility with higher and lower versions of PHP. 


PHP Version Support
-------

The project aims to cover all PHP compatibility changes introduced since PHP 5.0 up to the latest PHP release. This is an ongoing process and coverage is not yet 100% (if, indeed, it ever could be). Progress is tracked on [our Github issue tracker](https://github.com/wimg/PHPCompatibility/issues).

Pull requests that check for compatibility issues in PHP 4 code - in particular between PHP 4 and PHP 5.0 - are very welcome as there are still situations where people need help upgrading legacy systems. However, coverage for changes introduced before PHP 5.1 will remain patchy as sniffs for this are not actively being developed at this time.

Requirements
-------

* PHP 5.3+ for use with PHP CodeSniffer 1.x and 2.x.
* PHP 5.4+ for use with PHP CodeSniffer 3.x.

PHP CodeSniffer: 1.5.6, 2.2.0+ or 3.0.2+.

The sniffs are designed to give the same results regardless of which PHP version you are using to run PHP CodeSniffer. You should get reasonably consistent results independently of the PHP version used in your test environment, though for the best results it is recommended to run the sniffs on PHP 5.4 or higher.

PHP CodeSniffer 1.5.6 is required for 90% of the sniffs, PHP CodeSniffer 2.6.0 or later is required for full support, notices may be thrown on older versions.

As of version 8.0.0, the PHPCompatibility standard can also be used with PHP CodeSniffer 3.x.


Thank you
---------
Thanks to all [contributors](https://github.com/wimg/PHPCompatibility/graphs/contributors) for their valuable contributions.

[![WPEngine](https://cu.be/img/wpengine.png)](https://wpengine.com)

Thanks to [WP Engine](https://wpengine.com) for their support on the PHP 7.0 sniffs.


:warning: Upgrading to PHPCompatibility 8.0.0 :warning:
--------
As of version 8.0.0, the installation instructions have changed. For most users, this means they will have to run a one-time-only extra command, make a change to their Composer configuration and/or adjust their build scripts.

Please read the changelog for version [8.0.0](https://github.com/wimg/PHPCompatibility/releases/tag/8.0.0) carefully before upgrading.


Installation in a Composer project (method 1)
-------------------------------------------

* Add the following lines to the `require-dev` section of your `composer.json` file.
    ```json
    "require-dev": {
        "squizlabs/php_codesniffer": "*@stable",
        "wimg/php-compatibility": "*@stable"
    }
    ```
* Next, PHP CodeSniffer has to be informed of the location of the standard.
    - If PHPCompatibility is the **_only_** external PHP CodeSniffer standard you use, you can add the following to your `composer.json` file to automatically run the necessary command:
        ```json
        "scripts": {
            "post-install-cmd": "\"vendor/bin/phpcs\" --config-set installed_paths vendor/wimg/php-compatibility",
            "post-update-cmd" : "\"vendor/bin/phpcs\" --config-set installed_paths vendor/wimg/php-compatibility"
        }
        ```
    - Alternatively - and **_strongly recommended_** if you use more than one external PHP CodeSniffer standard - you can use any of the following Composer plugins to handle this for you.

       Just add the Composer plugin you prefer to the `require-dev` section of your `composer.json` file.

       * [DealerDirect/phpcodesniffer-composer-installer](https://github.com/DealerDirect/phpcodesniffer-composer-installer):"^0.4.3"
       * [higidi/composer-phpcodesniffer-standards-plugin](https://github.com/higidi/composer-phpcodesniffer-standards-plugin)
       * [SimplyAdmire/ComposerPlugins](https://github.com/SimplyAdmire/ComposerPlugins). This plugin *might* still work, but appears to be abandoned.
    - As a last alternative in case you use a custom ruleset, _and only if you use PHP CodeSniffer version 2.6.0 or higher_, you can tell PHP CodeSniffer the path to the PHPCompatibility standard by adding the following snippet to your custom ruleset:
        ```xml
        <config name="installed_paths" value="vendor/wimg/php-compatibility" />
        ```
* Run `composer update squizlabs/php_codesniffer wimg/php-compatibility --lock` to install both PHP CodeSniffer, the PHPCompatibility coding standard and - optionally - the Composer plugin.
* Verify that the PHPCompatibility standard is registered correctly by running `./vendor/bin/phpcs -i` on the command line. PHPCompatibility should be listed as one of the available standards.
* Now you can use the following command to inspect your code:
    ```bash
    ./vendor/bin/phpcs -p . --standard=PHPCompatibility
    ```

Installation via a git check-out to an arbitrary directory (method 2)
-----------------------

* Install [PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) via [your preferred method](https://github.com/squizlabs/PHP_CodeSniffer#installation).

    PHP CodeSniffer offers a variety of installation methods to suit your work-flow: Composer, [PEAR](http://pear.php.net/PHP_CodeSniffer), a Phar file, zipped/tarred release archives or checking the repository out using Git.

    **Pro-tip:** Register the path to PHPCS in your system `$PATH` environment variable to make the `phpcs` command available from anywhere in your file system.
* Download the [latest PHPCompatibility release](https://github.com/wimg/PHPCompatibility/releases) and unzip/untar it into an arbitrary directory.

    You can also choose to clone the repository using git to easily update your install regularly.
* Add the path to the directory in which you placed your copy of the PHPCompatibility repo to the PHP CodeSniffer configuration using the below command from the command line:
   ```bash
   phpcs --config-set installed_paths /path/to/PHPCompatibility
   ```
   I.e. if you placed the `PHPCompatibility` repository in the `/my/custom/standards/PHPCompatibility` directory, you will need to add that directory to the PHP CodeSniffer [`installed_paths` configuration variable](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Configuration-Options#setting-the-installed-standard-paths).

   **Warning**: :warning: The `installed_paths` command overwrites any previously set `installed_paths`. If you have previously set `installed_paths` for other external standards, run `phpcs --config-show` first and then run the `installed_paths` command with all the paths you need separated by comma's, i.e.:
   ```bash
   phpcs --config-set installed_paths /path/1,/path/2,/path/3
   ```

   **Pro-tip:** Alternatively, in case you use a custom ruleset _and only if you use PHP CodeSniffer version 2.6.0 or higher_, you can tell PHP CodeSniffer the path to the PHPCompatibility standard(s) by adding the following snippet to your custom ruleset:
   ```xml
   <config name="installed_paths" value="/path/to/PHPCompatibility" />
   ```
* Verify that the PHPCompatibility standard is registered correctly by running `phpcs -i` on the command line. PHPCompatibility should be listed as one of the available standards.
* Now you can use the following command to inspect your code:
    ```bash
    phpcs -p . --standard=PHPCompatibility
    ```

Sniffing your code for compatibility with specific PHP version(s)
------------------------------
* Run the coding standard from the command-line with `phpcs -p . --standard=PHPCompatibility`.
* By default, you will only receive notifications about deprecated and/or removed PHP features.
* To get the most out of the PHPCompatibility standard, you should specify a `testVersion` to check against. That will enable the checks for both deprecated/removed PHP features as well as the detection of code using new PHP features.
    - You can run the checks for just one specific PHP version by adding `--runtime-set testVersion 5.5` to your command line command.
    - You can also specify a range of PHP versions that your code needs to support. In this situation, compatibility issues that affect any of the PHP versions in that range will be reported: `--runtime-set testVersion 5.3-5.5`.
    - As of PHPCompatibility 7.1.3, you can omit one part of the range if you want to support everything above or below a particular version, i.e. use `--runtime-set testVersion 7.0-` to run all the checks for PHP 7.0 and above.
* By default the report will be sent to the console, if you want to save the report to a file, add the following to the command line command: `--report-full=path/to/report-file`.
    For more information and other reporting options, check the [PHP CodeSniffer wiki](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Reporting).

More information can be found on Wim Godden's [blog](http://techblog.wimgodden.be/tag/codesniffer).


### Using a framework/CMS specific ruleset

As of PHPCompatibility 8.2.0, this library ships with a [limited set of framework/CMS specific ruleset(s)](https://github.com/wimg/PHPCompatibility/tree/master/framework-rulesets).

Framework/CMS specific ruleset do not set the minimum PHP version for your project, so you will still need to pass a `testVersion` to get the most accurate results.

* To use a framework/CMS specific ruleset from the command-line:
    ```bash
    phpcs -p . --standard=path/to/PHPCompatibility/framework-rulesets/framework-name.xml --runtime-set testVersion 5.5-
    ```

* To use a framework/CMS specific ruleset from within a custom ruleset - more about those below -, it is **strongly** recommended to use a Composer-based install so the path to PHPCompatibility will be predictable and the same for all users of the custom ruleset.
    ```xml
    <config name="testVersion" value="5.5-"/>
    <rule ref="./vendor/wimg/php-compatibility/framework-rulesets/framework-name.xml"/>
    ```
    The path should be an absolute path or the path relative to the final ruleset in the root of a project.


Using a custom ruleset
------------------------------
Like with any PHP CodeSniffer standard, you can add PHPCompatibility to a custom PHP CodeSniffer ruleset.

```xml
<?xml version="1.0"?>
<ruleset name="Custom ruleset">
    <description>My rules for PHP CodeSniffer</description>

    <!-- Run against the PHPCompatibility ruleset -->
    <rule ref="PHPCompatibility"/>

    <!-- Run against a second ruleset -->
    <rule ref="PSR2"/>

</ruleset>
```

You can also set the `testVersion` from within the ruleset:
```xml
    <!-- Check for cross-version support for PHP 5.6 and higher. -->
    <config name="testVersion" value="5.6-"/>
```

Other advanced options, such as changing the message type or severity of select sniffs, as described in the [PHPCS Annotated ruleset](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Annotated-ruleset.xml) wiki page are, of course, also supported.

#### `testVersion` in the ruleset versus command-line

In PHPCS 3.2.0 and lower, once you set the `testVersion` in the ruleset, you could not overrule it from the command-line anymore.
Starting with PHPCS 3.3.0, the `testVersion` set via the command-line will overrule the `testVersion` in the ruleset.

This allows for more flexibility when, for instance, your project needs to comply with PHP `5.5-`, but you have a bootstrap file which needs to be compatible with PHP `5.2-`.


#### PHPCompatibility specific options

At this moment, there is one sniff which has a property which can be set via the ruleset. More custom properties may become available in the future.

The `PHPCompatibility.PHP.RemovedExtensions` sniff checks for removed extensions based on the function prefix used for these extensions.
This might clash with userland functions using the same function prefix.

To whitelist userland functions, you can pass a comma-delimited list of function names to the sniff.
```xml
    <!-- Whitelist the mysql_to_rfc3339() and mysql_another_function() functions. -->
    <rule ref="PHPCompatibility.PHP.RemovedExtensions">
        <properties>
            <property name="functionWhitelist" type="array" value="mysql_to_rfc3339,mysql_another_function"/>
        </properties>
    </rule>
```

This property was added in PHPCompatibility version 7.0.1.
As of PHPCompatibility version 8.0.0, this custom property is only supported in combination with PHP CodeSniffer > 2.6.0 due to an upstream bug (which was fixed in PHPCS 2.6.0).


License
-------
This code is released under the GNU Lesser General Public License (LGPL). For more information, visit http://www.gnu.org/copyleft/lesser.html
