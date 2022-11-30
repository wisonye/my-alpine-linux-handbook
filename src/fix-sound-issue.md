# Fix sound issue

- Install the packages below:

    ```bash
    doas apk --no-cache add pulseaudio alsa-utils

    # Reboot
    ```

</br>

- Run `alsamixer` and tune your sound setting

    - Press `F6` to choose your major audio playback device:

        ![select-audo-device.png](./images/select-audo-device.png)

    - After selecting your correct audio playback device, 
    press `F3` to setup the `Playback` volume. Use left/right arrow key 
    to switch item and use Up/Down arrow key to change the volume. 

        ![change-playback-volume.png](./images/change-playback-volume.png)

</br>

- Optionally, you can install **`pavucontrol`** GUI volume control app

    ```bash
    doas apk --no-cache add pavucontrol
    ```

    It looks like this:


    ![pulse-audio-volume-control.png](./images/pavucontrol-volume.png)

    </br>


