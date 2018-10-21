---
layout: post
title: Drupal on Symphony2
---

Notes from DrupalCon 2012 from a session I attended about Symfony2

<!--more-->

Some symphony components will come preinstalled in Drupal 8.

### ClassLoader

Component that loads files where classes are defined only when needed.

http://symfony.com/PSR0

### HttpFoundation


HTTP/1.1 (RFC 2616)  PLEASE READ THIS.

http://www.ietf.org/rfc/rfc2616.txt
http://tools.ietf.org/wg/httpbis

REQUESTS:

Normally, in php to get HTTP info, you need to use the `$_GET` and `$_SESSION`
and `$_SERVER` super globals.

This goes wrong, if there are reverse proxies and other things (e.g. for
HTTP_CLIENT_IP doesn't work behind a proxy.  The FORWARDED_FOR variable is not
always trustworthy. A lot of work just to get a reasonable client IP address.

Not object-oriented, singleton like, lot of low level work to do.

```php
$request = Request::createFromGlobals();
$request = Request::create('/hello.html', 'GET');
```

RESPONSE:

Plain php:


```php
header()
setcookies()
$_SESSION()
echo '…';
```

Doesn't play well with CLI.
Singleton like
Low-level abstraction only.
Not Object-Oriented.

### Symfony:

```php
$resonse = new REspponse('Not Found', 404).
new StreamedResponse()

$response->prepare($request);
```

Session Management
flash messages.


### Routing

Matching incoming requests, to know which code (controller) should handle the request.

```php
$route = new Route('node/{id}', array('_controller' => 'SomeClass:someMethod'));
$routes = new RouteCollection();
$routes->add(…
```

Symfony can also *generate* the urls.


```php
$generator = new UrlGeneratior($routes, $context);
echo $generator->generate('node', array('id' => 12));
```

### EventDispatcher

Implements a lightweight of the observer design pattern.

Like hook system.

```php
$dispatcher  = new EventDispatcher()

callable = function (Event $event) {
     // do somethingin
};

$dispather->addListener('event_name', $callable);
```

### HttpKernel

standard way to handle requests and ensure request gets sent back to browser.

```php
interface HttpKernelInterface {
     function handle(Request $request, $type = self::MASTER_REquest, $catch) {}
}

interface ControllerResolverInterface {
     function getController(Request $r)
     function getArguments(Request $r, $controller)
}
```

### HTTP Ccaching.

Symfony relies on http caching headers.

Experiation (Cache-Control, Expires header)

Validation:  Last-Modified, If-Modified-Since, ETag.

```php
$response->setTtl(10);
$response->setClientTtl(10);
```

