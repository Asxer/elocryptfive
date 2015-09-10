# elocryptfive

Automatically encrypt and decrypt Laravel 5 Eloquent values

This is inspired by Dtisgodsson's Laravel 4 "elocrypt" package, ported to Laravel 5.

# Installation

This package can be installed via Composer by adding the following to your composer.json file:

    "require": {
        "delatbabel/elocryptfive": "dev-master"
    }

You must then run the following command:

    composer update

# Usage

Simply reference the Elocrypt trait in any Eloquent Model you wish to apply encryption to and 
then define an "encryptable" array on that model containing a list of the attributes you wish
to Encrypt.

For example:

    class User extends Eloquent {

        use Elocrypt;

        public $encryptable = ['first_name', 'last_name', 'address_line_1', 'postcode'];
    }

# How it Works?

By including the Elocrypt trait, the setAttribute() and getAttributeFromArray() methods provided
by Eloquent are overridden to include an additional step. This additional step simply checks
whether the attribute being set or get is included in the "encryptable" array on the model,
and either encrypts/decrypts it accordingly.

# Keys and IVs

The key and encryption algorithm used are as per the Laravel Encrypter service, and defined in config/app.php
as follows:

    'key' => env('APP_KEY', 'SomeRandomString'),

    'cipher' => 'AES-256-CBC',

I recommend generating a random 32 character string for the encryption key, and using AES-256-CBC as the cipher
for encrypting data.  If you are encrypting long data strings then AES-256-CBC-HMAC-SHA1 will be better.

The IV for encryption is randomly generated.
