<template>
  <div></div>
</template>

<script>

// Since CEP doesn't allow require within an iframe, we need to include both entrypoints.

// Before using require in any file, we need to define it like so:
const require = require || cep_node.require;

// Now this works for either context
const fs = require('fs')

// If we need to know whether Developer or Production context specifically, we can do this:
// const fs = /localhost/.test(document.location.href) ? cep_node.require('fs') : require('fs')

export default {
  name: 'test',
  mounted() {

    let root = decodeURI(window.__adobe_cep__.getSystemPath("extension")).replace(
      /file\:\/{1,}/, ""
    )

    // Makes this available in either dev or production
    console.log(fs)
    console.log(fs.stat)
    
    // Example readFile()
    fs.readFile(`${root}/.debug`, { encoding: 'utf-8' }, (err, data) => {
      if (err) throw err;
      console.log(data);
    });

    // Example stat()
    fs.stat(`${root}/.debug`, (err, stats) => {
      // See the data
      console.log(stats)
      if (stats.isFile())
        console.log('This is a file');
      else if (stats.isDirectory()) 
          console.log('This is a directory');

    })
  }
  
}
</script>
