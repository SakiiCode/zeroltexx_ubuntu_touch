I could get to the bootloop part here is a guide if anyone interested


Check my repo for the files at https://github.com/SakiiCode/zeroltexx_ubuntu_touch

* Copy the manifest from [samsung_zeroltexx.xml](https://github.com/SakiiCode/zeroltexx_ubuntu_touch/blob/master/samsung_zeroltexx.xml)
* `./halium/devices/setup zeroltexx`
* `source build/envsetup.sh`
* `breakfast zeroltexx`
* Copy the kernel config from [lineageos_zeroltexx_defconfig](https://github.com/SakiiCode/zeroltexx_ubuntu_touch/blob/master/lineageos_zeroltexx_defconfig)
  * It is what I got with official guide plus CONFIG_USER_NS=n, so no additional modifications
* Set your mountpoints. I provided mine in [fixup_mountpoints](https://github.com/SakiiCode/zeroltexx_ubuntu_touch/blob/master/fixup-mountpoints), yours may be different
  * The official guide mentioned that we shouldn't include partitions with emmc or auto type, keep that in mind
* Replace the SettingsLib package in [frameworks/base/packages](https://github.com/SakiiCode/zeroltexx_ubuntu_touch/tree/master/frameworks/base/packages)
* Copy the vendor libraries from the [vendor](https://github.com/SakiiCode/zeroltexx_ubuntu_touch/tree/master/vendor) folder
* `export USE_HOST_LEX=yes`
* `mka halium-boot`
* `mka systemimage`
* Build heimdall from source, the prebuilt 1.4.0 didn't work for me, only 1.4.2
* `heimdall flash --BOOT out/target/product/zeroltexx/halium-boot.img --no-reboot`
* Reboot manually straight to TWRP recovery
* `./halium-install -p ut <path-to>/rootfs.tar.gz <path-to>/halium/out/target/product/zeroltexx/system.img`
* Reboot to system

Then it bootloops because `Kernel panic - not syncing: stack-protector: Kernel stack is corrupted in: ffffffc0007577f8`.

Here is the log: https://pastebin.com/BYEAiJtH

It would be great if somebody could help
