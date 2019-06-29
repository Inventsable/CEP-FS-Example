# fstest

## How to use any `require` module within a CEP extension's iframe (will update templates soon):

### First, we need to change the CEP version to 8.0 in two places in manifest.xml:
- From 7.0 to 8.0 in [Line #2](https://github.com/Inventsable/CEP-FS-Example/blob/master/CSXS/manifest.xml#L2):
```xml
  <!-- Inside <ExtensionManifest> -->
  Version="8.0"
```

- From 7.0 to 8.0 in [Line #16](https://github.com/Inventsable/CEP-FS-Example/blob/master/CSXS/manifest.xml#L16):
```xml
  <!-- Inside <RequiredRuntime> -->
  Version="8.0"
```

### Place the additional parameter `enable-nodejs` [inside the iframe of ./public/index-dev.html at Line #10](https://github.com/Inventsable/CEP-FS-Example/blob/master/public/index-dev.html#L10)

```html
  <iframe
    enable-nodejs
    src="http://localhost:8080"
    style="border: 0; width: 100vw; height: 100vh;"
  ></iframe>
```

### Whenever `require()` is needed, we need to provide backdoors for both context:

```js
// Before using require in any file, we need to define it like so:
const require = require || cep_node.require;

// Now this works for either context
const fs = require('fs')
```

## Working examples for fs.stat() [found in test.vue component here](https://github.com/Inventsable/CEP-FS-Example/blob/master/src/components/test.vue)