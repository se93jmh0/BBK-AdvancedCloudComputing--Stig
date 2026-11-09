# sudo vs root

> Why do Linux and cloud systems usually ask us to work with a normal user and
> use sudo, instead of working directly as root?

The superuser (user ID 0), which normally has the login name of root (Stephens &
Rago, 2013), is typically effectively omnipotent on Unix-like systems, and as
such great care must be taking when running anything as root, because the
operating system is not going to stop you if you tell it to do something silly.

As an example, consider typing the following at a Bash prompt:

    rm -rf Jan*

Accidentally striking the space bar while typing the `n` key could actually
result in:

    rm -rf Jan *

Which, depending on what the current working directory is, could be relatively
harmless, or it could be utterly catastrophic.

Instead, `sudo` makes such accidents less likely, for two reasons:
* typing sudo at the beginning of a command focuses the mind on the fact that
  whatever comes next can be very destructive;
* having to type a password interrupts the trivial flow of simply hitting the
  Return key.

As a result, some Linux distributions such as Ubuntu these days recommend a
purely `sudo`-based approach to system administration as canonical.

----

Stevens, W. Richard, and Rago, Stephen (2013) _Advanced programming in the UNIX environment_. Third Edition. Addison-Wesley.

Ubuntu (2026) _Bash scripting for beginners_. Available at:
https://wiki.ubuntu.com/Bash_scripting_for_beginners#Running_commands_as_root
(Accessed: 9 November 2026).
