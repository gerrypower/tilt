## How to fix a locale error

On Ubuntu, to fix a locale error, run these commands in the terminal:

```shell
export LC_ALL="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
sudo dpkg-reconfigure locales
```
