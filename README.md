# FFmpeg Specific Auto-Builds

[BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds) builds **full** versions of FFmpeg that include all dependencies,
thus the size of each asset is somehow too large.     
For example, `ffmpeg-master-latest-win64-lgpl.zip` ≈ 95.9 MB.   
Here, the aim of this repo is to smallize the asset size by customize the build configuration.  
Follow the steps below.



## Specify the Targets and Variants
See <https://github.com/ButterAndButterfly/FFmpeg-Builds/blob/9730dd67c1cebfb2a6bde84b6ba7c181a8984a51/.github/workflows/release.yml#L20-L21>

## Specify the build configuration
See the [commit](https://github.com/ButterAndButterfly/FFmpeg-Builds/commit/9730dd67c1cebfb2a6bde84b6ba7c181a8984a51). Or   
<https://github.com/ButterAndButterfly/FFmpeg-Builds/blob/9730dd67c1cebfb2a6bde84b6ba7c181a8984a51/build.sh#L69>  

You should ensure the configuration is part of the Variants,   
e.g. `--enable-gpl --enable-version3` is **invalid** for Variant `lgpl`.


For more details, see [release.yml](.github/workflows/release.yml)

