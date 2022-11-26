# Package management

The best documentation is [here](https://wiki.alpinelinux.org/wiki/Alpine_Package_Keeper)

</br>


- How to use mirror

    Mirror settings in `/etc/apk/repositories`;

    ```bash
    #/media/cdrom/apks
    http://mirror.2degrees.nz/alpine/v3.17/main
    http://mirror.2degrees.nz/alpine/v3.17/community
    #http://mirror.2degrees.nz/alpine/edge/main
    #http://mirror.2degrees.nz/alpine/edge/community
    #http://mirror.2degrees.nz/alpine/edge/testing
    ```

    Mirror list is [Here](https://mirrors.alpinelinux.org/)

    </br>

- Update and upgrade:

    ```bash
    # Update repository indexes
    apk update

    # Install upgrades available from repositories
    apk upgrade

    # Install upgrades only for the particular package
    apk upgrade PACKGE_NAME_HERE

    # Reinstall or upgrade packages without modifying WORLD
    apk fix
    ```

    </br>

- Search packages to install:


    ```bash
    # Search package
    apk search SERACH_KEYWORD_HERE

    # Search package with short description in result
    apk search -v SERACH_KEYWORD_HERE

    # Search match package names exactly: -e, -x, --exact
    apk search -x PACKAGE_NAME_HERE
    ```

    </br>

- Search installed packages:

    ```bash
    # List user packages that already installed
    bat /etc/apk/world

    # List all packages that already installed
    apk list --installed | bat
    apk info -vv | bat
    ```

    </br>


- Package info:

    ```bash
    # Query package info (after you know the full packge name)
    apk info PACKAGE_NAME_HERE

    # List package dependencies
    apk info --depend PACKAGE_NAME_HERE

    # List package install location files
    apk info --content PACKAGE_NAME_HERE
    ```

    </br>

- Install and remove:

    ```bash
    # Install
    apk add PACKAGE_NAME_HERE

    # Remove a package (and dependencies that are no longer needed.)
    # Simulate the requested operation without making any changes
    apk del --simulate PACKAGE_NAME_HERE

    # Remove a package (and dependencies that are no longer needed.)
    apk del PACKAGE_NAME_HERE
    ```

    </br>

