## Remove the Locale Settings Warning
After a fresh install of Ubuntu 14.04 (Trusty Tahr) on the BeagleBone Black,
a warning is issued:
    perl: warning: Please check that your locale settings:
        LANGUAGE = (unset),
        LC_ALL = (unset),
        LANG = "en_US.UTF-8"
        are supported and installed on your system.

Resolution: Generate the requested locales and reconfigure.

```shell
sudo locale-gen en_US en_US.UTF-8 en_CA en_CA.UTF-8
sudo dpkg-reconfigure locales
```

Source: http://ubuntuforums.org/showthread.php?t=1346581
