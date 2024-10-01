# Omnipay: NetCash

**NetCash driver for the Omnipay Laravel payment processing library**

[![Latest Stable Version](https://poser.pugx.org/armyan/omnipay-netcash/v/stable)](https://packagist.org/packages/armyan/omnipay-netcash)
[![Total Downloads](https://poser.pugx.org/armyan/omnipay-netcash/d/total.png)](https://packagist.org/packages/armyan/omnipay-netcash)

[Omnipay](https://github.com/thephpleague/omnipay) is a framework agnostic, multi-gateway payment
processing library for PHP 5.5+. This package implements NetCash support for Omnipay.

## Installation

Omnipay is installed via [Composer](http://getcomposer.org/). To install, simply add it
to your `composer.json` file:

```json
{
    "require": {
        "roland198412/omnipay-netcash": "^1.0.0"
    }
}
```

And run composer to update your dependencies:

    composer update

Or you can simply run

    composer require roland198412/omnipay-netcash

## Basic Usage

1. Use Omnipay gateway class:

```php
    use Omnipay\Omnipay;
```

2. Initialize NetCash gateway:

```php

    $gateway = Omnipay::create('NetCash');
    $gateway->setVendorKey(env('VENDOR_KEY'));
    $gateway->setAccountId(env('ACCOUNT_ID'));
    $gateway->setServiceKey(env('SERVICE_KEY'));
```

3. Call purchase, it will automatically redirect to NetCash's hosted page

```php

    $purchase = $gateway->purchase(
            [
                'amount' => 100, // Amount to charge
                'transactionId' => "unique reference ", // Transaction ID from your system
                'description' => 'description of goods - p3'  //'description of goods - p3',
                'email' => 'your@email.com', // Email address
                'phone' => '000000000' // Phone number
            ]
        )->send();
    $purchase->redirect();

```

4. Create a webhook controller to handle the callback request at your `RESULT_URL` and catch the webhook as follows

```php

    $gateway = Omnipay::create('NetCash');
    $gateway->setAccountId(env('ACCOUNT_ID'));
    $gateway->setServiceKey(env('SERVICE_KEY'));
    
    $purchase = $gateway->completePurchase()->send();
    
    // Do the rest with $purchase and response with 'OK'
    if ($purchase->isSuccessful()) {
        
        // Your logic
        
    }
    
    return new Response('OK');

```

For general usage instructions, please see the main [Omnipay](https://github.com/thephpleague/omnipay)
repository.

## Support

If you are having general issues with Omnipay, we suggest posting on
[Stack Overflow](http://stackoverflow.com/). Be sure to add the
[omnipay tag](http://stackoverflow.com/questions/tagged/omnipay) so it can be easily found.

If you want to keep up to date with release anouncements, discuss ideas for the project,
or ask more detailed questions, there is also a [mailing list](https://groups.google.com/forum/#!forum/omnipay) which
you can subscribe to.

If you believe you have found a bug, please report it using the [GitHub issue tracker](https://github.com/arm-yan/omnipay-netcash/issues),
or better yet, fork the library and submit a pull request.
