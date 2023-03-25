---
Title: Arch Linux
type: list
---


Arch Linux is a lightweight and flexible Linux distribution that tries to Keep It Simple.



### To increase disk space by cleaning packages cache -

1. 
    ```
    sudo ls /var/cache/pacman/pkg/ | wc -l
    ```
1. 
    ```
    du -sh /var/cache/pacman/pkg/
    ```
1. 
    ```
    sudo pacman -Sc
    ```

