# {{.Pkg.Git.Name}}-php

{{if .Pkg.Official}}Official {{end}}{{.Pkg.Name}} API library client for PHP

__This library is generated by [alpaca](https://github.com/pksunkara/alpaca)__

## Installation

Make sure you have [composer](https://getcomposer.org) installed.

Add the following to your composer.json

```js
{
    "require": {
        "{{.Pkg.Php.Vendor}}/{{.Pkg.Package}}": "*"
    }
}
```

Update your dependencies

```bash
$ php composer.phar update
```

> This package follows the `PSR-0` convention names for its classes, which means you can easily integrate these classes loading in your own autoloader.

#### Versions

Works with [ 5.4 / 5.5 ]

## Usage

```php
<?php

// This file is generated by Composer
require_once 'vendor/autoload.php';

// Then we instantiate a client (as shown below)
```

### Build a client
{{if .Api.authorization.need_auth}}
__Using this api without authentication gives an error__
{{else}}
##### Without any authentication

```php
$client = new {{call .Fnc.camelize .Pkg.Name}}\Client({{if .Api.base_as_arg}}'{{.Api.base}}'{{end}});

// If you need to send options
$client = new {{call .Fnc.camelize .Pkg.Name}}\Client({{if .Api.base_as_arg}}'{{.Api.base}}', {{end}}array(), $clientOptions);
```
{{end}}{{if .Api.authorization.basic}}
##### Basic authentication

```php
$auth = array('username' => 'pksunkara', 'password' => 'password');

$client = new {{call .Fnc.camelize .Pkg.Name}}\Client({{if .Api.base_as_arg}}'{{.Api.base}}', {{end}}$auth, $clientOptions);
```
{{end}}{{if .Api.authorization.header}}
##### Authorization header token

```php
$client = new {{call .Fnc.camelize .Pkg.Name}}\Client({{if .Api.base_as_arg}}'{{.Api.base}}', {{end}}{{if .Api.authorization.oauth}}array('http_header' => '1a2b3'){{else}}'1a2b3'{{end}}, $clientOptions);
```
{{end}}{{if .Api.authorization.oauth}}
##### Oauth acess token

```php
$client = new {{call .Fnc.camelize .Pkg.Name}}\Client({{if .Api.base_as_arg}}'{{.Api.base}}', {{end}}'1a2b3', $clientOptions);
```

##### Oauth client secret

```php
$auth = array('client_id' => '09a8b7', 'client_secret' => '1a2b3');

$client = new {{call .Fnc.camelize .Pkg.Name}}\Client({{if .Api.base_as_arg}}'{{.Api.base}}', {{end}}$auth, $clientOptions);
```
{{end}}
### Client Options

The following options are available while instantiating a client:

 * __base__: Base url for the api
 * __api_version__: Default version of the api (to be used in url)
 * __user_agent__: Default user-agent for all requests
 * __headers__: Default headers for all requests
 * __request_type__: Default format of the request body{{if .Api.response.suffix}}
 * __response_type__: Default format of the response (to be used in url suffix){{end}}

### Response information

__All the callbacks provided to an api call will recieve the response as shown below__

```php
$response = $client->klass('args')->method('args', $methodOptions);

$response->code;
// >>> 200

$response->headers;
// >>> array('x-server' => 'apache')
```
{{if .Api.response.formats.html}}
##### HTML/TEXT response

When the response sent by server is either __html__ or __text__, it is not changed in any way

```php
$response->body;
// >>> 'The username is pksunkara!'
```
{{end}}{{if .Api.response.formats.json}}
##### JSON response

When the response sent by server is __json__, it is decoded into an array

```php
$response->body;
// >>> array('user' => 'pksunkara')
```
{{end}}
### Method Options

The following options are available while calling a method of an api:

 * __api_version__: Version of the api (to be used in url)
 * __headers__: Headers for the request
 * __query__: Query parameters for the url
 * __body__: Body of the request
 * __request_type__: Format of the request body{{if .Api.response.suffix}}
 * __response_type__: Format of the response (to be used in url suffix){{end}}

### Request body information

Set __request_type__ in options to modify the body accordingly

##### RAW request

When the value is set to __raw__, don't modify the body at all.

```php
$body = 'username=pksunkara';
// >>> 'username=pksunkara'
```
{{if .Api.request.formats.form}}
##### FORM request

When the value is set to __form__, urlencode the body.

```php
$body = array('user' => 'pksunkara');
// >>> 'user=pksunkara'
```
{{end}}{{if .Api.request.formats.json}}
##### JSON request

When the value is set to __json__, JSON encode the body.

```php
$body = array('user' => 'pksunkara');
// >>> '{"user": "pksunkara"}'
```
{{end}}{{with $data := .}}{{range .Api.classes}}
### {{index $data.Doc . "title"}} api

{{index $data.Doc . "desc"}}{{with (index $data.Api.class . "args")}}

The following arguments are required:
{{end}}{{with $class := .}}{{range (index $data.Api.class . "args")}}
 * __{{.}}__: {{index $data.Doc $class "args" . "desc"}}{{end}}

```php
${{call $data.Fnc.camelizeDownFirst .}} = $client->{{call $data.Fnc.camelizeDownFirst .}}({{call $data.Fnc.prnt.php (index $data.Doc . "args") ", " false}});
```
{{range (call $data.Fnc.methods (index $data.Api.class .))}}
##### {{index $data.Doc $class . "title"}} ({{call $data.Fnc.upper (or (index $data.Api.class $class . "method") "get")}} {{index $data.Api.class $class . "path"}})

{{index $data.Doc $class . "desc"}}{{with (index $data.Api.class $class . "params")}}

The following arguments are required:
{{end}}{{with $method := .}}{{range (index $data.Api.class $class . "params")}}{{if .required}}
 * __{{.name}}__: {{index $data.Doc $class $method "params" .name "desc"}}{{end}}{{end}}{{end}}

```php
$response = ${{call $data.Fnc.camelizeDownFirst $class}}->{{call $data.Fnc.camelizeDownFirst .}}({{call $data.Fnc.prnt.php (index $data.Doc $class . "params") ", " true}}$options);
```
{{end}}{{end}}{{end}}{{end}}
## Contributors
Here is a list of [Contributors](https://{{.Pkg.Git.Site}}/{{.Pkg.Git.User}}/{{.Pkg.Git.Name}}-php/contributors)

### TODO

## License
{{.Pkg.License}}

## Bug Reports
Report [here](https://{{.Pkg.Git.Site}}/{{.Pkg.Git.User}}/{{.Pkg.Git.Name}}-php/issues).

## Contact
{{.Pkg.Author.Name}} ({{.Pkg.Author.Email}})
