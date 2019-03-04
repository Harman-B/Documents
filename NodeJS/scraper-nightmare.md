# Scraper using NightmareJS Getting Started

## Basic Setup

### Dev environment
- node
- npm

### Hello World
    const Nightmare = require('nightmare');
    nightmare = Nightmare({show: true, waitTimeout: 500000, openDevTools: true});
    nightmare
        .goto('https://duckduckgo.com')
        .type('#search_form_input_homepage', 'github nightmare')
        .click('#search_button_homepage')
        .wait('#r1-0 a.result__a')
        .evaluate(() => document.querySelector('#r1-0 a.result__a').href)
        .end()
        .then(console.log)
        .catch(error => {
            console.error('Search failed:', error)
        })

### Checks to make a good scraper
- check the robot.txt in the root directory of the site.
- It is good to setup user-agent using.
    `.useragent('your user agent here')`
    (more about [user-agents]())
- Robots may get detected based on their behaviour. One of those behaviours is waiting time. So I use random wait times.

### Loops in nightmare
Nightmare is designed to have a single queue running against a single Electron instance. Actions are chained off of a Nightmare instance, and then executed with `.then()`. Executing the operations in series requires arranging them to execute in sequential order.

We can use the following:
- `array.reduce`
- Using `vo`

For more detailed explaination. [link](https://github.com/rosshinkley/nightmare-examples/blob/master/docs/common-pitfalls/async-operations-loops.md)

### Pass variable from node runtime to evaluate()

`const selector = 'h1'
nightmare
  .evaluate(selector => {
    // now we're executing inside the browser scope.
    return document.querySelector(selector).innerText
  }, selector) // <-- that's how you pass parameters from Node scope to browser scope
  .then(text => {
    // ...
  })`

[link](https://github.com/segmentio/nightmare#evaluatefn-arg1-arg2)

### Other links
- how to detect bots [link](https://ppcprotect.com/how-to-detect-bot-traffic/)
- linkedin scraper by [FutoRicky](https://github.com/FutoRicky/linkedin-email-extractor/blob/master/index.js)