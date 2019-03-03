## View installed packages
- `npm ls --depth=0`
- or make a file test.js with the following code
    function npmls(cb) {
    require('child_process').exec('npm ls --json', function(err, stdout, stderr) {
        if (err) return cb(err)
        cb(null, JSON.parse(stdout));
    });
    }
    npmls(console.log);