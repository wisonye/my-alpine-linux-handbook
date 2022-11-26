# Open SSH

- Install and enable OpenSSH service

    ```bash
    # Install
    apk install openssh openssh-doc

    # Enable the sshd service so that it starts at boot
    rc-update add sshd

    # List services to verify sshd is enabled
    rc-status | rg sshd

    # Start the sshd service immediately and create configuration files:
    /etc/init.d/sshd start
    ```

    </br>

- Allow `root` to login

    Edit `doas vi /etc/ssh/sshd_config` and change the following settings:

    ```bash
    # Support values: yes, prohibit-password, forced-commands-only, or no.
    PermitRootLogin yes
    ```

    Then restart the service by running:

    ```bash
    rc-service sshd restart
    ```

    For more details, run `man sshd_config`.

    </br>



- Disable password to login for better safety reasons

    Watch [this](https://www.youtube.com/watch?v=tRJBC9rWH3A&list=PLlcnQQJK8SUjfkCph45fz6rC0de60LVZR&index=1) youtube video

    </br>

