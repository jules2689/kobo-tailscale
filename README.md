# kobo-tailscale
A fork of https://github.com/videah/kobo-tailscale. 

Install scripts for getting [Tailscale](https://tailscale.com) running on Kobo e-readers and persisting through reboots.

## Supported devices
- *Kobo Libra 2*
- *Koba Libra Colour*/*Koba Libra Color*
- *Kobo Clara BW*

If you have another device and would like to contribute, please open a PR!

## Installation
1. Clone this repo
2. cd into the directory that corresponds with your device

```
cd libra-color
```

3. Edit the ```TAILSCALE_VERSION``` variable in ```install-tailscale.sh``` to the latest version of Tailscale

```bash
nano install-tailscale.sh # ensure TAILSCALE_VERSION=1.80.2 corresponds with latest Tailscale release.
```

4. Connect your device to your computer via USB and copy the folder that corresponds to your device to your devices onboard storage:

```
cp /repo/on/computer/libra-color /path/to/kobo/device
```
5. Eject and unplug device 
6. Enable developer settings by typing ```devmodeon``` into the kobo search bar.
7. Find device's IP address by going to *settings* --> *device settings*.
8. Telnet into your device with the credentials ```admin/admin```

```
telnet 192.168.0.100
```

9. cd into the directory you copied to the device -- it should be located at ```/mnt/onboard```:

```
cd /mnt/onboard/libra-color
```

10. run ```./install-tailscale.sh```
11. run ```tailscale up``` and authenticate via the provided URL
12. Turn off telnet by typing ```devmodeoff``` into kobo search bar.

## Uninstallation
Re-enable devmode on your kobo and telnet back in. Then run `uninstall-tailscale.sh` from the repo directory.

## DNS Issues
When there's no DNS manager on a system, Tailscale will resort to just [overwriting resolv.conf](https://tailscale.com/kb/1235/resolv-conf/)
which can cause issues on Kobo devices. If you find that DNS breaks after a while you can fix this by running
`tailscale set --accept-dns=false` on your device to prevent it from overwriting resolv.conf.

## Acknowledgements
[videah for the original repo](https://github.com/videah)

[Dylan Staley for initial work and scripts on the Kobo Sage](https://dstaley.com/posts/tailscale-on-kobo-sage)

[jmacindoe for documenting kernel module compilation on Kobo readers](https://github.com/jmacindoe/kobo-kernel-modules)
