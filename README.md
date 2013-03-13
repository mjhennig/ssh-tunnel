SSH Tunnel Utility Version 0.0.1
--------------------------------

The `ssh-tunnel` utility allows the user to maintain persistent SSH-tunnel
configurations. Furthermore, it automates startup, restart and shut-down
of these tunnels in bulk, whilst also providing a simple status overview.

One of the tool's main features is that it differs between `root`
and regular users. Thus, both can maintain their own configuration but use
the exact same mechanisms.

Note that, unlike similar software, `ssh-tunnel` does not ship with a GUI.
The script's primary purpose is to be used by administrators and CLI
enthusiasts - within `initrd`-based systems (or similar), for example,
in order to establish SSH tunnels during the system boot. Or explicitely,
e.g. when working from home whilst being required to access a company's
infrastructure. Or else. 


Requirements
------------

Below please find a list of software that is required by the ssh-tunnel
utility:

- *autossh*:                            http://www.harding.motd.ca/autossh/
- *OpenSSH*:                                        http://www.openssh.org/


Resources
---------

Below please find a list of resources associated with the ssh-tunnel
utility:

- *Source-code*:                     https://github.com/mjhennig/ssh-tunnel
- *Issue-Tracker*:            https://github.com/mjhennig/ssh-tunnel/issues


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

