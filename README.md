# Easily build rom for rosemary (Redmi Note 10S)

Sync the rom
---------------
To sync rom sources, we use a tool called "repo". Here are the requirements to build android:
- A 64-bit system.
- At least 400 GB of free disk space to check out and build the code (250 GB to check out + 150 GB to build).
- 64 GB of RAM. (Atleast 32GB will probably do)
- Any Linux distribution with GNU C Library (glibc) 2.17 or later.

We use a simple ``repo`` command to retrieve a manifest repository:
```bash
repo init -u <url>
```


After initializing the ``repo``, we finally ``sync`` it with a ``repo`` command:
```bash
repo sync -j$(nproc --all)
```
This can take few hours depending on your internet...

Clone the device sources
---------------
We have to clone the device sources to introduce our device to the ``android build system``


Here im giving you a manifest to sync the device sources with the rom.
To clone these manifest you gotta create the folder. Paste these commands in the root of your rom folder:
```bash
mkdir .repo/local_manifests
nano .repo/local_manifests/rosemary.xml
```

Now paste these in ``rosemary.xml`` file:
```bash
<manifest>
  <project path="device/xiaomi/rosemary" name="xiaomi-mt6785-dev/android_device_xiaomi_rosemary" remote="github" revision="lineage-21" />
  <project path="vendor/xiaomi/rosemary" name="xiaomi-mt6785-dev/proprietary_vendor_xiaomi_rosemary" remote="github" revision="lineage-21" />
  <project path="kernel/xiaomi/mt6785" name="xiaomi-mt6785-dev/android_kernel_xiaomi_mt6785" remote="github" revision="lineage-21" />
</manifest>
```
Use ```CTRL+X``` to exit


Some roms are providing hardware_xiaomi and device_mediatek_sepolicy_vndr while some roms are not. So we are using ``git clone`` command to clone these repos. Paste these commands in the root of your source folder:
```bash
git clone https://github.com/LineageOS/android_hardware_xiaomi.git hardware/xiaomi -b lineage-21 --depth=1
git clone https://github.com/LineageOS/android_device_mediatek_sepolicy_vndr.git device/mediatek/sepolicy_vndr -b lineage-21 --depth=1
```

Start Building
---------------
Now that we have cloned all device sources, time for the final step!
```bash
. build/envsetup.sh
```
```bash
lunch lineage_rosemary-userdebug
```
```bash
The rom specific command to start the build. You can learn them at the manifest repo of your rom
```
Happy buildings!

Next tutorial
--------------
How to adapt your device sources to your rom.
