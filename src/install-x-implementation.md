# Install X implementation

The **`X`** Window System (**`X11`**, or simply **`X`**) is a windowing system for bitmap displays, 
common on Unix-like operating systems. It provides the basic framework for a GUI environment:

- Drawing
- Moving windows
- Interact with mouse and keyboard


It's `Client, Server` architecture

More information from [here](https://en.wikipedia.org/wiki/X_Window_System)

</br>

- Install `X` implementation


    ```bash
    doas setup-xorg-base

    # >> Enabling community repositories
    # fetch http://mirror.2degrees.nz/alpine/v3.17/main/x86_64/APKINDEX.tar.gz
    # fetch http://mirror.2degrees.nz/alpine/v3.17/community/x86_64/APKINDEX.tar.gz
    # v3.17.0-21-g62c4fc0981 [http://mirror.2degrees.nz/alpine/v3.17/main]
    # v3.17.0-22-g7482d95e0b [http://mirror.2degrees.nz/alpine/v3.17/community]
    # OK: 17802 distinct packages available
    # (1/58) Installing udev-init-scripts (35-r1)
    # (2/58) Installing udev-init-scripts-openrc (35-r1)
    # (3/58) Installing eudev-libs (3.2.11-r4)
    # (4/58) Installing eudev (3.2.11-r4)
    # (5/58) Installing eudev-openrc (3.2.11-r4)
    # (6/58) Installing mesa (22.2.4-r1)
    # (7/58) Installing hwdata-pci (0.364-r0)
    # (8/58) Installing libpciaccess (0.17-r0)
    # (9/58) Installing libdrm (2.4.114-r0)
    # (10/58) Installing musl-fts (1.2.7-r3)
    # (11/58) Installing libelf (0.187-r2)
    # (12/58) Installing mesa-glapi (22.2.4-r1)
    # (13/58) Installing libxau (1.0.10-r0)
    # (14/58) Installing libmd (1.0.4-r0)
    # (15/58) Installing libbsd (0.11.7-r0)
    # (16/58) Installing libxdmcp (1.1.4-r0)
    # (17/58) Installing libxcb (1.15-r0)
    # (18/58) Installing mesa-dri-gallium (22.2.4-r1)
    # (19/58) Installing libevdev (1.13.0-r0)
    # (20/58) Installing mtdev (1.1.6-r1)
    # (21/58) Installing libinput-libs (1.22.0-r0)
    # (22/58) Installing xf86-input-libinput (1.2.1-r0)
    # (23/58) Installing encodings (1.0.6-r0)
    # (24/58) Installing font-alias (1.0.4-r0)
    # (25/58) Installing libfontenc (1.1.6-r0)
    # (26/58) Installing libpng (1.6.38-r0)
    # (27/58) Installing freetype (2.12.1-r0)
    # (28/58) Installing mkfontscale (1.2.2-r1)
    # (29/58) Installing fontconfig (2.14.1-r0)
    # (30/58) Installing pkgconf (1.9.3-r0)
    # (31/58) Installing util-macros (1.19.3-r0)
    # (32/58) Installing font-misc-misc (1.1.2-r3)
    # (33/58) Installing font-cursor-misc (1.0.3-r3)
    # (34/58) Installing xkeyboard-config (2.37-r0)
    # (35/58) Installing libx11 (1.8.2-r0)
    # (36/58) Installing libxkbfile (1.1.1-r0)
    # (37/58) Installing xkbcomp (1.4.5-r1)
    # (38/58) Installing libxext (1.3.5-r0)
    # (39/58) Installing libice (1.0.10-r1)
    # (40/58) Installing libsm (1.2.3-r1)
    # (41/58) Installing libxt (1.2.1-r0)
    # (42/58) Installing libxmu (1.1.4-r0)
    # (43/58) Installing xauth (1.1.2-r0)
    # (44/58) Installing xmodmap (1.0.11-r0)
    # (45/58) Installing xrdb (1.2.1-r1)
    # (46/58) Installing xinit (1.4.1-r1)
    # (47/58) Installing xorg-server-common (21.1.4-r1)
    # (48/58) Installing libxfixes (6.0.0-r0)
    # (49/58) Installing libxxf86vm (1.1.5-r0)
    # (50/58) Installing libxshmfence (1.3.1-r0)
    # (51/58) Installing mesa-gl (22.2.4-r1)
    # (52/58) Installing libxfont2 (2.0.6-r0)
    # (53/58) Installing libepoxy (1.5.10-r0)
    # (54/58) Installing wayland-libs-server (1.21.0-r1)
    # (55/58) Installing mesa-gbm (22.2.4-r1)
    # (56/58) Installing pixman (0.42.2-r0)
    # (57/58) Installing libxcvt (0.1.2-r0)
    # (58/58) Installing xorg-server (21.1.4-r1)
    # Executing busybox-1.35.0-r29.trigger
    # Executing eudev-3.2.11-r4.trigger
    # Executing mkfontscale-1.2.2-r1.trigger
    # Executing fontconfig-2.14.1-r0.trigger
    # OK: 1937 MiB in 250 packages
    #  * Starting udev ...
    #  * Generating a rule to create a /dev/root symlink ...
    #  * Populating /dev with existing devices through uevents ...
    #  * Waiting for uevents to be processed ...
    ```

    </br>

    Install extra packages:

    ```bash
    doas apk add --no-cache setxkbmap pciutils xrandr mesa-demos
    ```

    </br>


    Make sure to install the following packages:

    ```bash
    doas apk add --no-cache xf86-video-modesetting xf86-video-vesa xf86-video-fbdev
    ```

    Otherwise, you will see the following errors in `~/.local/share/xorg/Xorg.0.log`
    and the `X` never can get rid of the **black screen**!!!

    ```bash
    Failed to load module "vesa" (module does not exist, 0)
    Failed to load module "fbdev" (module does not exist, 0)
    ```

    </br>

    For more details, plz read [here](https://wiki.alpinelinux.org/wiki/Alpine_setup_scripts#setup-xorg-base).

    </br>

- Identify your graphics card:

    If you're running Alpine Linux in  `Paralles Desktop` then you should see
    something like this:

    ```bash
    lspci -v | grep -A1 -e VGA -e 3D

    # 01:00.0 VGA compatible controller: Red Hat, Inc. Virtio GPU (rev 01) (prog-if 00 [VGA controller])
    #        Subsystem: Parallels, Inc. Device 0010
    ```

    </br>

    If you're running Apline Linux in real Apple Hardware, then you should see
    something like this:

    ```bash
    lspci -v | grep -A1 -e VGA -e 3D

    # VGA compatible controller: Intel Corproation Crystal ell Integrated Grahpics Controller (rev 08) (prog-if 00 [VGA controller])
    # Subsystem: Apple Inc. Device 0147

    ```

    So you know that's a GPU integrated inside Intel CPU and `Subsystem` show
    you the specific model for you to find the driver

    </br>

- Fix GPU driver (you don't need this if running in VM)

    [Here](https://wiki.archlinux.org/index.php/xorg) is the full list for all GPU brands.

    </br>

    - Install driver for `Radeon Pro 570X (4GB VRAM)`

        ```bash
        apk add xf86-video-amdgpu linux-firmware-amdgpu

        # After installing, the following files will be installed:
        # /usr/lib/xorg/modules/drivers/amdgpu_drv.so
        # /usr/share/X11/xorg.conf.d/10-amdgpu.conf
        ```

        Copy the AMD GPU configuration:

        ```bash
        # Create this folder if not exists
        doas mkdir /etc/X11/xorg.conf.d

        doas cp -rvf /usr/share/X11/xorg.conf.d/10-amdgpu.conf /etc/X11/xorg.conf.d
        ```

        </br>

    - Enable Kernel Modesetting (KMS)

        ```bash
        su root

        echo amdgpu >> /etc/modules
        echo fbcon >> /etc/modules

        apk add mkinitfs
        ```

        </br>

        `vi /etc/mkinitfs/mkinitfs.conf` and add `kms` to the first place
        like below:

        ```bash
        features="kms ata base ide scsi usb virtio ext4"
        ```

        Then update config:

        ```bash
        mkinitfs
        ```

        Reboot to take effect.

        </br>

        After reboot, you should see the `amdgpu` loaded like below:

        ```bash
        doas dmesg | rg amd
        ```

        ```bash
        lspci -v | grep -A10 -e VGA -e 3D
        ```

        </br>

        If you use another AMD/ATI GPU, plz read from [here](https://wiki.alpinelinux.org/wiki/Radeon_Video)

        If you use another AMD/ATI GPU, plz read from [here](https://wiki.alpinelinux.org/wiki/Radeon_Video)

        If you use another AMD/ATI GPU, plz read from [here](https://wiki.alpinelinux.org/wiki/Radeon_Video)

        </br>

- Test your video driver:

    After that, you can run the utilities below to check your OpenGL ability:

    ```
    # Check the OpenGL version
    glxinfo | grep "OpenGL version"

    # Test the OpenGL render framerate
    glxgears
    ```

    </br>

