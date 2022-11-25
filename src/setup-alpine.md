# setup-alpine

After booting from USB, then login as `root` (no password by default), and then
type `setup-alpine` to start the setup process.

</br>

- Timezone

    You can type `?` to list all supported time zones.

    For New Zealand, type `Pacific/Auckland`.

    </br>

- Mirror

    For New Zealand mirror, that's the `mirror.2degrees.nz` choice. Type **`65`**.

    [Here](https://mirrors.alpinelinux.org/) is the mirror list you can have a look for you country.

    </br>

- Disk mode

    After selecting the install target disk, it will ask like this:

    ```bash
    How could you like to use it?
    ```

    Choose `sys`

    </br>

- Setup console font after rebooting

    ```bash
    # Install terminal fonts (Monospace font)
    apk add terminus-font
    ```

    try out fonts in a virtual console by using:

    ```bash
    setfont /usr/share/consolefonts/ter-132n.psf.gz
    ```

    </br>


    If that's not ok, feel free to choose another terminal fonts in
    `/usr/share/consolefonts` folder. If ok, then set it into
    `/etc/conf.d/consolefont` with the your font like this:

    ```bash
    vi /etc/conf.d/consolefont

    # consolefont="ter-132n.psf.gz"
    ```

    </br>

    Enable it on boot:

    ```bash
    rc-update add consolefont boot
    ```

    Reboot to take effect.

    </br>


