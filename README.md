# Ubuntu Touch device tree for the Samsung Galaxy S10e

Description
-----------

This repository is to build Ubuntu Touch's vendor for the S10e (SM-G970F)

How to build Ubuntu Touch vendor
----------------------

* Make a workspace:

        mkdir -p ~/ut/repo
        cd ~/ut/repo

* Initialize the repo:

        repo init -u git://github.com/LineageOS/android.git -b lineage-17.1

* Create a local manifest:

        vim .repo/local_manifests/roomservice.xml

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <project name="temp-utvendor/android_device_samsung_beyond0lte" path="device/samsung/beyond0lte" />
            <project name="temp-utvendor/android_device_samsung_exynos9820-common" path="device/samsung/exynos9820-common" remote="github" />
            <project name="whatawurst/android_kernel_samsung_exynos9820" path="kernel/samsung/exynos9820" remote="github" />
            <project name="temp-utvendor/android_vendor_samsung_beyond0lte" path="vendor/samsung/beyond0lte" remote="github" />
            <project name="LineageOS/android_device_samsung_slsi_sepolicy" path="device/samsung_slsi/sepolicy" remote="github" />
            <project name="LineageOS/android_hardware_samsung" path="hardware/samsung" remote="github" />
        </manifest>

* Sync the repo:

        repo sync

* Extract vendor blobs

        cd device/samsung/beyond0lte
        ./extract-files.sh
        cd ../../../

* Setup the environment

        source build/envsetup.sh
        lunch lineage_beyond0lte-userdebug

* Build the vendor

        make vendorimage # the final image should be in out/target/product/beyond0lte/vendor.img
