# fstest

## How to use any `require` module within a CEP extension's iframe (will update templates soon):

### First, we need to change the CEP version to 8.0 in two places in manifest.xml:
- From 7.0 to 8.0 in Line #2:
```xml
  <!-- Inside <ExtensionManifest> -->
  Version="8.0"
```

- From 7.0 to 8.0 in Line #16:
```xml
  <!-- Inside <RequiredRuntime> -->
  Version="8.0"
```

### Place the additional parameter `enable-nodejs` inside the iframe of `./public/index-dev.html`

```html
  <iframe
    enable-nodejs
    src="http://localhost:8080"
    style="border: 0; width: 100vw; height: 100vh;"
  ></iframe>
```

### Whenever `require()` is needed for both Production and Developer, we need to require it like so:

```js
// If DEVELOPER, use cep_node.require(), else use require()
const fs = /localhost/.test(document.location.href) ? cep_node.require('fs') : require('fs')
```

## Working examples for fs.stat() found in test component here