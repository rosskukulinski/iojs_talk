# iojs_talk
Talk on the emergence of IOJS and what it means to the NodeJS community


## Outline





## Dump Space

### Node Forward
Node Forward - http://nodeforward.org/   
Brain-child of @mikeal in an effort to improve node's ecosystem, Website went live on Oct 14    
"Node Forward is a broad community effort to improve Node, JavaScript, and their ecosystem through open collaboration"   

_Node Forward is you._

### IO.JS
https://github.com/iojs/io.js

IOJS is a fork of the joyent/node project.

The projects major reasons for splitting are:

1. Slow NodeJS release cycle
1. Lagging included V8 Releases (es6 support, perf, etc.)
1. Concerns about NodeJS Governence

The NodeJS team is focused on putting out 'enterprise ready' releases, but 
continually having a release that's 'about to ship in 2-weeks' for over a year
hurts credibility



#### Project Governence
https://github.com/iojs/io.js/blob/v1.x/GOVERNANCE.md

The io.js project is jointly governed by a Technical Committee (TC) which is responsible for high-level guidance of the project.

The TC has final authority over this project including:

Technical direction
Project governance and process (including this policy)
Contribution policy
GitHub repository hosting
Conduct guidelines
Maintaining the list of additional Collaborators

TC follows a Consensus Seeking decision making model. 

TC meets weekly on a Google Hangout 'On the Air' and are posted to YouTube afterwards

Why io.js? Because Joyent owns the Trademark 'NodeJS', and their legal team
needed to protect the trademark

Current TC:
* Isaac Z. Schlueter (@isaacs) <i@izs.me> (Technical Committee)
* Ben Noordhuis (@bnoordhuis) <info@bnoordhuis.nl> (Technical Committee)
* Bert Belder (@piscisaureus) <bertbelder@gmail.com> (Technical Committee)
* Fedor Indutny (@indutny) <fedor.indutny@gmail.com> (Technical Committee)
* Trevor Norris (@trevnorris) <trev.norris@gmail.com> (Technical Committee)
* Chris Dickinson (@chrisdickinson) <christopher.s.dickinson@gmail.com> (Technical Committee)
* Colin Ihrig (@cjihrig) <cjihrig@gmail.com> (Technical Committee)
* Mikeal Rogers (@mikeal) <mikeal.rogers@gmail.com>
* Rod Vagg (@rvagg) <rod@vagg.org>

### Roadmap
https://github.com/iojs/roadmap/issues/

Why? io.js aims to provide faster and predictable release cycles. It currently merges in the latest language, API and performance improvements to V8 while also updating libuv and other base libraries.

io.js has moved to Semver. The choice to release as 1.0.x was not to signify that io.js should be considered production-ready, but because it was a significant enough release from Node.js™ to warrant a major version increment.

There is an #io.js channel on Freenode IRC. We keep logs of the channel here.

https://nodebug.me/

So What's _in_ iojs?
* https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md
* https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#summary-of-changes-from-nodejs-v01035-to-iojs-v100 
* io.js@1.x V8 4.1+
* Just about everything that would have been Node 0.12
* es6 enabled by default (no --harmoney flag)

Big picture changes:
* V8 Upgrade from 3.14.5.9 (Node v0.10.35 ) to 3.26.33 (Node.js v0.11.14) to finally 3.31.74.1 (io.js v1.0.0) (Note: V8 4.1 is now shipping with iojs 1.03 - not a major change)
   * This brings along many fixes and performance improvements, as well as additional support for new ES6 language features
* npm: 1.4.28 to 2.1.18
* openssl: 1.0.1j to 1.0.1k
* Streams3, execSync child_process, cluster LB, crypto

All shipping features, the ones that V8 has considered stable, like generators, templates, new string methods and many others are turned on by default on io.js and do NOT require any kind of runtime flag.
Then there are staged features which are almost-completed features that haven't been completely tested or updated to the latest spec yet and therefore are not considered stable by the V8 team (e.g. there might be some edge cases left to discover). This is probably the equivalent of the state of generators on 3.26. These are the "use at your own risk" type of features that now require a runtime flag: --es_staging (or its synonym, --harmony).
Finally, all in progress features can be activated individually by their respective harmony flag (e.g. --harmony_arrow_functions), although this is highly discouraged unless for testing purposes.

https://kangax.github.io/compat-table/es6/

https://iojs.org/es6.html / Helpful comparison https://gist.github.com/cerebrl/8fe8ffe04bace984882e

* Block scoping
* let
* const
* function-in-blocks
* As of v8 3.31.74.1, block-scoped declarations are intentionally implemented with a non-compliant limitation to strict mode code. Developers should be aware that this will change as v8 continues towards ES6 specification compliance.
* Collections
* Map
* WeakMap
* Set
* WeakSet
* Generators
* Binary and Octal literals
* Promises
* New String methods
* Symbols
* Template strings

In Depth videon on what to expect with new version:
* Trevor Norris https://www.youtube.com/watch?v=HW89vNKCUMw&list=PLDVWhE1r7sji1NpNKmjfJiJgvr1UAVNyY&index=7

Other tidbit:
* Node-Webkit is now NW.JS and running with iojs

Node vs IOJS Binary, and long-term compatability:
https://github.com/iojs/io.js/issues/43

Discussion  of LTS of iojs for customers needing to run the same version with security/bug fixes backported
  * NodeSource
  * StrongLoop
  
Logos galore: https://github.com/iojs/logos
https://github.com/iojs/io.js/issues/37
  
From @maxogden https://gist.github.com/maxogden/d96123138522c84cdb25
*  io is a fork of node v0.12 (the next stable version of node.js, currently unreleased)
*  io.js will be totally compatible with node.js
*  the people who created io.js are node core contributors who have different ideas on how to run the project
*  it is not a zero-sum game. many core contributors will help maintain both node.js and io.js
*  io.js is not adversarial to node.js
*  the io.js project uses an open governance model
*  io is the 4th largest moon of jupiter. it also means 'input/output', which is what io.js is good at (asynchronous i/o)
*  'noders' is to node as 'ionians' is to io
*  you will probably be able to apt-get install iojs and get a node executable
*  the first stable release of io will be in January
*  the io team is working on an automated build infrastructure to enable a weekly release schedule
*  io core team (technical committee) meetings are on youtube
*  bugs etc fixed in node will be cherry-picked as necessary into io  
  
  
  
IOJS TC Meetings:
https://github.com/iojs/io.js/tree/v1.x/doc/tc-meetings


## So what breaks?
* Native modules (i.e. C++)
* List of Node modules not supported (yet) https://github.com/iojs/io.js/issues/456

## Installing iojs
* nvm support already shipped
* n support has been PRd, waiting for merge (https://github.com/tj/n)
* bew support TBD (https://github.com/Homebrew/homebrew/pull/35853)

On Windows, there's .msi installer
https://iojs.org/dist/v1.0.3/

On Linux, 