Post Exploitation Wiki
======================

This wiki is powered by MDwiki which is a self contained wiki in a single HTML file.

All you have to do to use the wiki is clone the repo to anywhere you can open HTML, served or local.

Contributors please see here: https://github.com/mubix/post-exploitation-wiki/wiki/Contributor-Wiki

### Live Online Copy:

You can find a copy of the project online at: http://mubix.github.io/post-exploitation-wiki/. If you are reading this from the live website and want to get to the Github repository click here -> https://github.com/mubix/post-exploitation-wiki.

### Offline Use:

  1. Clone the repository or pull the archive ([download zip](https://github.com/mubix/post-exploitation-wiki/archive/master.zip)) of the repo
  2. Open index.html
  3. Most modern browsers don't allow the access of local files from a locally loaded HTML file. On Windows you can use [Mongoose Tiny](http://cesanta.com/downloads.html) or [HFS](http://www.rejetto.com/hfs/) to host the files locally. On OSX and Linux `python -m SimpleHTTPServer` seems to work just fine.

### Reference Binaries:

If the binary referenced isn't built into the respective OS, can be found here:
https://github.com/mubix/post-exploitation

#### Known issue with Chrome:

Chrome doesn't allow local file access from local files loaded in the
browser (ala index.html loading index.md). There are two ways around this. Use a web server to host
it (Apache, nginx, python SimpleHTTPServer, etc) or start Chrome with the `--allow-file-access-from-files`
argument. See here for more details: http://dynalon.github.io/mdwiki/#!faq.md


### More info about MDwiki:

http://dynalon.github.io/mdwiki/#!index.md
