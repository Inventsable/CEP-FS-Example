<template>
  <div></div>
</template>

<script>

// CEP doesn't let us access "require()" as a global if in an iframe. But we can take care of both production and development like this:
const fs = /localhost/.test(document.location.href) ? cep_node.require('fs') : require('fs')

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
