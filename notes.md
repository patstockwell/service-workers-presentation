title: Service workers
author:
  name: Patrick Stockwell
  url: mail@deciphr.net
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

#### Hullo, Service workers!

Service workers allow us to define 'caching instructions' for the browser.

--

#### Hullo, Service workers!

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

### My reaction

![](https://media.giphy.com/media/iAYupOdWXQy5a4nVGk/giphy.gif)

--

#### They cache stuff!
Service workers `===` super fast user experience

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

#### Service Worker Lifecycle Events
_Assuming this is the first visit_

- 🚗 `registration` - Request the SW file.
- 🚙 `install` - Parsing the SW and caching files begins
- 🚛 `activate` - Ready to control the in-scope pages
- ✈️ `fetch` - A Request has been made and passed through the SW

--

#### Service Worker Lifecycle Events
_Assuming you have updated your SW_

- 🚗 `registration` - Request the SW file. (Could be the same name as the old one)
- 🚙 `install` - Parsing the SW and caching files begins
- 🚜 `waiting` - Installed successfully but the old SW is still in control
- 🚛 `activate` - The old SW is no longer controlling any pages and the new one is
now active.
- ✈️ `fetch` - A Request has been made and passed through the SW

--

#### Demo

Let's check out some SW code and see it in action 🥊

http://deciphr.net
