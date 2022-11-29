# Install docker

- Installation

    ```bash
    doas apk --no-cache add docker

    # (1/15) Installing runc (1.1.4-r3)
    # (2/15) Installing containerd (1.6.10-r0)
    # (3/15) Installing containerd-openrc (1.6.10-r0)
    # (4/15) Installing libmnl (1.0.5-r0)
    # (5/15) Installing libnftnl (1.2.4-r0)
    # (6/15) Installing iptables (1.8.8-r2)
    # (7/15) Installing iptables-openrc (1.8.8-r2)
    # (8/15) Installing ip6tables (1.8.8-r2)
    # (9/15) Installing ip6tables-openrc (1.8.8-r2)
    # (10/15) Installing tini-static (0.19.0-r1)
    # (11/15) Installing docker-engine (20.10.21-r1)
    # (12/15) Installing docker-openrc (20.10.21-r1)
    # (13/15) Installing docker-cli (20.10.21-r1)
    # (14/15) Installing docker (20.10.21-r1)
    # Executing docker-20.10.21-r1.pre-install
    # (15/15) Installing docker-fish-completion (20.10.21-r1)
    # Executing busybox-1.35.0-r29.trigger
    # OK: 2531 MiB in 409 packages
    ```

    Connecting to the Docker daemon through its socket requires you to add yourself to the `docker` group.

    ```bash
    doas addgroup YOUR_USER_NAME_HERE docker
    ```

    Re-login to take affect.

    </br>

    What components are installed be default?
    
    ![docker-pacman-install.png](./images/docker-pacman-install.png)

</br>

- Handle `docker` as a service

    - Query status

        ```bash
        doas service docker status
        ```
    - Start

        ```bash
        doas service docker start
        ```
    - Stop

        ```bash
        doas service docker stop
        ```

    - Enable auto start

        ```bash
        doas rc-update add docker boot
        ```

    - Disable auto start

        ```bash
        doas rc-update del docker boot
        ```

        </br>


- Install `docker-compose`

    ```bash
    sudo bash -c 'curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" \
        -o /usr/bin/docker-compose && chmod +x /usr/bin/docker-compose'
    ```
