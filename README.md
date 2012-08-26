Gitane
======

Easy Node.JS Git wrapper with support for SSH keys. By default, the Git CLI
tool will only use the SSH key of the current user (e.g. `$HOME/.ssh/id_dsa`).

In order to be able to use Git with an arbitrary SSH key, a wrapper shell script to invoke `ssh -i <key>` must be written and the GIT_SSH environment
variable must point to that script.

Gitane wraps all this plumbing for you. Simply pass the SSH private key you wish to run Git with as a string argument and let Gitane do the rest. Gitane will clean up the temporary wrapper script after it is done.


Installation
============

Gitane is available in NPM. `npm install gitane`


Example
=======
```
  var fs = require('fs')
  var gitane = require('gitane')
  var path = require('path')

  // Use current working dir
  var baseDir = process.cwd()
  // Read private key from ~/.ssh/id_dsa
  var privKey = fs.readFileSync(path.join(process.env.HOME, '.ssh/id_dsa'), 'utf8')

  gitane.run(baseDir, privKey, "git clone git@github.com:niallo/Gitane.git",
    function(err, stdout, stderr) {
    if (err) {
      console.log("An error occurred: " + stderr)
      process.exit(1)
    }

    console.log("Git clone complete!")
  })
```

Tests
=====

Gitane comes with tests. To run, simply execute `npm test`.

License
=======

Gitane is released under a BSD license.
