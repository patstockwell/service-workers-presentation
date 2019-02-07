title: Service workers
author:
  name: Patrick Stockwell
  url: http://deciphr.net
output: build/service-workers.html
controls: false

--

# Service workers
## A first look

--

#### Imagine...

Wouldn't it be cool if, as developers, we could instruct browsers to save a copy
of our website?

--

#### Websites behaving like apps

It would work in slow-network and offline environments 🔌

Serving the site from the user's device would mean near-instant load times ⚡️

--

#### What might that look like?

- Website code (`.html`, `.css`, `.js`)
- Caching/serving instructions (`.js`)

--

#### An example request for your site

- Ask the browser for `www.yoursite.com`
- Browser checks to see if any 'caching instructions' exist for this site
- Uses the cache/network to serve assets based on those instructions

--

#### Hello, Service workers!

Service workers allow us to define 'caching instructions' for the browser.

--

#### Hello, Service workers!

Service workers are a recent addition to the web specification.
They're a tool that the browser provides via an API, just like `console.log`,
`window`, or `localStorage`.

--

#### What do others say?

> _A service worker is a script that your browser runs in the background,
separate from a web page, opening the door to features that don't need a web
page or user interaction._

###### https://developers.google.com/web/fundamentals/primers/service-workers/

--

#### What do others say?

> _Service workers essentially act as proxy servers that sit between web
applications and the network._

###### https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API

--

#### They cache stuff!
Service workers `===` super fast user experience

--

### My reaction

![](https://media.giphy.com/media/iAYupOdWXQy5a4nVGk/giphy.gif)

--

### Let's build a mental model

_'Normal Javascript'_

vs

_A service worker_

--

#### Normal JavaScript

Is requested via a `<script>` tag
```html
<script src="./app.js"></script>
```

--

#### A service worker

Is requested programmatically
```js
navigator.serviceWorker.register('./service-worker.js')
```

--

#### Normal JavaScript

Has global objects `window` and `document`

--

#### A service worker

Has an entirely different runtime environment.

- The global object is _ServiceWorkerGlobalScope_ (referenced with `self`)
- Has no access to the DOM

--

#### Normal JavaScript

Stored in main memory (volatile)

--

#### A service worker

Stored on the hard disk (non-volatile)

--

#### Normal JavaScript

You can have many `.js` files per page

--

#### A service worker

You can only have one `.js` service worker per _scope_

--

#### Normal JavaScript

The primary purpose is to manipulate the document

--

#### A service worker

The primary purpose is to manipulate network requests

--

#### A registration example

This runs in our normal runtime environment

```js
// app.js

if ('serviceWorker' in navigator) {
  window.addEventListener('load', function() {
    console.log('attempting to install service worker');
    navigator.serviceWorker.register('./service-worker.js')
      .then(function(registration) {
        console.log('ServiceWorker registered: ', registration.scope);
      })
      .catch(function(error) {
        console.log('ServiceWorker registration failed: ', error);
      });
  });
}
```

--

#### A list of things

* Item 1
* Item B
* Item gamma

No need for multiple templates!
