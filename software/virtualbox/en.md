+++
title = "VirtualBox"
lastmod = "2017-11-09T13:40:00+10:30"
+++
# VirtualBox

[VirtualBox](https://virtualbox.org) is an x86 virtualization software package developed by Oracle.

## Solus as Guest

For using VirtualBox in guest mode, it is important that you install the correct headers for your kernel,
as Solus support both a `current` and `lts` kernel.

If you aren't sure which kernel you
are running, run the following in terminal:

``` bash
uname -r
```

You will either have a `.current` or `.lts` suffix. Examples: `4.13.12-32.current` or `4.9.61-57.lts`

If you have an lts kernel, install the lts headers:

``` bash
sudo eopkg install linux-lts-headers
```

If you have a current kernel, installing the current headers:

``` bash
sudo eopkg install linux-current-headers
```

Make sure you have the necessary core packages installed:

``` bash
sudo eopkg upgrade
sudo eopkg install gcc make autoconf binutils xorg-server-devel
```

Reboot your system first so that it's all up to date.

Now install the **Guest Additions** : from the VirtualBox menu `Devices` -> `Insert Guest Additions CD image...`

On the guest Machine, open `Files` and click on the optical drive icon (CD name starts with VBOXADDITIONS) then click on the `Run Software` button and follow the on screen instructions.

{{< altimg "autorun.png" "help-center/software/virtualbox/" >}}

**Note:** For each kernel update you will need to rebuild the VirtualBox Modules. So simply remount the ISO and run the instructions again.

### Virtual machine settings

Here is a brief overview on some options you may want to set (you can only do it when your virtual machine is not running).

Select your guest machine and click on the Settings icon.

#### Clipboard Sharing,  Drag & Drop
By default, Clipboard Sharing and Drag'n'Drop are disabled, you can change this in `General` -> `Advanced`

{{< altimg "vbox-clipboard.png" "help-center/software/virtualbox/" >}}

#### Number of CPU
Virtual machines are created with only 1 CPU. You can change this in
`System` -> `Processor`

#### 3D Acceleration
For better performances, it is strongly recommended to enable 3D Acceleration in `Display` -> `Screen`

#### USB Controller
If you have installed the [extension pack](https://www.virtualbox.org/manual/ch01.html#intro-installing) and your hardware supports it, you set the USB Controller to USB 2.0 or 3.0,  in `USB`

Note: Access to USB is granted by the user group `vboxusers` on the **Host** operating system. You can add yourself to this group with the following command:

``` bash
sudo usermod -aG vboxusers `whoami`
```

#### Shared Folders

You can share folders from the Host to the Guest in `Shared Folders`

**Note:** auto-mounted shared folders are mounted into the `/media` directory, along with the prefix `sf_`. For example, the shared folder `myfiles` would be mounted to `/media/sf_myfiles`. Access to auto-mounted shared folders is only granted to the user group `vboxsf` on the Guest operating system.

Execute these commands to set the permissions and add yourself to the group:
``` bash
sudo chmod 755 /media
sudo usermod -aG vboxsf `whoami`
```

## Solus as Host

VirtualBox is available in the Software Center.

Using VirtualBox in host mode also requires that you install the correct version for your kernel,
as Solus support both a `current` and `lts` kernel.

If you aren't sure which kernel you
are running, run the following in terminal:

``` bash
uname -r
```

You will either have a `.current` or `.lts` suffix. Examples: `4.13.12-32.current` or `4.9.61-57.lts`

If you have an lts kernel, install VirtualBox for the lts kernel:

```sudo eopkg install virtualbox-lts```

If you have a current kernel, install VirtualBox for the current kernel:

``` bash
sudo eopkg install virtualbox-current```
