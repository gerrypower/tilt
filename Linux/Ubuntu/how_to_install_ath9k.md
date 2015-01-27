## How to Install or Upgrade [Ath9k Wireless Drivers](https://wireless.wiki.kernel.org/en/users/Drivers/ath9k)

1. Get the latest toolset and the kernel headers for your distro
```shell
sudo apt-get update
sudo apt-get dist-upgrade
apt-get install gcc build-essential linux-headers-generic linux-headers-`uname -r`
```
2. Download the [latest backports](https://www.kernel.org/pub/linux/kernel/projects/backports/stable/)
3. Extract
4. Cleanup
```shell
make clean
make
```
5. Select the drivers as per the instructions in step 4.
```shell
make defconfig-ath9k
```
6. Build
```shell
make
```
7. Install
```shell
sudo make install
```
8. Load
```shell
echo "ath9k" | sudo tee -a /etc/modules
echo "ath9k_htc" | sudo tee -a /etc/modules
```
9. Reboot
10. If device was not found, bind it to the driver
```shell
echo "[YOUR USB DEVICE ID](https://wikidevi.com/wiki/Main_Page)" | tee /sys/bus/usb/drivers/ath9k_htc/new_id
```
