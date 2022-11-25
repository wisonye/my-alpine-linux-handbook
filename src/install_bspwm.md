# Install bspwm window manager

- Install

    ```bash
    do as apk add --no-cache bspwm sxhkd alacritty feh dmenu polybar
    ```

    </br>


- Tricky things

    Plz make sure the `chmod +x ~/.config/bspwm/bspwmrc`!!!

    Plz make sure the `chmod +x ~/.config/bspwm/bspwmrc`!!!

    Plz make sure the `chmod +x ~/.config/bspwm/bspwmrc`!!!

    Otherwise, the `bspwm` runs but can't load the configuration file, as
    that configuration `it's a shell script`!!!! It can't run without the
    `+x` attribute!!!

    </br>


    **Super important!!!**

    **Super important!!!**

    **Super important!!!**

    Before you run `startx`, make sure you add yourself into the `input` group.
    Otherwise, you can't see anything after running `startx`!!!!

    If you see the log by running:

    ```bash
    bat ~/.local/share/xorg/Xorg.0.log
    ```

    Then you will see a lot of error like:

    ```bas
    failed to create input device '/dev/input/eventX'
    ```

    </br>


- How to start `bspwm` without installing any `DM (Dispaly Manager)`

    The **xinit** program allows a user to manually start and **Xorg** display
    server. The **startx** script is a front-end for **xinit**.

    - Customize your `.xinitrc`

        ```bash
        cp -rvf /etc/X11/xinit/xinitrc  ~/.xinitrc
        ```

        Then open it and let is start `bspwm` at the end:

        ```bash
        #!/bin/sh

        userresources=$HOME/.Xresources
        usermodmap=$HOME/.Xmodmap
        sysresources=/etc/X11/xinit/.Xresources
        sysmodmap=/etc/X11/xinit/.Xmodmap

        # merge in defaults and keymaps

        if [ -f $sysresources ]; then
            xrdb -merge $sysresources
        fi

        if [ -f $sysmodmap ]; then
            xmodmap $sysmodmap
        fi

        if [ -f "$userresources" ]; then
            xrdb -merge "$userresources"
        fi

        if [ -f "$usermodmap" ]; then
            xmodmap "$usermodmap"
        fi

        # start some nice programs

        if [ -d /etc/X11/xinit/xinitrc.d ] ; then
         for f in /etc/X11/xinit/xinitrc.d/?*.sh ; do
          [ -x "$f" ] && . "$f"
         done
         unset f
        fi

        # ------------------------------------------------------------------
        # Start window manager
        # ------------------------------------------------------------------
        bspwm -c ~/.config/bspwm/bspwmrc 2>~/.bspwm.err >~/.bspwm.out
        ```

        The script is very simple, it does the following things:

        - Run your `~/.Xresources` if exists. Mine is for setting the `Xft.dpi` for
        my monitor.

        - Run your `~/.Xmodmap` if exists. Mine is for setting the keyboard.

        - Then run your window manager (the `bspwm`` in this case)

        </br>

        Check the `~/.bspwm.err` if it doesn't run correctly.

        </br>

