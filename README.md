Zxcvbn-PHP is a password strength estimator using pattern matching and minimum entropy calculation. Zxcvbn-PHP is based on the [the Javascript zxcvbn project](https://github.com/dropbox/zxcvbn) from [Dropbox and @lowe](https://blogs.dropbox.com/tech/2012/04/zxcvbn-realistic-password-strength-estimation/). "zxcvbn" is bad password, just like "qwerty" and "123456".

>zxcvbn attempts to give sound password advice through pattern matching and conservative entropy calculations. It finds 10k common passwords, common American names and surnames, common English words, and common patterns like dates, repeats (aaa), sequences (abcd), and QWERTY patterns.

[![Build Status](https://travis-ci.org/nostromo/zxcvbn-php-german.png?branch=master)](https://travis-ci.org/nostromo/zxcvbn-php-german)
[![Coverage Status](https://coveralls.io/repos/github/nostromo/zxcvbn-php-german/badge.svg?branch=master)](https://coveralls.io/github/nostromo/zxcvbn-php-german?branch=master)
[![Latest Stable Version](https://poser.pugx.org/nostromo/zxcvbn-php-german/v/stable)](https://packagist.org/packages/nostromo/zxcvbn-php-german)
[![License](https://poser.pugx.org/nostromo/zxcvbn-php-german/license)](https://packagist.org/packages/nostromo/zxcvbn-php-german)

## Installation

The library can be installed with [Composer](http://getcomposer.org) by adding it as a dependency to your composer.json file.

Via the command line run:
`composer require nostromo/zxcvbn-php-german`

Or in your composer.json add
```json
{
    "require": {
        "nostromo/zxcvbn-php-german": "^1.0"
    }
}
```

Then run `composer update` on the command line and include the
autoloader in your PHP scripts so that the ZxcvbnPhp class is available.

```php
require_once 'vendor/autoload.php';
```

## Usage

```php
use ZxcvbnPhp\Zxcvbn;

$userData = [
  'Marco',
  'marco@example.com'
];

$zxcvbn = new Zxcvbn();
$weak = $zxcvbn->passwordStrength('password', $userData);
echo $weak['score']; // will print 0

$strong = $zxcvbn->passwordStrength('correct horse battery staple');
echo $strong['score']; // will print 4

echo $weak['feedback']['warning']; // will print user-facing feedback on the password, set only when score <= 2
// $weak['feedback']['suggestions'] may contain user-facing suggestions to improve the score
```

Scores are integers from 0 to 4:
* 0 means the password is extremely guessable (within 10^3 guesses), dictionary words like 'password' or 'mother' score a 0
* 1 is still very guessable (guesses < 10^6), an extra character on a dictionary word can score a 1
* 2 is somewhat guessable (guesses < 10^8), provides some protection from unthrottled online attacks
* 3 is safely unguessable (guesses < 10^10), offers moderate protection from offline slow-hash scenario
* 4 is very unguessable (guesses >= 10^10) and provides strong protection from offline slow-hash scenario

### Acknowledgements
Thanks to:
* @lowe for the original [Javascript Zxcvbn](https://github.com/lowe/zxcvbn)
* [@Dreyer's port](https://github.com/Dreyer/php-zxcvbn) for reference for initial implementation
* [@mkopinsky](https://github.com/mkopinsky) for major updates to keep in sync with upstream scoring


