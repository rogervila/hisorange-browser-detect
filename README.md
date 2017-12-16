## Browser Detection by _[hisorange](https://hisorange.me)_ ###

[![Latest Stable Version](https://poser.pugx.org/hisorange/browser-detect/v/stable)](https://packagist.org/packages/hisorange/browser-detect)
[![Build Status](https://travis-ci.org/hisorange/browser-detect.svg?branch=stable)](https://travis-ci.org/hisorange/browser-detect)
[![Coverage Status](https://coveralls.io/repos/github/hisorange/browser-detect/badge.svg)](https://coveralls.io/github/hisorange/browser-detect)
[![Total Downloads](https://poser.pugx.org/hisorange/browser-detect/downloads)](https://packagist.org/packages/hisorange/browser-detect)
[![Dependency Status](https://www.versioneye.com/user/projects/5a2485d90fb24f27ceaeb6d1/badge.svg?style=flat-square)](https://www.versioneye.com/user/projects/5a2485d90fb24f27ceaeb6d1)
[![License](https://poser.pugx.org/hisorange/browser-detect/license)](https://packagist.org/packages/hisorange/browser-detect)

Easy to use package to identify the user's browser details and device type. Magic is not involved the results are generated by multiple well tested and developed packages. Supporting every **laravel** version between **5.0 &raquo; 5.5**, also tested on every release **PHP** between **5.6 &raquo; 7.2**.

### How to install ###
***

```sh
composer require hisorange/browser-detect
```

Yep, that's it! At least for lavarel 5.5 and above, for 5.4 and below please read [the extended installation](#extended-installation).

### How to use ###
***

In your classes and controllers just call the **Browser** facade:

```php
// Determine the user's device type is simple as this:
Browser::isMobile();
Browser::isTablet();
Browser::isDesktop();

// Every wondered if it is a bot who loading your page?
if (Browser::isBot()) {
    echo 'No need to wonder anymore!';
}

// Check for vendors.
if (Browser::isFirefox() || Browser::isOpera()) {
    $output .= '<script src="firefox-fix.js"></script>';
}
```

Even in your blade templates:

```blade
{{-- Directives are built in laravel 5.5 and above! --}}
@mobile
    <p>This is the MOBILE template!</p>
    @include('your-mobile-template')
@endmobile

@tablet
    <p>This is the TABLET template!</p>
    <link rel="stylesheet" href="tablet.css" title="Reduce the page size, load what the user need">
@endtablet

@desktop
    <p>This is the DESKTOP template!</p>
@enddesktop

// Every key is supported.
@browser('isBot')
    <p>Bots are identified too :)</p>
@endbrowser
```

### Available API calls ###
***

Every call on the **Browser** facade is mirrored to the result object, so the following informations are available on your result too, where you can use the array syntax to access them.

| Call | Response | Internal Type |
| :--- | :--- | :---: |
| Browser::userAgent() | Current visitor's HTTP_USER_AGENT string. | _(string)_ |
| Browser::isMobile() | Is this a mobile device. | _(boolean)_ |
| Browser::isTablet() | Is this a tablet device. | _(boolean)_ |
| Browser::isDesktop() | Is this a desktop computer. | _(boolean)_ |
| Browser::isBot() | Is this a crawler / bot. | _(boolean)_ |
| **Browser related functions**  |||
| Browser::browserName() | Browser's human friendly name like Firefox 3.6, Chrome 42. | _(string)_ |
| Browser::browserFamily() | Browser's vendor like Chrome, Firefox, Opera. | _(string)_ |
| Browser::browserVersion() | Browser's human friendly version string. | _(string)_ |
| Browser::browserVersionMajor() | Browser's [semantic](https://semver.org/) major version. | _(integer)_ |
| Browser::browserVersionMinor() | Browser's [semantic](https://semver.org/) minor version. | _(integer)_ |
| Browser::browserVersionPatch() | Browser's [semantic](https://semver.org/) patch version. | _(integer)_ |
| **Operating system related functions**  |||
| Browser::platformName() | Operating system's human friendly name like Windows XP, MacOS 10. | _(string)_ |
| Browser::platformFamily() | Operating system's vendor like Linux, Windows, MacOS. | _(string)_ |
| Browser::platformVersion() | Operating system's human friendly version like XP, Vista, 10. | _(integer)_ |
| Browser::platformVersionMajor() | Operating system's [semantic](https://semver.org/) major version. | _(integer)_ |
| Browser::platformVersionMinor() | Operating system's [semantic](https://semver.org/) minor version. | _(integer)_ |
| Browser::platformVersionPatch() | Operating system's [semantic](https://semver.org/) patch version. | _(integer)_ |
| **Device related functions**  |||
| Browser::deviceFamily() | Device's vendor like Samsung, Apple, Huawei. | _(string)_ |
| Browser::deviceModel() | Device's brand name like iPad, iPhone, Nexus. | _(string)_ |
| Browser::mobileGrade() | Device's mobile grade in scale of A,B,C for performance. | _(string)_ |
| **Browser vendor related functions**  |||
| Browser::isChrome() | Is this a chrome browser. | _(boolean)_ |
| Browser::isFirefox() | Is this a firefox browser. | _(boolean)_ |
| Browser::isOpera() | Is this an opera browser. | _(boolean)_ |
| Browser::isSafari() | Is this a safari browser. | _(boolean)_ |
| Browser::isIE() | Checks if the browser is an some kind of Internet Explorer (or Trident) | _(boolean)_ |
| Browser::isIEVersion() | Compares to a given IE version | _(boolean)_ |


### Version support ###
***

The following matrix is being continuously tested by the great and awesome [Travis CI](https://travis-ci.org/hisorange)!

| ----- | PHP 5.6 | PHP 7.0 | PHP 7.1 | PHP 7.2 |
| :---: | :-----: | :-----: | :-----: | :-----: |
| Laravel 5.0 | &#10003; | - | - | - |
| Laravel 5.1 | &#10003; | - | - | - |
| Laravel 5.2 | &#10003; | - | - | - |
| Laravel 5.3 | &#10003; | - | - | - |
| Laravel 5.4 | &#10003; | &#10003; | &#10003; | &#10003; |
| Laravel 5.5 | - | &#10003; | &#10003; | &#10003; |

\* _Cannot auto test the laravel 5.4 on PHP 7.1 because of version incompatibility between the PHPUnit, Laravel and the package testing library, but the versions are tested manually._

##### Laravel 4.x support

Laravel 4.x releases are not actively developed but you can still use the browser detect 1.x for it; You can find those releases under the [versions](https://github.com/hisorange/browser-detect/releases) tab. Please read the readme from the release use choose, after version 2.x the package was redesigned from the sketch so nor the installation nor the usage is the same.

### Extended Installation ###
***

If you are using laravel 5.4 and below you have to add the service provider in your **config/app.php** like this:

```php
	'providers' => [
    	// Package Service Providers...
    	\hisorange\BrowserDetect\ServiceProvider::class,
    ]
```

and don't forget to add the **facade** in the same file like this:

```php
	'aliases' => [
    	'Browser' => \hisorange\BrowserDetect\Facade::class,
    ]
```

### Extended Usage Information ###
***

The code is designed to be an easy to use style, so every call you make on the **Browser** facade will access the result object and get the data for you, but you can parse agents other then the current user's.

```php
// When you call the detect function you will get a result object, from the current user's agent.
$result = Browser::detect();

// If you wana get browser details from a user agent other then the current user call the parse function.
$result = Browser::parse('Opera/9.80 (Windows NT 6.0) Presto/2.12.388 Version/12.14');
```

### Changlog
***

See the detailed changes in the [CHANGELOG](CHANGELOG.md) file.

