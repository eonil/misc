Ubuntu
======

Locale Issue
------------
Not specifically to Ubuntu, but there's a very annoying issue with
Ubuntu server configuration.

When you connect to an Ubuntu server it will keep failing setting 
locales like this when you do something.

    perl: warning: Setting locale failed.
    perl: warning: Please check that your locale settings:
        LC_ALL = (unset),
        LANG = "en_US.UTF-8"
        are supported and installed on your system.
    perl: warning: Falling back to the standard locale ("C").

[Here's the solution!](http://stackoverflow.com/a/2510548/246776)

In summary, edit `/etc/ssh/sshd_config` file, and comment out this line.

    AcceptEnv LANG LC_*

Don't forget to restart server after editing it.

Execute this to test whether the locale is working well.

    perl -e exit

