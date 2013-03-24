SSH Tunnel Utility Version 0.0.2
--------------------------------

The `ssh-tunnel` utility allows the user to maintain persistent SSH-tunnel
configurations. Furthermore, it automates startup, restart and shut-down
of these tunnels in bulk, whilst also providing a simple status overview.

One of the tool's main features is that it differs between `root`
and regular users. Thus, both can maintain their own configuration but use
the exact same mechanisms.

Note that, unlike similar software, `ssh-tunnel` does not ship with a GUI.
The script's primary purpose is to be used by system administrators and
CLI enthusiasts.


Requirements
------------

Below please find a list of software that is required by the `ssh-tunnel`
utility:

- **autossh**:                         http://www.harding.motd.ca/autossh/
- **OpenSSH**:                                     http://www.openssh.org/

The `/usr/bin/ssh-tunnel` script should work for most POSIX- and UNIX-like
operating systems that fulfill the aforementioned requirements.

The `/etc/init.d/ssh-tunnel` file, however, is a _Linux Standard Base_
_init-script_ that processes the the SSH-tunnel group definitions in the
`/etc/ssh/tunnel/groups-enabled` directory during the system boot. It has
been tested and verified with the following operating systems so far:

- _Debian GNU/Linux 7.x "wheezy"_
- _Debian GNU/Linux 6.x "squeeze"_
- _Debian GNU/Linux 5.x "lenny"_
- _Ubuntu 12.10 "Quantal Quetzal"_
- _Ubuntu 12.04 "Precise Pangolin"_

For systems without an _LSB_ model, one could either write the glue-code
necessary to port the scripts or use `cron(8)` to establish the tunnels.
Please refer to the _Configuration_ section for more information on this
topic.

Anyway, writing the glue-code is probably the better way to go. Note
that any contributions to the `ssh-tunnel` project are very welcome,
especially when increasing the portability!


Configuration
-------------

The `ssh-tunnel` command operates with so-called _tunnel groups_. This
are basically files containing one or more _tunnel definitions_, which are
not more than `ssh(1)` resp. `autossh(1)` commands where the command name
is replaced by the tunnel name, e.g.:

	user@host:~# cat default
    alpha -L 8888:target.example.com:80 user@proxy.example.com
	beta -R 2222:localhost:22 user@remote.example.com

The _tunnel group definition files_ for the `root` user are placed in
`/etc/ssh/tunnel/groups-enabled`. It is recommended that the items in
this directory are symlinks to `/etc/ssh/tunnel/groups-available`, but
that's not a requirment.

Regular users store their definitions in `~/.ssh/tunnel/group.d`.

The `ssh-tunnel` utility maintains a distinct `ssh-agent(1)` per user,
governing the private keys in `/etc/ssh/tunnel/keys-enabled` or, for
regular users, `~/.ssh/tunnel/keys.d`.
Note that any automated tunnel startup will fail if some private key
requires a password!

Linux system administrators can automate tunnel startup during system
boot via `/etc/init.d/ssh-tunnel` by using `update-rc.d`:

    root@host:~# update-rc.d ssh-tunnel start 01 S

This will cause connection attempts for all tunnel groups that are
linked into `/etc/ssh/tunnel/groups-enabled`.

As mentioned in the _Requirements_ section above, there is currently no
integration for systems without the _LSB_ _init-script_ model. However,
one can still automate the tunnel setup using `cron(8)`. Simply edit the
personal crontab (type `crontab -e`) and append the following lines:

    # m h dom mon dow command
    * * * * * /usr/bin/ssh-tunnel start >/dev/null

The above example also allows users without `root` access to automate
their setup.

Please note that the _tunnel definition files_ and _private key files_
should be accessible by their respective owners only.


Resources
---------

Below please find a list of resources associated with the `ssh-tunnel`
utility:

- **Source-code**:                  https://github.com/mjhennig/ssh-tunnel
- **Issue-Tracker**:         https://github.com/mjhennig/ssh-tunnel/issues


Copyright & License
-------------------

Copyright (c) 2013 Mathias J. Hennig

All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

1.  Redistributions of source code must retain the above copyright
    notice, this list of conditions and the following disclaimer.
2.  Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in
    the documentation and/or other materials provided with the
    distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDER AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

