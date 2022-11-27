# Control services

`OpenRC` is a dependency-based init system for Unix-like systems that maintains
compatibility with the system-provided `init system`, normally located in `/sbin/init`.
`OpenRC` is `Gentoo`'s native init system, although other init systems are available.

`OpenRC` will start necessary system services in the correct order at boot, manage
them while the system is in use, and stop them at shutdown.

Best document [here](https://wiki.alpinelinux.org/wiki/OpenRC)

</br>

- Supported runlevels

    - `default`

        Used if no runlevel is specified. (This is generally the runlevel you want to add services to.)

    - `hotplugged`
    - `manual`

    </br>

    The special runlevels are:

    - `sysinit`

        Brings up system specific stuff such as /dev, /proc and optionally /sys for Linux based systems. It also mounts /lib/rc/init.d as a ramdisk using tmpfs where available unless / is mounted rw at boot. rc uses /lib/rc/init.d to hold state information about the services it runs. sysinit always runs when the host first starts and should not be run again.

    - `boot`

        Generally the only services you should add to the boot runlevel are those which deal with the mounting of filesystems, set the initial state of attached peripherals and logging. Hotplugged services are added to the boot runlevel by the system. All services in the boot and sysinit runlevels are automatically included in all other runlevels except for those listed here.

    - `single`

        Stops all services except for those in the sysinit runlevel.

    - `reboot`

        Changes to the shutdown runlevel and then reboots the host.

    - `shutdown`

        Changes to the shutdown runlevel and then halts the host.

        </br>


- To check services and their set runlevels

    ```bash
    # List all services by runlevel category
    rc-status

    # Same result but in different output format, orderd by service name.
    # Result doesn't include status!!!
    rc-update show

    # List all services by runlevel category, include: sysinit, boot, shutdown
    rc-status --all

    # List all services without runlevel category
    rc-status --servicelist

    # Show services not assigned to any runlevel
    rc-status --unused
    ```

    </br>

- Add or remove services

    ```bash
    rc-update [options] add service <runlevel>
    rc-update [options] del service <runlevel>
    ```

    </br>

- Start or stop services

    ```bash
    rc-service <service> <start stop restart>
    ```

    </br>


```bash
# List services
rcctl ls all|failed|off|on|started|stopped [daemon]

# Start, stop or restart services
rcctl [-df] check|reload|restart|stop|start [daemon]

# Enable or disable when booting
rcctl disable|enable|order [daemon]
```

`[daemon]` is the service name which you can found that in `/etc/rc.d` folder

All services enable or not are configure in `/etc/rc.conf`, super simple:)

But plz **DO NOT** modify the `/etc/rc.conf`, just keep that to default settings,
as it will be changed when upgrading to new version. So, for your
personal customized service, just use `rcctl` to save them into `/etc/rc.conf.local`!!!

</br>
