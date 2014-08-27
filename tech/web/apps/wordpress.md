# Wordpress

## General Exploitation Tips For Wordpress Installations
Most of the problems from Wordpress installations are not due to Wordpress itself but rather a number of other factors. Because of this I believe it best if we look at some various problems with typical installations and how they could impact the security of the system, as well as how to test for them where applicable.

### Outdated installations
Whilst many of the RCE and more high impact bugs have been fixed in the latest releases, there still exists unknown bugs in the Wordpress code that could compromise the sites security. Check to see if the Wordpress site is running an old version of Wordpress. If your running Wordpress yourself, make sure its updated to the latest version.

### Outdated Plugins
This is probably the main reason most Wordpress sites get hacked, and is by and far the largest source of vulnerabilites. To give some examples of how bad this problem is, take a look at [this news article](http://arstechnica.com/security/2014/07/mass-exploit-of-wordpress-plugin-backdoors-sites-running-joomla-magento-too/), which explains a case earlier this year (2014) in which a vulnerability in a very popular plugin called MailPoet was crafted into a worm that was used to backdoor thousands of Wordpress websites. In a similar manner, other plugins may contain vulnerable code that could allow any number of attacks from RCE to XSS to CSRF.

To audit these website's plugins, I would recommend using WPScan ([available here](http://wpscan.org/)), which is a tool created to help you identify vulnerable Wordpress installations in your network.

To specifically check for outdated plugins, use the following code with WPScan:

```bash
./wpscan.rb --url *url to target* --enumerate p
```

### Weak Passwords
Users may also have weak passwords that can be easily bruteforced or guessed. Using the WPScan tool from earlier, it is quite easy to start guessing passwords with a provided wordlist:

```bash
./wpscan.rb --url *url to target* --wordlist *your wordlist* --username *username to target*
```

You can prepend the --threads *number of thread* option if you wish to use more threads against the target.

You may want to retrieve the current users on the Wordpress installation first by preforming the following command:

```bash
./wpscan.rb --url *url to target* --enumerate u
```

### Using the same username for your posts as your login username
Expanding on the post above, if the target uses the same username for their posts as they do their login (which you should be able to find via the above command anyway, but in case it doesn't this may help), it will greatly assist you when you try to later brute force their password. Therefore take a note of the names of the users who are posting on the blog for later dictionary attacks.

### Not setting the right permissions on various directories
If you start enumerating directories with something like DirBuster and find interesting directories, it may be useful to check their permissions to see if they have been configured incorrectly. A in-configured directory could provide a foothold into the target.

### Not locking down user registration
If the site accidentally enables user registration without a proper need, you may be able to create a user account on the Wordpress site that could allow you to gain additional privileges to other parts of the website. If you manage to find a vulnerability in one of those components, the new user account could potentially be used in combination with the vulnerability to gain access to the box.

### Leaving the "test" database available on the MySQL installation
If the default "test database is available on the MySQL installation on the Wordpress server, any user can alternate or change this database, thus allowing easier navigation and exploitation of the database.

### Vulnerable TimThumb Installations
Best bet to fixing these set of vulnerabilities is to actually just disable TimThumb entirely. As the creator states [here](http://www.infosecurity-magazine.com/news/timthumb-zero-day-exploit-weakens-wordpress/), he no longer maintains TimThumb except for major security issues and newer versions of Wordpress already have the features that his tool offers built in.

However its still worth checking for TimThumb installations as quite a lot of Wordpress sites do use it and its prone to a number of different bugs. To do this, we can use the following command with WPScan:

```bash
./wpscan.rb --url *url to target* --enumerate tt
```

### Outdated Themes
Yes, even themes can have vulnerabilities within them as well, though this tends to happen less often than with plugins or TimThumb.

To check for vulnerabilities with a site's Wordpress themes, one can use the following check:

```bash
./wpscan.rb --url *url to target* --enumerate t
```

### Vulnerable Hosting Servers
Well it doesn't matter if you secure the hell out the Wordpress site, if your hosting provider is being silly with their security, you can just get in through the other door so to say. Therefore, if your allowed to and you obtain permission from the hosting provider, you may want to check to see if you can't get in through the hosting provider's insecure set up of the box the Wordpress server is running on.

Now obviously this could turn into a very sticky situation, so I would recommend caution when taking this approach, and make sure you have permission before you perform each step. Depending on what you get permission to test, will in turn determine how options you have for compromising the box an alternative way.


## Vulnerability Database
One may also wish to check out wpsecure.net's vulnerability database for Wordpress. While not bleeding edge by any means, its fairly up to date (last updated in July when I checked in September), and maintains a good catalog of vulnerabilities in various Wordpress plugins.

You can find a copy of it [here](http://wpsecure.net/category/exploits/). An RSS feed of the same list can be found [here](http://www.wpsecure.net/category/exploits/feed/)

## Credits
Huge thanks to [wpsecure.net](http://www.wpsecure.net) for putting together a comprehensive set of tutorials and guides for securing Wordpress installations and for maintaining a fairly up to date vulnerability catalog.

