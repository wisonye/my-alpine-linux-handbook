# Install bspwm window manager

- Install

    ```bash
    doas apk add --no-cache bspwm sxhkd alacritty feh dmenu polybar
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

        Then open it and add the start `bspwm` script at the bottom:

        **Super important!!!**

        **Super important!!!**

        **Super important!!!**

        Remember to remove the follow block, otherwise, `.xinitrc` will fall into
        a never ending loop: found `~/.xinitrc` and execute it and repeat that
        steps forever.

        ```bash
        # First try ~/.xinitrc
        if [ -f "$HOME/.xinitrc" ]; then
            echo "Found wison .xinitrc" >> "/home/wison/sys_xinitrc.log"
            XINITRC="$HOME/.xinitrc"
            if [ -x $XINITRC ]; then
                echo "Execute wison .xinitrc" >> "/home/wison/sys_xinitrc.log"
                # if the x bit is set on .xinitrc
                # it means the xinitrc is not a
                # shell script but something else
                exec $XINITRC "$@"
            else
                echo "Execute wison .xinitrc as shell script" >> "/home/wison/sys_xinitrc.log"
                exec /bin/sh "$HOME/.xinitrc" "$@"
            fi
        fi
        ```

        </br>


        So, here is the correct `.xinitrc`:

        ```bash
        #!/bin/sh
        # $Xorg: xinitrc.cpp,v 1.3 2000/08/17 19:54:30 cpqbld Exp $

        userresources=$HOME/.Xresources
        usermodmap=$HOME/.Xmodmap
        xinitdir=/etc/X11
        sysresources=$xinitdir/Xresources
        sysmodmap=$xinitdir/Xmodmap

        # Clear log
        echo "" > ~/xinitrc.log

        # merge in defaults and keymaps

        if [ -f $sysresources ]; then
            echo "merge system Xresources" >> ~/xinitrc.log
            xrdb -merge $sysresources
        fi

        if [ -f $sysmodmap ]; then
            echo "merge system Xmodmap" >> ~/xinitrc.log
            xmodmap $sysmodmap
        fi

        if [ -f $userresources ]; then
            echo "merge user Xresources" >> ~/xinitrc.log
            xrdb -merge $userresources
        fi

        if [ -f $usermodmap ]; then
            echo "merge user Xmodmap" >> ~/xinitrc.log
            xmodmap $usermodmap
        fi

        if [ -d /etc/X11/xinit/xinitrc.d ] ; then
            for f in /etc/X11/xinit/xinitrc.d/?* ; do
            │   [ -x "$f" ] && . "$f"
            done
            unset f
        fi

        echo "Start bspwm ......" >> ~/xinitrc.log
        exec bspwm -c ~/.config/bspwm/bspwmrc 2>~/.bspwm.err >~/.bspwm.out
        ```

        </br>

        The script is very simple, it does the following things:

        - Run your `~/.Xresources` if exists. Mine is for setting the `Xft.dpi` for
        my monitor.

        - Run your `~/.Xmodmap` if exists. Mine is for setting the keyboard.

        - Then run your window manager (the `bspwm` in this case)

        </br>

        Check the `~/.bspwm.err` if it doesn't run correctly.

        </br>

