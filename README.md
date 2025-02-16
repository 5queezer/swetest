# Swetest

[![Build Status](https://travis-ci.org/DestinyLab/swetest.svg?branch=master)](https://travis-ci.org/DestinyLab/swetest)

Swetest is the simple wrapper of swisseph library's swetest.

## Requirement

 - PHP >=5.4

## Installing via Composer

The recommended way to install Swetest is through Composer.

```bash
# Install Composer
curl -sS https://getcomposer.org/installer | php
```

Next, Run the Composer require command from the Terminal:

    composer require hardevine/swetest


## Usage

```php
<?php

require_once 'vendor/autoload.php';

use DestinyLab\Swetest;
$swetest = new Swetest();

// ephemeris of Mercury (-p2) starting on 1 Dec 1900,
// 15 positions (-n15) in two-day steps (-s2)
$swetest->query('-b5.1.2002 -p -house12.05,49.50,k -ut12:30')->execute();

// another query way
$arr = [
    'b' => '5.1.2002',
    'p' => null,
    'house' => '12.05,49.50,k',
    'ut' => '12:30',
];
$swetest->query($arr)->execute();

// angular distance of moon (-p1) from sun (-d0) for 10
// consecutive days (-n10).
$swetest->query('-p1 -d0 -b1.12.1900 -n10 -fPTl -head')->execute();

// another query way
$arr = [
    'p' => 1,
    'd' => 0,
    'b' => '1.12.1900',
    'n' => 10,
    'f' => 'PTL',
    'head',
];
$swetest->query($arr)->execute();

// Midpoints between Saturn (-p6) and Chiron (-DD) for 100
// consecutive steps (-n100) with 5-day steps (-s5) with
// longitude in degree-sign format (-f..Z) rounded to minutes (-roundmin)
$swetest->query('-p6 -DD -b1.12.1900 -n100 -s5 -fPTZ -head -roundmin')->execute();

// another query way
$arr = [
    'p' => 6,
    'D' => 'D',
    'b' => '1.12.1900',
    'n' => 100,
    's' => 5,
    'f' => 'PTZ',
    'roundmin',
];
$swetest->query($arr)->execute();

// get response (status + output)
print_r($swetest->response());

// or just get status
print_r($swetest->getStatus());

// or just get output
print_r($swetest->getOutput());

// get last query
print_r($swetest->getLastQuery());
```

## Configuration

Mask swetest executable path (default to `true`):

```php
<?php

$swetest->setMaskPath(true);
```

Changing the swetest file's path:

```php
<?php

require_once 'vendor/autoload.php';

use DestinyLab\Swetest;

// method 1
$swetest = new Swetest('/path/to/swetest');

// method 2
$swetest = new Swetest();
$swetest->setPath('/path/to/swetest');
```

The resource by default includes following files:
 - seas_18.se1
 - semo_18.se1
 - sepl_18.se1

If you need more file, just download from <http://www.astro.com/ftp/swisseph/ephe/>.

## More Infomation

 - [swetest help](http://www.astro.com/cgi/swetest.cgi?arg=-h&p=0)

## License

MIT
