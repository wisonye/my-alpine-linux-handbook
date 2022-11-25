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
    doas apk add --no-cache setup-xorg-base
    doas apk add --no-cache setxkbmap pciutils xrandr mesa-demos
    ```

    </br>


    Make sure to install the following packages, 

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

- Fix iMac GPU

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

- Fix MacBookPro Intel integrated GPU

