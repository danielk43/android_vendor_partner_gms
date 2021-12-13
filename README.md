# microG Mobile Services

This is a collection of FOSS APKs, coupled with the respective Makefiles for an
easy integration in the Android build system.

To include them in your build, add a repo manifest file to include this repository as `vendor/partner_gms` and set
`WITH_GMS` to `true` when building.

Example manifest:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
    <project path="vendor/partner_gms" name="danielk43/android_vendor_partner_gms" remote="github" revision="main" />
</manifest>
```

Note: You do not need to set `CUSTOM_PACKAGES` for the packages to be included when building with [lineageos4microg/docker-lineage-cicd](https://github.com/lineageos4microg/docker-lineage-cicd).

The included APKs are:
 * FDroid packages (binaries sourced from [here](https://f-droid.org/packages/org.fdroid.fdroid/) and [here](https://f-droid.org/packages/org.fdroid.fdroid.privileged/))
   * FDroid: a catalogue of FOSS (Free and Open Source Software) applications for the Android platform
   * FDroid Privileged Extension: a FDroid extension to ease the installation/removal of apps
   * LocalGsmNlpBackend: UnifiedNlp backend that uses local GSM data to resolve user location
   * NominatimGeocoderBackend: Geocoder backend that uses OSM Nominatim service.
   * additional_repos.xml: a configuration file to include the [microG](https://microg.org/fdroid.html), [Bromite](https://www.bromite.org/fdroid), and [IzzyOnDroid](https://apt.izzysoft.de/fdroid/repo) FDroid repositories in the ROM (requires FDroid >= 1.5)
 * microG packages (binaries sourced from [here](https://microg.org/download.html) and [here](https://github.com/microg/android_frameworks_mapsv1))
   * GmsCore: the main component of microG, a FOSS reimplementation of the Google Play Services (requires GsfProxy and FakeStore for full functionality)
   * GsfProxy: a GmsCore proxy for legacy GCM compatibility
   * FakeStore: an empty package that mocks the existence of the Google Play Store
   * com.google.android.maps: legacy microG's mapsv1 reimplementation
 * AuroraOSS packages (binaries sourced from [here](https://gitlab.com/AuroraOSS))
   * AuroraDroid: an alternate to the FDroid app store
   * AuroraStore: an alternate to Google's Play Store
   * AuroraServices: a system / root application that integrates with the Aurora line of products
 * GrapheneOS packages (binaries sourced from [here](https://github.com/GrapheneOS/PdfViewer/releases))
   * PdfViewer: a simple Android PDF viewer based on pdf.js and content providers

These are official unmodified prebuilt binaries, signed by the
corresponding developers, except for:
 * com.google.android.maps, as the JAR and the XML have been extracted from the ZIP on the [microG's GitHub release page](https://github.com/microg/android_frameworks_mapsv1/releases)
 * additional_repos.xml, to include the nonstandard repositories in FDroid
