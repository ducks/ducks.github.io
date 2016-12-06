extends: default.liquid

title: |
  Automatic directory based git user config using smartcd
date: 6 December 2016 00:00:00 -0700
path: /:year/:month/:day/automatic-dir-based-git-user-config-smartcd
---

## Oh, The Places You&rsquo;ll Go!

When it comes to computer interfaces, I still feel most at home in a 
terminal, or cli, a command line interface. Most things I do can be done
more efficiently through a command or a script. Throughout any day, I 
am in and out of countless directories. Far too many to count without
writing a script to look through my history.

But not all directories are created equal. Depending on a number of factors,
your configuration may not be created equal either. 

For example, depending on which organization you're a part of, you may
want to make git commits with a specific name and/or email. I want to show
this example because 1) I couldn't find any docs or examples showing this,
and 2) I didn't get it to work the first time, and I'll probably forget it
again, so I'm leaving myself a note. 

## Enter smartcd

[Smartcd](https://github.com/cxreg/smartcd) is a neat tool that basically
allows you to perform actions on any directory change. It also comes
with an auxiliary library called `varstash` that will save the current
value of any variables, aliases, or shell function and temporarily change
or unset them. When you `cd` back out of that directory, those values
will automatically be reset to the original.

After installing smartcd, you can use it by cding into a directory and
running `smartcd edit enter`.

This will open a file in your editor that looks like this:

```
########################################################################
# smartcd enter - /Users/thedude/urbanachievers
#
# This is a smartcd script.  Commands you type will be run when you
# enter this directory.  The string __PATH__ will be replaced with
# the current path.  Some examples are editing your $PATH or creating
# a temporary alias:
#
#     autostash PATH=__PATH__/bin:$PATH
#     autostash alias restart="service stop; sleep 1; service start"
#
# See http://smartcd.org for more ideas about what can be put here
########################################################################
```

## Let me explain something to you. Um, I am not "Mr. Lebowski".

To set your git email and name, add the following lines:

```
autostash GIT_AUTHOR_NAME="The Dude"
autostash GIT_AUTHOR_EMAIL="thedude@theurbanachievers.io"
```

This simply sets the `GIT_AUTHOR_NAME` and `GIT_AUTHOR_EMAIL`
environment variables. Git will use these if present and fall back to
default configuration if not. Then, if we leave this directory, these
variables are reset, so git will automatically fallback to your global
configuration.

And voilà, any commits in this directory will contain the author information
we set in the `smartcd` enter script. You can edit this script again by
going back to the same directory and rerunning `smartcd edit enter`, or you
can find these scripts in the smartcd directory. By default this installs to
`~/.smartcd/scripts` but this can differ depending on how you installed.

Tweet me at [@rjgoldsborough](https://twitter.com/rjgoldsborough) with any
questions, concerns, or improvements. Thanks for reading.
