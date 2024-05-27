# microG Mobile Services

This is a collection of FOSS APKs, coupled with the respective Makefiles for an
easy integration in the Android build system.

To include them in your build, add a repo manifest file to include this repository as `vendor/partner_gms` and set
`WITH_GMS` to `true` when building.

For traditional install with MicroG, set `GMS_MAKEFILE` to `gms_fdroid.mk`.  
For full install in addition to MicroG, set `GMS_MAKEFILE` to `gms_full.mk`.  
For only open source apks in this fork, set `GMS_MAKEFILE` to `gms_extras.mk`.  
Or create and set a custom makefile

Example manifest:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
    <project path="vendor/partner_gms" name="danielk43/android_vendor_partner_gms" remote="github" revision="main" />
</manifest>
```

Note 1. You do not need to set `CUSTOM_PACKAGES` for the packages to be included when building with [our Docker engine](https://github.com/lineageos4microg/docker-lineage-cicd).

Note 2. LineageOS now supports ***restricted*** signature spoofing, so it is no longer neccessary to patch their sources, unless you want ***unrestricted*** signature spoofing 

Note 3. If you encounter problems related to APK / app signing when using these components you may need to add the following line in the Android.mk for the component in question:
```
LOCAL_REPLACE_PREBUILT_APK_INSTALLED := $(LOCAL_PATH)/$(LOCAL_MODULE).apk
```
Such problems can occur when
* the app / APK is resigned with your keys; (this should not happen if the line LOCAL_CERTIFICATE := PRESIGNED is included in the app makefile)
* the app / APK signatures are 'stripped` during the during the deodexing phase of the build. For some apps the deodexed app ends up unsigned, and so will not run.

The symptoms of the problem as some apps from this repo (e.g. FakeStore and GmsCore) missing completely from your launcher and acting like they're not installed.

(Some background to this issue can be found [here](https://github.com/lineageos4microg/android_vendor_partner_gms/issues/30) and [here](https://gitlab.com/iode/os/public/lineage/vendor_extra/-/issues/4))

---------------

The included APKs are:
 * FDroid packages (binaries sourced from [here](https://f-droid.org/packages/org.fdroid.fdroid/) and [here](https://f-droid.org/packages/org.fdroid.fdroid.privileged/))
   * FDroid: a catalogue of FOSS (Free and Open Source Software) applications for the Android platform
   * FDroid Privileged Extension: a FDroid extension to ease the installation/removal of apps
   * additional_repos.xml: a configuration file to include the [microG](https://microg.org/fdroid.html), and [IzzyOnDroid](https://apt.izzysoft.de/fdroid/repo) FDroid repositories in the ROM (requires FDroid >= 1.5)
 * microG packages (binaries sourced from [here](https://microg.org/download.html))
   * GmsCore: the main component of microG, a FOSS reimplementation of the Google Play Services (requires GsfProxy for full functionality)
   * GsfProxy: a GmsCore proxy for legacy GCM compatibility
 * Open Source apks
   * AuroraStore: an alternate to Google's Play Store (binaries sourced from [here](https://gitlab.com/AuroraOSS/AuroraStore/-/releases))
   * Obtainium: allows you to install and update Open-Source Apps directly (binaries sourced from [here](https://github.com/ImranR98/Obtainium/releases))
   * PdfViewer: a simple Android PDF viewer (binaries sourced from [here](https://github.com/GrapheneOS/PdfViewer/releases))

These are official unmodified prebuilt binaries, signed by the
corresponding developers.
