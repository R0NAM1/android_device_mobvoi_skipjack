# TWRP for Skipjack (Ticwatch C2+)
Scripts and device configuration for TWRP to compile to Skipjack (Ticwatch C2+).

(Only for use with the +, for some insane reason they kept codenames between hardware revisions, since it WAS just a RAM upgrade and CPU upgrade it should have been fine, but they also made it so Android 9 is the only kernel that supports it, so the repo I forked this from (OR TWRP's offical image) just doesn't work)


## How to compile

Install the build tools / dependencies:
```sh
apt install openjdk-8-jdk make rsync bc bison build-essential g++-multilib git make python zip schedtool
```

Create your directory and get all the files (Beware of repo sync, it downloads like 40 GB, just so you know, and it is SLOW sometimes).
```sh
mkdir skipjack_twrp
cd skipjack_twrp/
mkdir -p device/mobvoi/
git clone https://github.com/R0NAM1/android_device_mobvoi_skipjack.git device/mobvoi/skipjack
git clone --verbose --single-branch --depth=1 --branch android-msm-skipjack-3.18-oreo-wear-dr https://android.googlesource.com/kernel/msm device/mobvoi/skipjack/kernel
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-6.0
repo sync
```

Ready to compile? WRONG: For some reason I needed to run 'sudo chown 777 -R *' (Something something git keeps permissions blah blah)

Now we can compile:
```sh
. build/envsetup.sh
export LANG=C
lunch omni_skipjack-eng
make -j4 recoveryimage
```

And you have your working image!

Or you can just download the releases on the right there ------->

(Original instructions shamelessly taken from https://github.com/MagneFire/omni_twrp_device_smelt)
