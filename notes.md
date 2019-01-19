title: Service workers
author:
  name: Patrick Stockwell
  url: http://deciphr.net
output: service-workers.html
controls: false

--

# Service workers
## A first look

--

### A textual example

Content can be written in **Markdown!** New lines no longer need two angle brackets.

This will be in a separate paragraph
```js
if ('serviceWorker' in navigator) {
  window.addEventListener('load', function() {
    console.log('attempting to install service worker');
    navigator.serviceWorker.register('./service-worker.js')
      .then(function(registration) {
        console.log('ServiceWorker registration successful with scope: ', registration.scope);
      })
      .catch(function(error) {
        console.log('ServiceWorker registration failed: ', error);
      });
  });
}
```

--

### A list of things

* Item 1
* Item B
* Item gamma

No need for multiple templates!
