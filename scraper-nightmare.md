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
- It is good to setup user-agent using (more about [user-agents]())
    `.useragent('your user agent here')`
- Robots may get detected based on their behaviour. One of those behaviours is waiting time. So I use random wait timees.
- 

