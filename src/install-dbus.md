# DBus - Message bus

`D-Bus` is a message bus system, a simple way for applications to talk to one
another. It's a library that provides one-to-one communication between any two
applications.

`dbus-daemon` is the D-Bus message bus daemon. See [here](http://www.freedesktop.org/software/dbus/)
for more information about the big picture.

There are two standard message bus instances:

- `systemwide` message bus (installed on many systems as the `messagebus` init
service, but in Alpine Linux, service name is `dbus`)

- `per-user-login-session` message bus (started each time a user logs in).

`dbus-daemon` is used for both of these instances, but with a different
configuration file.

</br>

Use the following options to select different configuration files:


- `--session`: is equivalent to `--config-file=/usr/share/dbus-1/session.conf`

- `--system`: is equivalent to `--config-file=/usr/share/dbus-1/system.conf`

</br>

#### 1. Install `dbus`

```bash
doas apk --no-cache add dbus dbus-libs dbus-openrc xdg-dbus-proxy dbus-doc

# dbus-1.14.4-r0 - Freedesktop.org message bus system
# dbus-libs-1.14.4-r0 - D-BUS access libraries
# dbus-openrc-1.14.4-r0 - Freedesktop.org message bus system (OpenRC init scripts)
# xdg-dbus-proxy-0.1.4-r0 - Filtering proxy for D-Bus connections
# dbus-doc-1.14.4-r0 - Freedesktop.org message bus system (documentation)
```

</br>


#### 2. How to start `dbus`

```bash
doas service dbus start
# * Starting System Message Bus ... [ ok ]

service dbus status
# * status: started

doas service dbus stop
```

</br>

`dbus-uuidgen` will be called the first time to run `systemwide` `dbus-daemon`,
the purpose is to create the following bus ID file:

```bash
cat /etc/machine-id
# 2b0587d46f91d9fdf3998fb563831028
```

And then `/var/run/dbus/system_bus_socket` unix socket file will be created when
`systemwide` `dbus-daemon` instance is running. That setting comes from the 
`/usr/share/dbus-1/system.conf` configuration file:

```bash
<!-- Only listen on a local socket. (abstract=/path/to/socket
     means use abstract namespace, don't really create filesystem
     file; only Linux supports this. Use path=/whatever on other
     systems.) -->
<listen>unix:path=/var/run/dbus/system_bus_socket</listen>
```

</br>

#### 3. How to start session message bus instance

Usually, you don't need to always start systemwide message bus if you don't run
any programs relying on it.

You only need `session` message bus to run the particular program (e.g `Brave Browser`)

`dbus-run-session` is used to start a session bus instance of `dbus-daemon`
from a shell script, and start a specified program in that session. The
`dbus-daemon` will run for as long as the program does, after which it will
terminate.

One use is to run a shell with its own dbus-daemon in a text‐mode or
SSH session, and have the dbus-daemon terminate automatically on
leaving the sub‐shell.

</br>

For example

```bash
dbus-run-session flatpak run com.brave.Browser
```

After that, a new `dbus-daemon` instance created to run, and it will be terminated
when `Brave Browser` is closed.

```bash
procs dbus

# PID:▲  User │  TTY  Threads TCP    VmRSS │ Command
# │                    [bytes] │
# 11568 wison │ pts/1    1     [] 508.000K │ dbus-run-session flatpak run com.brave.Browser
# 11569 wison │ pts/1    1     []   1.320M │ dbus-daemon --nofork --print-address 5 --session
# 11580 wison │ pts/1    1     [] 652.000K │ bwrap --args 38 xdg-dbus-proxy --args=40
# 11581 wison │ pts/1    4     []   3.344M │ xdg-dbus-proxy --args=40
```

</br>

